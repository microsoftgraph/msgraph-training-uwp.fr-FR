<!-- markdownlint-disable MD002 MD041 -->

Dans cet exercice, vous allez incorporer Microsoft Graph dans l’application. Pour cette application, vous allez utiliser la [bibliothèque cliente Microsoft Graph pour .net](https://github.com/microsoftgraph/msgraph-sdk-dotnet) pour effectuer des appels à Microsoft Graph.

## <a name="get-calendar-events-from-outlook"></a>Récupérer les événements de calendrier à partir d’Outlook

1. Ajoutez une nouvelle page pour l’affichage Calendrier. Cliquez avec le bouton droit sur le projet **GraphTutorial** dans l’Explorateur de solutions et sélectionnez **Ajouter > nouvel élément...**. Choisissez **page vierge**, entrez `CalendarPage.xaml` dans le champ **nom** , puis sélectionnez **Ajouter**.

1. Ouvrez `CalendarPage.xaml` et ajoutez la ligne suivante à l’intérieur de l' `<Grid>` élément existant.

    ```xaml
    <TextBlock x:Name="Events" TextWrapping="Wrap"/>
    ```

1. Ouvrez `CalendarPage.xaml.cs` et ajoutez les `using` instructions suivantes en haut du fichier.

    ```csharp
    using Microsoft.Graph;
    using Microsoft.Toolkit.Graph.Providers;
    using Microsoft.Toolkit.Uwp.UI.Controls;
    using Newtonsoft.Json;
    ```

1. Ajoutez les fonctions suivantes à la `CalendarPage` classe.

    ```csharp
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
        // Get the Graph client from the provider
        var graphClient = ProviderManager.Instance.GlobalProvider.Graph;

        try
        {
            // Get the user's mailbox settings to determine
            // their time zone
            var user = await graphClient.Me.Request()
                .Select(u => new { u.MailboxSettings })
                .GetAsync();

            var startOfWeek = GetUtcStartOfWeekInTimeZone(DateTime.Today, user.MailboxSettings.TimeZone);
            var endOfWeek = startOfWeek.AddDays(7);

            var queryOptions = new List<QueryOption>
            {
                new QueryOption("startDateTime", startOfWeek.ToString("o")),
                new QueryOption("endDateTime", endOfWeek.ToString("o"))
            };

            // Get the events
            var events = await graphClient.Me.CalendarView.Request(queryOptions)
                .Header("Prefer", $"outlook.timezone=\"{user.MailboxSettings.TimeZone}\"")
                .Select(ev => new
                {
                    ev.Subject,
                    ev.Organizer,
                    ev.Start,
                    ev.End
                })
                .OrderBy("start/dateTime")
                .Top(50)
                .GetAsync();

            // TEMPORARY: Show the results as JSON
            Events.Text = JsonConvert.SerializeObject(events.CurrentPage);
        }
        catch (ServiceException ex)
        {
            ShowNotification($"Exception getting events: {ex.Message}");
        }

        base.OnNavigatedTo(e);
    }

    private static DateTime GetUtcStartOfWeekInTimeZone(DateTime today, string timeZoneId)
    {
        TimeZoneInfo userTimeZone = TimeZoneInfo.FindSystemTimeZoneById(timeZoneId);

        // Assumes Sunday as first day of week
        int diff = System.DayOfWeek.Sunday - today.DayOfWeek;

        // create date as unspecified kind
        var unspecifiedStart = DateTime.SpecifyKind(today.AddDays(diff), DateTimeKind.Unspecified);

        // convert to UTC
        return TimeZoneInfo.ConvertTimeToUtc(unspecifiedStart, userTimeZone);
    }
    ```

    Examinez le code dans est en cours d' `OnNavigatedTo` exécution.

    - L’URL qui sera appelée est `/me/calendarview`.
        - Les `startDateTime` `endDateTime` paramètres et définissent le début et la fin de l’affichage Calendrier.
        - L' `Prefer: outlook.timezone` en-tête entraîne le `start` `end` renvoi des événements et dans le fuseau horaire de l’utilisateur.
        - La `Select` fonction limite les champs renvoyés pour chaque événement à ceux que l’application utilisera réellement.
        - La `OrderBy` fonction trie les résultats en fonction de la date et de l’heure de début.
        - La `Top` fonction demande au plus 50 événements.

1. Modifiez la `NavView_ItemInvoked` méthode dans le `MainPage.xaml.cs` fichier pour remplacer l' `switch` instruction existante par ce qui suit.

    ```csharp
    switch (invokedItem.ToLower())
    {
        case "new event":
            throw new NotImplementedException();
            break;
        case "calendar":
            RootFrame.Navigate(typeof(CalendarPage));
            break;
        case "home":
        default:
            RootFrame.Navigate(typeof(HomePage));
            break;
    }
    ```

Vous pouvez maintenant exécuter l’application, vous connecter et cliquer sur l’élément de navigation **calendrier** dans le menu de gauche. Vous devriez voir un dump JSON des événements sur le calendrier de l’utilisateur.

## <a name="display-the-results"></a>Afficher les résultats

1. Remplacez tout le contenu de `CalendarPage.xaml` par par ce qui suit.

    ```xaml
    <Page
        x:Class="GraphTutorial.CalendarPage"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:GraphTutorial"
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

1. Ouvrez `CalendarPage.xaml.cs` et remplacez la `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);` ligne par ce qui suit.

    ```csharp
    EventList.ItemsSource = events.CurrentPage.ToList();
    ```

    Si vous exécutez l’application maintenant et sélectionnez le calendrier, vous devez obtenir la liste des événements dans une grille de données. Toutefois, les valeurs de **début** et de **fin** sont affichées de manière non conviviale. Vous pouvez contrôler le mode d’affichage de ces valeurs à l’aide d’un [convertisseur de valeur](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter).

1. Cliquez avec le bouton droit sur le projet **GraphTutorial** dans l’Explorateur de solutions et sélectionnez **Ajouter une > classe...**. Nommez la classe `GraphDateTimeTimeZoneConverter.cs` et sélectionnez **Ajouter**. Remplacez tout le contenu du fichier par ce qui suit.

    :::code language="csharp" source="../demo/GraphTutorial/GraphDateTimeTimeZoneConverter.cs" id="ConverterSnippet":::

    Ce code prend la structure [dateTimeTimeZone](/graph/api/resources/datetimetimezone?view=graph-rest-1.0) renvoyée par Microsoft Graph et l’analyse en un `DateTimeOffset` objet. Il convertit ensuite la valeur dans le fuseau horaire de l’utilisateur et renvoie la valeur mise en forme.

1. Ouvrez `CalendarPage.xaml` et ajoutez les éléments suivants **avant** l' `<Grid>` élément.

    :::code language="xaml" source="../demo/GraphTutorial/CalendarPage.xaml" id="ResourcesSnippet":::

1. Remplacez les deux derniers `DataGridTextColumn` éléments par ce qui suit.

    :::code language="xaml" source="../demo/GraphTutorial/CalendarPage.xaml" id="BindingSnippet" highlight="4,9":::

1. Exécutez l’application, connectez-vous, puis cliquez sur l’élément de navigation **calendrier** . Vous devriez voir la liste des événements dont les valeurs de **début** et de **fin** sont mises en forme.

    ![Capture d’écran du tableau des événements](./images/add-msgraph-01.png)
