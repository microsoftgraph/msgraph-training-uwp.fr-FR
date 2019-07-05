<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="1bbe3-101">Dans cet exercice, vous allez incorporer Microsoft Graph dans l’application.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="1bbe3-102">Pour cette application, vous allez utiliser la [bibliothèque cliente Microsoft Graph pour .net](https://github.com/microsoftgraph/msgraph-sdk-dotnet) pour effectuer des appels à Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-102">For this application, you will use the [Microsoft Graph Client Library for .NET](https://github.com/microsoftgraph/msgraph-sdk-dotnet) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="1bbe3-103">Obtenir des événements de calendrier à partir d’Outlook</span><span class="sxs-lookup"><span data-stu-id="1bbe3-103">Get calendar events from Outlook</span></span>

<span data-ttu-id="1bbe3-104">Commencez par ajouter une nouvelle page pour l’affichage Calendrier.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-104">Start by adding a new page for the calendar view.</span></span> <span data-ttu-id="1bbe3-105">Cliquez avec le bouton droit sur le projet du **didacticiel Graph** dans l’Explorateur de solutions et sélectionnez **Ajouter > nouvel élément...**. Choisissez **page vierge**, entrez `CalendarPage.xaml` dans le champ **nom** , puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-105">Right-click the **graph-tutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Blank Page**, enter `CalendarPage.xaml` in the **Name** field, and select **Add**.</span></span>

<span data-ttu-id="1bbe3-106">Ouvrez `CalendarPage.xaml` et ajoutez la ligne suivante à l’intérieur `<Grid>` de l’élément existant.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-106">Open `CalendarPage.xaml` and add the following line inside the existing `<Grid>` element.</span></span>

```xml
<TextBlock x:Name="Events" TextWrapping="Wrap"/>
```

<span data-ttu-id="1bbe3-107">Ouvrez `CalendarPage.xaml.cs` et ajoutez les instructions `using` suivantes en haut du fichier.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-107">Open `CalendarPage.xaml.cs` and add the following `using` statements at the top of the file.</span></span>

```cs
using Microsoft.Toolkit.Services.MicrosoftGraph;
using Microsoft.Toolkit.Uwp.UI.Controls;
using Newtonsoft.Json;
```

<span data-ttu-id="1bbe3-108">Ajoutez ensuite les fonctions suivantes à la `CalendarPage` classe.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-108">Then add the following functions to the `CalendarPage` class.</span></span>

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

<span data-ttu-id="1bbe3-109">Examinez le code dans `OnNavigatedTo` est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-109">Consider with the code in `OnNavigatedTo` is doing.</span></span>

- <span data-ttu-id="1bbe3-110">L’URL qui sera appelée est `/v1.0/me/events`.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-110">The URL that will be called is `/v1.0/me/events`.</span></span>
- <span data-ttu-id="1bbe3-111">La `Select` fonction limite les champs renvoyés pour chaque événement à ceux que l’affichage utilise réellement.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-111">The `Select` function limits the fields returned for each events to just those the view will actually use.</span></span>
- <span data-ttu-id="1bbe3-112">La `OrderBy` fonction trie les résultats en fonction de la date et de l’heure de leur création, avec l’élément le plus récent en premier.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-112">The `OrderBy` function sorts the results by the date and time they were created, with the most recent item being first.</span></span>

<span data-ttu-id="1bbe3-113">Juste avant d’exécuter l’application, pour pouvoir accéder à cette page de calendrier, modifiez la `NavView_ItemInvoked` méthode dans le `MainPage.xaml.cs` fichier de manière à remplacer la `throw new NotImplementedException();` ligne comme suit.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-113">Just before running the app, in order to be able to navigate to this calendar page, modify the `NavView_ItemInvoked` method in the `MainPage.xaml.cs` file to replace the `throw new NotImplementedException();` line with as follows.</span></span>

```cs
case "calendar":
    RootFrame.Navigate(typeof(CalendarPage));
    break;
```

<span data-ttu-id="1bbe3-114">Vous pouvez maintenant exécuter l’application, vous connecter et cliquer sur l’élément de navigation **calendrier** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-114">You can now run the app, sign in, and click the **Calendar** navigation item in the left-hand menu.</span></span> <span data-ttu-id="1bbe3-115">Vous devriez voir un dump JSON des événements sur le calendrier de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-115">You should see a JSON dump of the events on the user's calendar.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="1bbe3-116">Afficher les résultats</span><span class="sxs-lookup"><span data-stu-id="1bbe3-116">Display the results</span></span>

<span data-ttu-id="1bbe3-117">À présent, vous pouvez remplacer le vidage JSON par un texte pour afficher les résultats de manière conviviale.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-117">Now you can replace the JSON dump with something to display the results in a user-friendly manner.</span></span> <span data-ttu-id="1bbe3-118">Remplacez tout le contenu de `CalendarPage.xaml` par par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-118">Replace the entire contents of `CalendarPage.xaml` with the following.</span></span>

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

<span data-ttu-id="1bbe3-119">Cela remplace le `TextBlock` par un `DataGrid`.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-119">This replaces the `TextBlock` with a `DataGrid`.</span></span> <span data-ttu-id="1bbe3-120">Maintenant, `CalendarPage.xaml.cs` ouvrez et remplacez `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);` la ligne par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-120">Now open `CalendarPage.xaml.cs` and replace the `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);` line with the following.</span></span>

```cs
EventList.ItemsSource = events.CurrentPage.ToList();
```

<span data-ttu-id="1bbe3-121">Si vous exécutez l’application maintenant et sélectionnez le calendrier, vous devez obtenir la liste des événements dans une grille de données.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-121">If you run the app now and select the calendar, you should get a list of events in a data grid.</span></span> <span data-ttu-id="1bbe3-122">Toutefois, les valeurs de **début** et de **fin** sont affichées de manière non conviviale.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-122">However, the **Start** and **End** values are displayed in a non-user-friendly manner.</span></span> <span data-ttu-id="1bbe3-123">Vous pouvez contrôler le mode d’affichage de ces valeurs à l’aide d’un [convertisseur de valeur](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter).</span><span class="sxs-lookup"><span data-stu-id="1bbe3-123">You can control how those values are displayed by using a [value converter](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter).</span></span>

<span data-ttu-id="1bbe3-124">Cliquez avec le bouton droit sur le projet du **didacticiel Graph** dans l’Explorateur de solutions et sélectionnez **Ajouter une > classe...**. Nommez la `GraphDateTimeTimeZoneConverter.cs` classe et sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-124">Right-click the **graph-tutorial** project in Solution Explorer and select **Add > Class...**. Name the class `GraphDateTimeTimeZoneConverter.cs` and select **Add**.</span></span> <span data-ttu-id="1bbe3-125">Remplacez tout le contenu du fichier par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-125">Replace the entire contents of the file with the following.</span></span>

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

<span data-ttu-id="1bbe3-126">Ce code prend la structure [dateTimeTimeZone](https://docs.microsoft.com/graph/api/resources/datetimetimezone?view=graph-rest-1.0) renvoyée par Microsoft Graph et l’analyse en un `DateTimeOffset` objet.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-126">This code takes the [dateTimeTimeZone](https://docs.microsoft.com/graph/api/resources/datetimetimezone?view=graph-rest-1.0) structure returned by Microsoft Graph and parses it into a `DateTimeOffset` object.</span></span> <span data-ttu-id="1bbe3-127">Il convertit ensuite la valeur dans le fuseau horaire de l’utilisateur et renvoie la valeur mise en forme.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-127">It then converts the value into the user's time zone and returns the formatted value.</span></span>

<span data-ttu-id="1bbe3-128">Ouvrez `CalendarPage.xaml` et ajoutez les éléments \*\*\*\* suivants avant `<Grid>` l’élément.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-128">Open `CalendarPage.xaml` and add the following **before** the `<Grid>` element.</span></span>

```xml
<Page.Resources>
    <local:GraphDateTimeTimeZoneConverter x:Key="DateTimeTimeZoneValueConverter" />
</Page.Resources>
```

<span data-ttu-id="1bbe3-129">Ensuite, remplacez la `Binding="{Binding Start.DateTime}"` ligne par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-129">Then, replace the `Binding="{Binding Start.DateTime}"` line with the following.</span></span>

```xml
Binding="{Binding Start, Converter={StaticResource DateTimeTimeZoneValueConverter}}"
```

<span data-ttu-id="1bbe3-130">Remplacez la `Binding="{Binding End.DateTime}"` ligne par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-130">Replace the `Binding="{Binding End.DateTime}"` line with the following.</span></span>

```xml
Binding="{Binding End, Converter={StaticResource DateTimeTimeZoneValueConverter}}"
```

<span data-ttu-id="1bbe3-131">Exécutez l’application, connectez-vous, puis cliquez sur l’élément de navigation **calendrier** .</span><span class="sxs-lookup"><span data-stu-id="1bbe3-131">Run the app, sign in, and click the **Calendar** navigation item.</span></span> <span data-ttu-id="1bbe3-132">Vous devriez voir la liste des événements dont les valeurs de **début** et de **fin** sont mises en forme.</span><span class="sxs-lookup"><span data-stu-id="1bbe3-132">You should see the list of events with the **Start** and **End** values formatted.</span></span>

![Capture d’écran du tableau des événements](./images/add-msgraph-01.png)
