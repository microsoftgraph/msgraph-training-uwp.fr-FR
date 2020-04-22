<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="431c3-101">Dans cet exercice, vous allez incorporer Microsoft Graph dans l’application.</span><span class="sxs-lookup"><span data-stu-id="431c3-101">In this exercise you will incorporate the Microsoft Graph into the application.</span></span> <span data-ttu-id="431c3-102">Pour cette application, vous allez utiliser la [bibliothèque cliente Microsoft Graph pour .net](https://github.com/microsoftgraph/msgraph-sdk-dotnet) pour effectuer des appels à Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="431c3-102">For this application, you will use the [Microsoft Graph Client Library for .NET](https://github.com/microsoftgraph/msgraph-sdk-dotnet) to make calls to Microsoft Graph.</span></span>

## <a name="get-calendar-events-from-outlook"></a><span data-ttu-id="431c3-103">Récupérer les événements de calendrier à partir d’Outlook</span><span class="sxs-lookup"><span data-stu-id="431c3-103">Get calendar events from Outlook</span></span>

1. <span data-ttu-id="431c3-104">Ajoutez une nouvelle page pour l’affichage Calendrier.</span><span class="sxs-lookup"><span data-stu-id="431c3-104">Add a new page for the calendar view.</span></span> <span data-ttu-id="431c3-105">Cliquez avec le bouton droit sur le projet **GraphTutorial** dans l’Explorateur de solutions et sélectionnez **Ajouter > nouvel élément...**. Choisissez **page vierge**, entrez `CalendarPage.xaml` dans le champ **nom** , puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="431c3-105">Right-click the **GraphTutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Blank Page**, enter `CalendarPage.xaml` in the **Name** field, and select **Add**.</span></span>

1. <span data-ttu-id="431c3-106">Ouvrez `CalendarPage.xaml` et ajoutez la ligne suivante à l’intérieur `<Grid>` de l’élément existant.</span><span class="sxs-lookup"><span data-stu-id="431c3-106">Open `CalendarPage.xaml` and add the following line inside the existing `<Grid>` element.</span></span>

    ```xaml
    <TextBlock x:Name="Events" TextWrapping="Wrap"/>
    ```

1. <span data-ttu-id="431c3-107">Ouvrez `CalendarPage.xaml.cs` et ajoutez les instructions `using` suivantes en haut du fichier.</span><span class="sxs-lookup"><span data-stu-id="431c3-107">Open `CalendarPage.xaml.cs` and add the following `using` statements at the top of the file.</span></span>

    ```csharp
    using Microsoft.Toolkit.Graph.Providers;
    using Microsoft.Toolkit.Uwp.UI.Controls;
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="431c3-108">Ajoutez les fonctions suivantes à la `CalendarPage` classe.</span><span class="sxs-lookup"><span data-stu-id="431c3-108">Add the following functions to the `CalendarPage` class.</span></span>

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

    <span data-ttu-id="431c3-109">Examinez le code dans `OnNavigatedTo` est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="431c3-109">Consider with the code in `OnNavigatedTo` is doing.</span></span>

    - <span data-ttu-id="431c3-110">L’URL qui sera appelée est `/v1.0/me/events`.</span><span class="sxs-lookup"><span data-stu-id="431c3-110">The URL that will be called is `/v1.0/me/events`.</span></span>
    - <span data-ttu-id="431c3-111">La fonction `Select` limite les champs renvoyés pour chaque événement à ceux que la vue utilise réellement.</span><span class="sxs-lookup"><span data-stu-id="431c3-111">The `Select` function limits the fields returned for each events to just those the view will actually use.</span></span>
    - <span data-ttu-id="431c3-112">La fonction `OrderBy` trie les résultats en fonction de la date et de l’heure de création, avec l’élément le plus récent en premier.</span><span class="sxs-lookup"><span data-stu-id="431c3-112">The `OrderBy` function sorts the results by the date and time they were created, with the most recent item being first.</span></span>

1. <span data-ttu-id="431c3-113">Modifiez la `NavView_ItemInvoked` méthode dans le `MainPage.xaml.cs` fichier pour remplacer l’instruction `switch` existante par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="431c3-113">Modify the `NavView_ItemInvoked` method in the `MainPage.xaml.cs` file to replace the existing `switch` statement with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="SwitchStatementSnippet" highlight="4":::

<span data-ttu-id="431c3-114">Vous pouvez maintenant exécuter l’application, vous connecter et cliquer sur l’élément de navigation **calendrier** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="431c3-114">You can now run the app, sign in, and click the **Calendar** navigation item in the left-hand menu.</span></span> <span data-ttu-id="431c3-115">Vous devriez voir un dump JSON des événements sur le calendrier de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="431c3-115">You should see a JSON dump of the events on the user's calendar.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="431c3-116">Afficher les résultats</span><span class="sxs-lookup"><span data-stu-id="431c3-116">Display the results</span></span>

1. <span data-ttu-id="431c3-117">Remplacez tout le contenu de `CalendarPage.xaml` par par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="431c3-117">Replace the entire contents of `CalendarPage.xaml` with the following.</span></span>

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

1. <span data-ttu-id="431c3-118">Ouvrez `CalendarPage.xaml.cs` et remplacez la `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);` ligne par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="431c3-118">Open `CalendarPage.xaml.cs` and replace the `Events.Text = JsonConvert.SerializeObject(events.CurrentPage);` line with the following.</span></span>

    ```csharp
    EventList.ItemsSource = events.CurrentPage.ToList();
    ```

    <span data-ttu-id="431c3-119">Si vous exécutez l’application maintenant et sélectionnez le calendrier, vous devez obtenir la liste des événements dans une grille de données.</span><span class="sxs-lookup"><span data-stu-id="431c3-119">If you run the app now and select the calendar, you should get a list of events in a data grid.</span></span> <span data-ttu-id="431c3-120">Toutefois, les valeurs de **début** et de **fin** sont affichées de manière non conviviale.</span><span class="sxs-lookup"><span data-stu-id="431c3-120">However, the **Start** and **End** values are displayed in a non-user-friendly manner.</span></span> <span data-ttu-id="431c3-121">Vous pouvez contrôler le mode d’affichage de ces valeurs à l’aide d’un [convertisseur de valeur](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter).</span><span class="sxs-lookup"><span data-stu-id="431c3-121">You can control how those values are displayed by using a [value converter](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Data.IValueConverter).</span></span>

1. <span data-ttu-id="431c3-122">Cliquez avec le bouton droit sur le projet **GraphTutorial** dans l’Explorateur de solutions et sélectionnez **Ajouter une > classe...**. Nommez la `GraphDateTimeTimeZoneConverter.cs` classe et sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="431c3-122">Right-click the **GraphTutorial** project in Solution Explorer and select **Add > Class...**. Name the class `GraphDateTimeTimeZoneConverter.cs` and select **Add**.</span></span> <span data-ttu-id="431c3-123">Remplacez tout le contenu du fichier par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="431c3-123">Replace the entire contents of the file with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/GraphDateTimeTimeZoneConverter.cs" id="ConverterSnippet":::

    <span data-ttu-id="431c3-124">Ce code prend la structure [dateTimeTimeZone](/graph/api/resources/datetimetimezone?view=graph-rest-1.0) renvoyée par Microsoft Graph et l’analyse en un `DateTimeOffset` objet.</span><span class="sxs-lookup"><span data-stu-id="431c3-124">This code takes the [dateTimeTimeZone](/graph/api/resources/datetimetimezone?view=graph-rest-1.0) structure returned by Microsoft Graph and parses it into a `DateTimeOffset` object.</span></span> <span data-ttu-id="431c3-125">Il convertit ensuite la valeur dans le fuseau horaire de l’utilisateur et renvoie la valeur mise en forme.</span><span class="sxs-lookup"><span data-stu-id="431c3-125">It then converts the value into the user's time zone and returns the formatted value.</span></span>

1. <span data-ttu-id="431c3-126">Ouvrez `CalendarPage.xaml` et ajoutez les éléments **before** suivants avant `<Grid>` l’élément.</span><span class="sxs-lookup"><span data-stu-id="431c3-126">Open `CalendarPage.xaml` and add the following **before** the `<Grid>` element.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/CalendarPage.xaml" id="ResourcesSnippet":::

1. <span data-ttu-id="431c3-127">Remplacez les deux `DataGridTextColumn` derniers éléments par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="431c3-127">Replace the last two `DataGridTextColumn` elements with the following.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/CalendarPage.xaml" id="BindingSnippet" highlight="4,9":::

1. <span data-ttu-id="431c3-128">Exécutez l’application, connectez-vous, puis cliquez sur l’élément de navigation **calendrier** .</span><span class="sxs-lookup"><span data-stu-id="431c3-128">Run the app, sign in, and click the **Calendar** navigation item.</span></span> <span data-ttu-id="431c3-129">Vous devriez voir la liste des événements dont les valeurs de **début** et de **fin** sont mises en forme.</span><span class="sxs-lookup"><span data-stu-id="431c3-129">You should see the list of events with the **Start** and **End** values formatted.</span></span>

    ![Capture d’écran du tableau des événements](./images/add-msgraph-01.png)
