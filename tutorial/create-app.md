<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="100b7-101">Ouvrez Visual Studio, puis sélectionnez **fichier _GT_ nouveau projet >**.</span><span class="sxs-lookup"><span data-stu-id="100b7-101">Open Visual Studio, and select **File > New > Project**.</span></span> <span data-ttu-id="100b7-102">Dans la boîte de dialogue **nouveau projet** , procédez comme suit:</span><span class="sxs-lookup"><span data-stu-id="100b7-102">In the **New Project** dialog, do the following:</span></span>

1. <span data-ttu-id="100b7-103">Sélectionnez **modèles _GT_ Visual C# _GT_ Windows Universal**.</span><span class="sxs-lookup"><span data-stu-id="100b7-103">Select **Templates > Visual C# > Windows Universal**.</span></span>
1. <span data-ttu-id="100b7-104">Sélectionnez **application vierge (Windows universel)**.</span><span class="sxs-lookup"><span data-stu-id="100b7-104">Select **Blank App (Universal Windows)**.</span></span>
1. <span data-ttu-id="100b7-105">Entrez **un didacticiel** pour le nom du projet.</span><span class="sxs-lookup"><span data-stu-id="100b7-105">Enter **graph-tutorial** for the Name of the project.</span></span>

![Boîte de dialogue créer un nouveau projet dans Visual Studio 2017](./images/vs-newproj-01.png)

> [!IMPORTANT]
> <span data-ttu-id="100b7-107">Assurez-vous d'entrer exactement le même nom pour le projet Visual Studio spécifié dans ces instructions d'atelier.</span><span class="sxs-lookup"><span data-stu-id="100b7-107">Ensure that you enter the exact same name for the Visual Studio Project that is specified in these lab instructions.</span></span> <span data-ttu-id="100b7-108">Le nom du projet Visual Studio devient partie intégrante de l'espace de noms dans le code.</span><span class="sxs-lookup"><span data-stu-id="100b7-108">The Visual Studio Project name becomes part of the namespace in the code.</span></span> <span data-ttu-id="100b7-109">Le code à l'intérieur de ces instructions dépend de l'espace de noms correspondant au nom de projet Visual Studio spécifié dans ces instructions.</span><span class="sxs-lookup"><span data-stu-id="100b7-109">The code inside these instructions depends on the namespace matching the Visual Studio Project name specified in these instructions.</span></span> <span data-ttu-id="100b7-110">Si vous utilisez un nom de projet différent, le code n'est pas compilé, sauf si vous ajustez tous les espaces de noms pour qu'ils correspondent au nom de projet Visual Studio que vous entrez lors de la création du projet.</span><span class="sxs-lookup"><span data-stu-id="100b7-110">If you use a different project name the code will not compile unless you adjust all the namespaces to match the Visual Studio Project name you enter when you create the project.</span></span>

<span data-ttu-id="100b7-111">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="100b7-111">Select **OK**.</span></span> <span data-ttu-id="100b7-112">Dans la boîte de dialogue **nouveau projet de plateforme Windows universelle** , vérifiez que la **version minimale** est définie sur `Windows 10 Fall Creators Update (10.0; Build 16299)` ou version ultérieure, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="100b7-112">In the **New Universal Windows Platform Project** dialog, ensure that the **Minimum version** is set to `Windows 10 Fall Creators Update (10.0; Build 16299)` or later and select **OK**.</span></span>

<span data-ttu-id="100b7-113">Avant de poursuivre, installez des packages NuGet supplémentaires que vous utiliserez plus tard.</span><span class="sxs-lookup"><span data-stu-id="100b7-113">Before moving on, install some additional NuGet packages that you will use later.</span></span>

- <span data-ttu-id="100b7-114">[Microsoft. Toolkit. UWP. UI. Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls/) pour ajouter des contrôles d'interface utilisateur pour les notifications et les indicateurs de chargement dans l'application.</span><span class="sxs-lookup"><span data-stu-id="100b7-114">[Microsoft.Toolkit.Uwp.Ui.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls/) to add some UI controls for in-app notifications and loading indicators.</span></span>
- <span data-ttu-id="100b7-115">[Microsoft. Toolkit. UWP. UI. Controls. DataGrid](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/) pour afficher les informations renvoyées par Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="100b7-115">[Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/) to display the information returned by Microsoft Graph.</span></span>
- <span data-ttu-id="100b7-116">[Microsoft. Toolkit. UWP. UI. Controls. Graph](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.Graph/) pour gérer l'extraction des jetons d'accès et de connexion.</span><span class="sxs-lookup"><span data-stu-id="100b7-116">[Microsoft.Toolkit.Uwp.Ui.Controls.Graph](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.Graph/) to handle login and access token retrieval.</span></span>
- <span data-ttu-id="100b7-117">[Microsoft. Graph](https://www.nuget.org/packages/Microsoft.Graph/) pour effectuer des appels à Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="100b7-117">[Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/) for making calls to the Microsoft Graph.</span></span>

<span data-ttu-id="100b7-118">Sélectionnez **Outils _GT_ gestionnaire de package NuGet _GT_ console Gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="100b7-118">Select **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="100b7-119">Dans la console Gestionnaire de package, entrez les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="100b7-119">In the Package Manager Console, enter the following commands.</span></span>

```Powershell
Install-Package Microsoft.Toolkit.Uwp.Ui.Controls
Install-Package Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid
Install-Package Microsoft.Toolkit.Uwp.Ui.Controls.Graph
Install-Package Microsoft.Graph
```

## <a name="design-the-app"></a><span data-ttu-id="100b7-120">Concevoir l'application</span><span class="sxs-lookup"><span data-stu-id="100b7-120">Design the app</span></span>

<span data-ttu-id="100b7-121">Commencez par ajouter une variable au niveau de l'application pour effectuer le suivi de l'état d'authentification.</span><span class="sxs-lookup"><span data-stu-id="100b7-121">Start by adding an application-level variable to track authentication state.</span></span> <span data-ttu-id="100b7-122">Dans l'Explorateur de solutions, développez **app. Xaml** et ouvrez **app.Xaml.cs**.</span><span class="sxs-lookup"><span data-stu-id="100b7-122">In Solution Explorer, expand **App.xaml** and open **App.xaml.cs**.</span></span> <span data-ttu-id="100b7-123">Ajoutez la propriété suivante à la `App` classe.</span><span class="sxs-lookup"><span data-stu-id="100b7-123">Add the following property to the `App` class.</span></span>

```cs
public bool IsAuthenticated { get; set; }
```

<span data-ttu-id="100b7-124">Définissez ensuite la disposition de la page principale.</span><span class="sxs-lookup"><span data-stu-id="100b7-124">Next, define the layout for the main page.</span></span> <span data-ttu-id="100b7-125">Ouvrez `MainPage.xaml` et remplacez l'intégralité de son contenu par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="100b7-125">Open `MainPage.xaml` and replace its entire contents with the following.</span></span>

```xml
<Page
    x:Class="graph_tutorial.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:graph_tutorial"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"
    xmlns:graphControls="using:Microsoft.Toolkit.Uwp.UI.Controls.Graph"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <Grid>
        <NavigationView x:Name="NavView"
            IsSettingsVisible="False"
            ItemInvoked="NavView_ItemInvoked">

            <NavigationView.Header>
                <graphControls:AadLogin x:Name="Login"
                    HorizontalAlignment="Left"
                    View="SmallProfilePhotoLeft"
                    AllowSignInAsDifferentUser="False"
                    />
            </NavigationView.Header>

            <NavigationView.MenuItems>
                <NavigationViewItem Content="Home" x:Name="Home" Tag="home">
                    <NavigationViewItem.Icon>
                        <FontIcon Glyph="&#xE10F;"/>
                    </NavigationViewItem.Icon>
                </NavigationViewItem>
                <NavigationViewItem Content="Calendar" x:Name="Calendar" Tag="calendar">
                    <NavigationViewItem.Icon>
                        <FontIcon Glyph="&#xE163;"/>
                    </NavigationViewItem.Icon>
                </NavigationViewItem>
            </NavigationView.MenuItems>

            <StackPanel>
                <controls:InAppNotification x:Name="Notification" ShowDismissButton="true" />
                <Frame x:Name="RootFrame" Margin="24, 0" />
            </StackPanel>
        </NavigationView>
    </Grid>
</Page>
```

<span data-ttu-id="100b7-126">Cela définit un [NavigationView](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.navigationview) de base avec des liens de navigation **Accueil** et **calendrier** pour agir en tant que vue principale de l'application.</span><span class="sxs-lookup"><span data-stu-id="100b7-126">This defines a basic [NavigationView](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.navigationview) with **Home** and **Calendar** navigation links to act as the main view of the app.</span></span> <span data-ttu-id="100b7-127">Il ajoute également un contrôle [AadLogin](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.controls.graph.aadlogin?view=win-comm-toolkit-dotnet-stable) dans l'en-tête de la vue.</span><span class="sxs-lookup"><span data-stu-id="100b7-127">It also adds an [AadLogin](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.controls.graph.aadlogin?view=win-comm-toolkit-dotnet-stable) control in the header of the view.</span></span> <span data-ttu-id="100b7-128">Ce contrôle permettra à l'utilisateur de se connecter et de se déconnecter. Le contrôle n'est pas encore entièrement activé, vous le configurerez dans un exercice ultérieur.</span><span class="sxs-lookup"><span data-stu-id="100b7-128">That control will allow the user to sign in and out. The control isn't fully enabled yet, you will configure it in a later exercise.</span></span>

<span data-ttu-id="100b7-129">Maintenant, ajoutez une autre page XAML pour le mode Accueil.</span><span class="sxs-lookup"><span data-stu-id="100b7-129">Now add another XAML page for the Home view.</span></span> <span data-ttu-id="100b7-130">Cliquez avec le bouton droit sur le projet du **didacticiel Graph** dans l'Explorateur de solutions et choisissez **Ajouter un nouvel élément >...**. Choisissez **page vierge**, entrez `HomePage.xaml` dans le champ **nom** , puis choisissez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="100b7-130">Right-click the **graph-tutorial** project in Solution Explorer and choose **Add > New Item...**. Choose **Blank Page**, enter `HomePage.xaml` in the **Name** field, and choose **Add**.</span></span> <span data-ttu-id="100b7-131">Ajoutez le code suivant à l' `<Grid>` intérieur de l'élément dans le fichier.</span><span class="sxs-lookup"><span data-stu-id="100b7-131">Add the following code inside the `<Grid>` element in the file.</span></span>

```xml
<StackPanel>
    <TextBlock FontSize="44" FontWeight="Bold" Margin="0, 12">Microsoft Graph UWP Tutorial</TextBlock>
    <TextBlock x:Name="HomePageMessage">Please sign in to continue.</TextBlock>
</StackPanel>
```

<span data-ttu-id="100b7-132">Maintenant, développez **MainPage. Xaml** dans l'Explorateur `MainPage.xaml.cs`de solutions et ouvrez.</span><span class="sxs-lookup"><span data-stu-id="100b7-132">Now expand **MainPage.xaml** in Solution Explorer and open `MainPage.xaml.cs`.</span></span> <span data-ttu-id="100b7-133">Ajoutez le code suivant au `MainPage()` constructeur **après** la `this.InitializeComponent();` ligne.</span><span class="sxs-lookup"><span data-stu-id="100b7-133">Add the following code to the `MainPage()` constructor **after** the `this.InitializeComponent();` line.</span></span>

```cs
// Initialize auth state to false
SetAuthState(false);

// Navigate to HomePage.xaml
RootFrame.Navigate(typeof(HomePage));
```

<span data-ttu-id="100b7-134">Lorsque l'application démarre pour la première fois, elle Initialise l'état d' `false` authentification et accède à la page d'accueil.</span><span class="sxs-lookup"><span data-stu-id="100b7-134">When the app first starts, it will initialize the authentication state to `false` and navigate to the home page.</span></span>

<span data-ttu-id="100b7-135">Ajoutez la fonction suivante à la `MainPage` classe pour gérer l'état de l'authentification.</span><span class="sxs-lookup"><span data-stu-id="100b7-135">Add the following function to the `MainPage` class to manage authentication state.</span></span>

```cs
private void SetAuthState(bool isAuthenticated)
{
    (App.Current as App).IsAuthenticated = isAuthenticated;

    // Toggle controls that require auth
    Calendar.IsEnabled = isAuthenticated;
}
```

<span data-ttu-id="100b7-136">Ajoutez le gestionnaire d'événements suivant pour charger la page demandée lorsque l'utilisateur sélectionne un élément dans l'affichage de navigation.</span><span class="sxs-lookup"><span data-stu-id="100b7-136">Add the following event handler to load the requested page when the user selects an item from the navigation view.</span></span>

```cs
private void NavView_ItemInvoked(NavigationView sender, NavigationViewItemInvokedEventArgs args)
{
    var invokedItem = args.InvokedItem as string;

    switch (invokedItem.ToLower())
    {
        case "calendar":
            throw new NotImplementedException();
            break;
        case "home":
        default:
            RootFrame.Navigate(typeof(HomePage));
            break;
    }
}
```

<span data-ttu-id="100b7-137">Enregistrez toutes vos modifications, appuyez sur **F5** ou sélectionnez **débogage > démarrer** le débogage dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="100b7-137">Save all of your changes, then press **F5** or select **Debug > Start Debugging** in Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="100b7-138">Assurez-vous que vous sélectionnez la configuration appropriée pour votre ordinateur (ARM, x64, x86).</span><span class="sxs-lookup"><span data-stu-id="100b7-138">Make sure you select the appropriate configuration for your machine (ARM, x64, x86).</span></span>

![Capture d’écran de la page d’accueil](./images/create-app-01.png)
