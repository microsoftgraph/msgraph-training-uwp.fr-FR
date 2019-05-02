<!-- markdownlint-disable MD002 MD041 -->

Dans cet exercice, vous allez incorporer Microsoft Graph dans l’application. Pour cette application, vous allez utiliser la [bibliothèque cliente Microsoft Graph pour .net](https://github.com/microsoftgraph/msgraph-sdk-dotnet) pour effectuer des appels à Microsoft Graph.

## <a name="get-calendar-events-from-outlook"></a>Obtenir des événements de calendrier à partir d’Outlook

Commencez par ajouter une nouvelle page pour l’affichage Calendrier. Cliquez avec le bouton droit sur le projet du **didacticiel Graph** dans l’Explorateur de solutions et choisissez **Ajouter un nouvel élément >...**. Choisissez **page vierge**, entrez `CalendarPage.xaml` dans le champ **nom** , puis choisissez **Ajouter**.

Ouvrez `CalendarPage.xaml` et ajoutez la ligne suivante à l’intérieur `<Grid>` de l’élément existant.

```xml
<TextBlock x:Name="Events" TextWrapping="Wrap"/>
```

Ouvrez `CalendarPage.xaml.cs` et ajoutez les instructions `using` suivantes en haut du fichier.

```cs
using Microsoft.Toolkit.Services.MicrosoftGraph;
using Microsoft.Toolkit.Uwp.UI.Controls;
using Newtonsoft.Json;
```

Ajoutez ensuite les fonctions suivantes à la `CalendarPage` classe.

```cs
private void ShowNotification(string message)
{
    // Get the main page that contains the InAppNotification
    var mainPage = (Window.Current.Content as Frame).Content as MainPage;

    // Get the notification control
    var notification = mainPage.FindName("Notification") as InAppNotification;

    notification.Show(message);
}

protected override async void OnNavigatedTo(NavigationEventArgs e)
{
    // Get the Graph client from the service
    var graphClient = MicrosoftGraphService.Instance.GraphProvider;

    try
    {
        // Get the events
        var events = await graphClient.Me.Events.Request()
            .Select("subject,organizer,start,end")
            .OrderBy("createdDateTime DESC")
            .GetAsync();

        // TEMPORARY: Show the results as JSON
        Events.Text = JsonConvert.SerializeObject(events.CurrentPage);
    }
    catch(Microsoft.Graph.ServiceException ex)
    {
        ShowNotification($"Exception getting events: {ex.Message}");
    }

    base.OnNavigatedTo(e);
}
```

Examinez le code dans `OnNavigatedTo` est en cours d’exécution.

- L’URL qui sera appelée est `/v1.0/me/events`.
- La `Select` fonction limite les champs renvoyés pour chaque événement à ceux que l’affichage utilise réellement.
- La `OrderBy` fonction trie les résultats en fonction de la date et de l’heure de leur création, avec l’élément le plus récent en premier.

Juste avant d’exécuter l’application, pour pouvoir accéder à cette page de calendrier, modifiez la `NavView_ItemInvoked` méthode dans le `MainPage.xaml.cs` fichier de manière à remplacer la `throw new NotImplementedException();` ligne comme suit.

```cs
case "calendar":
    RootFrame.Navigate(typeof(CalendarPage));
    break;
```

Vous pouvez maintenant exécuter l’application, vous connecter et cliquer sur l’élément de navigation **calendrier** dans le menu de gauche. Vous devriez voir un dump JSON des événements sur le calendrier de l’utilisateur.

## <a name="display-the-results"></a>Afficher les résultats

À présent, vous pouvez remplacer le vidage JSON par un texte pour afficher les résultats de manière conviviale. Remplacez tout le contenu de `CalendarPage.xaml` par par ce qui suit.

```xml
<Page
    x:Class="graph_tutorial.CalendarPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:graph_tutorial"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <Grid>
        <controls:DataGrid x:Name="EventList" Grid.Row="1"
                AutoGenerateColumns="False">
            <controls:DataGrid.Columns>
                <controls:DataGridTextColumn
                        Header="Organizer"
                        Width="SizeToCells"
                        Binding="{Binding Organizer.EmailAddress.Name}"
                        FontSize="20" />
                <controls:DataGridTextColumn
                        Header="Subject"
                        Width="SizeToCells"
                        Binding="{Binding Subject}"
                        FontSize="20" />
                <controls:DataGridTextColumn
                        Header="Start"
                        Width="SizeToCells"
                        Binding="{Binding Start.DateTime}"
                        FontSize="20" />
                <controls:DataGridTextColumn
                        Header="End"
                        Width="SizeToCells"
                        Binding="{Binding End.DateTime}"
                        FontSize="20" />
            </controls:DataGrid.Columns>
        </controls:DataGrid>
    </Grid>
</Page>
```

Cela remplace le `TextBlock` par un `DataGrid`. Maintenant, `CalendarPage.xaml.cs` ouvrez et remplacez `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);` la ligne par ce qui suit.

```cs
EventList.ItemsSource = events.CurrentPage.ToList();
```

Si vous exécutez l’application maintenant et sélectionnez le calendrier, vous devez obtenir la liste des événements dans une grille de données. Toutefois, les valeurs de **début** et de **fin** sont affichées de manière non conviviale. Vous pouvez contrôler le mode d’affichage de ces valeurs à l’aide d’un [convertisseur de valeur](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter).

Cliquez avec le bouton droit sur le projet du **didacticiel Graph** dans l’Explorateur de solutions et choisissez **Ajouter une classe >.**... Nommez la `GraphDateTimeTimeZoneConverter.cs` classe, puis choisissez **Ajouter**. Remplacez tout le contenu du fichier par ce qui suit.

```cs
using Microsoft.Graph;
using System;

namespace graph_tutorial
{
    class GraphDateTimeTimeZoneConverter : Windows.UI.Xaml.Data.IValueConverter
    {
        public object Convert(object value, Type targetType, object parameter, string language)
        {
            DateTimeTimeZone date = value as DateTimeTimeZone;

            if (date != null)
            {
                // Resolve the time zone
                var timezone = TimeZoneInfo.FindSystemTimeZoneById(date.TimeZone);
                // Parse method assumes local time, which may not be the case
                var parsedDateAsLocal = DateTimeOffset.Parse(date.DateTime);
                // Determine the offset from UTC time for the specific date
                // Making this call adjusts for DST as appropriate
                var tzOffset = timezone.GetUtcOffset(parsedDateAsLocal.DateTime);
                // Create a new DateTimeOffset with the specific offset from UTC
                var correctedDate = new DateTimeOffset(parsedDateAsLocal.DateTime, tzOffset);
                // Return the local date time string
                return correctedDate.LocalDateTime.ToString();
            }

            return string.Empty;
        }

        public object ConvertBack(object value, Type targetType, object parameter, string language)
        {
            throw new NotImplementedException();
        }
    }
}
```

Ce code prend la structure [dateTimeTimeZone](https://developer.microsoft.com/en-us/graph/docs/api-reference/v1.0/resources/datetimetimezone) renvoyée par Microsoft Graph et l’analyse en un `DateTimeOffset` objet. Il convertit ensuite la valeur dans le fuseau horaire de l’utilisateur et renvoie la valeur mise en forme.

Ouvrez `CalendarPage.xaml` et ajoutez les éléments **** suivants avant `<Grid>` l’élément.

```xml
<Page.Resources>
    <local:GraphDateTimeTimeZoneConverter x:Key="DateTimeTimeZoneValueConverter" />
</Page.Resources>
```

Ensuite, remplacez la `Binding="{Binding Start.DateTime}"` ligne par ce qui suit.

```xml
Binding="{Binding Start, Converter={StaticResource DateTimeTimeZoneValueConverter}}"
```

Remplacez la `Binding="{Binding End.DateTime}"` ligne par ce qui suit.

```xml
Binding="{Binding End, Converter={StaticResource DateTimeTimeZoneValueConverter}}"
```

Exécutez l’application, connectez-vous, puis cliquez sur l’élément de navigation **calendrier** . Vous devriez voir la liste des événements dont les valeurs de **début** et de **fin** sont mises en forme.

![Capture d’écran du tableau des événements](./images/add-msgraph-01.png)
