<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="c85db-101">Dans cette section, vous allez créer une application UWP.</span><span class="sxs-lookup"><span data-stu-id="c85db-101">In this section you'll create a new UWP app.</span></span>

1. <span data-ttu-id="c85db-102">Ouvrez Visual Studio et sélectionnez **Créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="c85db-102">Open Visual Studio, and select **Create a new project**.</span></span> <span data-ttu-id="c85db-103">Choisissez l’option **application vierge (Windows universel)** qui utilise C#, puis sélectionnez **suivant**.</span><span class="sxs-lookup"><span data-stu-id="c85db-103">Choose the **Blank App (Universal Windows)** option that uses C#, then select **Next**.</span></span>

    ![Boîte de dialogue créer un nouveau projet dans Visual Studio 2019](./images/vs-create-new-project.png)

1. <span data-ttu-id="c85db-105">Dans la boîte de dialogue **configurer votre nouveau projet** , entrez `GraphTutorial` dans le champ **nom du projet** et sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="c85db-105">In the **Configure your new project** dialog, enter `GraphTutorial` in the **Project name** field and select **Create**.</span></span>

    ![Boîte de dialogue Configurer un nouveau projet de Visual Studio 2019](./images/vs-configure-new-project.png)

    > [!IMPORTANT]
    > <span data-ttu-id="c85db-107">Assurez-vous d’entrer exactement le même nom pour le projet Visual Studio spécifié dans ces instructions d’atelier.</span><span class="sxs-lookup"><span data-stu-id="c85db-107">Ensure that you enter the exact same name for the Visual Studio Project that is specified in these lab instructions.</span></span> <span data-ttu-id="c85db-108">Le nom du projet Visual Studio fait alors partie de l’espace de noms dans le code.</span><span class="sxs-lookup"><span data-stu-id="c85db-108">The Visual Studio Project name becomes part of the namespace in the code.</span></span> <span data-ttu-id="c85db-109">Le code figurant dans ces instructions dépend de l’espace de noms qui correspond au nom de projet Visual Studio spécifié dans celles-ci.</span><span class="sxs-lookup"><span data-stu-id="c85db-109">The code inside these instructions depends on the namespace matching the Visual Studio Project name specified in these instructions.</span></span> <span data-ttu-id="c85db-110">Si vous utilisez un autre nom de projet, celui-ci n’est pas compilé sauf si vous ajustez tous les espaces de noms pour qu’ils correspondent au nom de projet Visual Studio saisi à la création du projet.</span><span class="sxs-lookup"><span data-stu-id="c85db-110">If you use a different project name the code will not compile unless you adjust all the namespaces to match the Visual Studio Project name you enter when you create the project.</span></span>

1. <span data-ttu-id="c85db-111">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="c85db-111">Select **OK**.</span></span> <span data-ttu-id="c85db-112">Dans la boîte de dialogue **nouveau projet de plateforme Windows universelle** , vérifiez que la **version minimale** est définie sur `Windows 10, Version 1809 (10.0; Build 17763)` ou version ultérieure, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="c85db-112">In the **New Universal Windows Platform Project** dialog, ensure that the **Minimum version** is set to `Windows 10, Version 1809 (10.0; Build 17763)` or later and select **OK**.</span></span>

## <a name="install-nuget-packages"></a><span data-ttu-id="c85db-113">Installation de packages NuGet</span><span class="sxs-lookup"><span data-stu-id="c85db-113">Install NuGet packages</span></span>

<span data-ttu-id="c85db-114">Avant de poursuivre, installez des packages NuGet supplémentaires que vous utiliserez plus tard.</span><span class="sxs-lookup"><span data-stu-id="c85db-114">Before moving on, install some additional NuGet packages that you will use later.</span></span>

- <span data-ttu-id="c85db-115">[Microsoft. Toolkit. UWP. UI. Controls. DataGrid](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/) pour afficher les informations renvoyées par Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="c85db-115">[Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/) to display the information returned by Microsoft Graph.</span></span>
- <span data-ttu-id="c85db-116">[Microsoft. Toolkit. Graph. Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Graph.Controls) pour gérer la récupération de la connexion et du jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="c85db-116">[Microsoft.Toolkit.Graph.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Graph.Controls) to handle login and access token retrieval.</span></span>

1. <span data-ttu-id="c85db-117">Sélectionnez **Outils > Gestionnaire de package NuGet > Console Gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="c85db-117">Select **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="c85db-118">Dans le menu Console du Gestionnaire de package, saisissez les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="c85db-118">In the Package Manager Console, enter the following commands.</span></span>

    ```powershell
    Install-Package Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid -IncludePrerelease
    Install-Package Microsoft.Toolkit.Graph.Controls -IncludePrerelease
    ```

## <a name="design-the-app"></a><span data-ttu-id="c85db-119">Concevoir l’application</span><span class="sxs-lookup"><span data-stu-id="c85db-119">Design the app</span></span>

<span data-ttu-id="c85db-120">Dans cette section, vous allez créer l’interface utilisateur de l’application.</span><span class="sxs-lookup"><span data-stu-id="c85db-120">In this section you'll create the UI for the app.</span></span>

1. <span data-ttu-id="c85db-121">Commencez par ajouter une variable au niveau de l’application pour effectuer le suivi de l’état d’authentification.</span><span class="sxs-lookup"><span data-stu-id="c85db-121">Start by adding an application-level variable to track authentication state.</span></span> <span data-ttu-id="c85db-122">Dans l’Explorateur de solutions, développez **app. Xaml** et ouvrez **app.Xaml.cs**.</span><span class="sxs-lookup"><span data-stu-id="c85db-122">In Solution Explorer, expand **App.xaml** and open **App.xaml.cs**.</span></span> <span data-ttu-id="c85db-123">Ajoutez la propriété ci-dessous à la classe `App`.</span><span class="sxs-lookup"><span data-stu-id="c85db-123">Add the following property to the `App` class.</span></span>

    ```csharp
    public bool IsAuthenticated { get; set; }
    ```

1. <span data-ttu-id="c85db-124">Définir la disposition de la page principale.</span><span class="sxs-lookup"><span data-stu-id="c85db-124">Define the layout for the main page.</span></span> <span data-ttu-id="c85db-125">Ouvrez `MainPage.xaml` et remplacez l’intégralité de son contenu par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="c85db-125">Open `MainPage.xaml` and replace its entire contents with the following.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/MainPage.xaml" id="MainPageXamlSnippet":::

    <span data-ttu-id="c85db-126">Cette définition définit un [NavigationView](/uwp/api/windows.ui.xaml.controls.navigationview) de base avec des liens de navigation d’événement **Accueil**, **calendrier** et **nouveau** pour agir en tant que vue principale de l’application.</span><span class="sxs-lookup"><span data-stu-id="c85db-126">This defines a basic [NavigationView](/uwp/api/windows.ui.xaml.controls.navigationview) with **Home**, **Calendar**, and **New event** navigation links to act as the main view of the app.</span></span> <span data-ttu-id="c85db-127">Il ajoute également un contrôle [LoginButton](https://github.com/windows-toolkit/Graph-Controls) dans l’en-tête de la vue.</span><span class="sxs-lookup"><span data-stu-id="c85db-127">It also adds a [LoginButton](https://github.com/windows-toolkit/Graph-Controls) control in the header of the view.</span></span> <span data-ttu-id="c85db-128">Ce contrôle permettra à l’utilisateur de se connecter et de se déconnecter. Le contrôle n’est pas encore entièrement activé, vous le configurerez dans un exercice ultérieur.</span><span class="sxs-lookup"><span data-stu-id="c85db-128">That control will allow the user to sign in and out. The control isn't fully enabled yet, you will configure it in a later exercise.</span></span>

1. <span data-ttu-id="c85db-129">Cliquez avec le bouton droit sur le projet du **didacticiel Graph** dans l’Explorateur de solutions et sélectionnez **Ajouter > nouvel élément...**. Choisissez **page vierge**, entrez `HomePage.xaml` dans le champ **nom** , puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c85db-129">Right-click the **graph-tutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Blank Page**, enter `HomePage.xaml` in the **Name** field, and select **Add**.</span></span> <span data-ttu-id="c85db-130">Remplacez l' `<Grid>` élément existant dans le fichier par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="c85db-130">Replace the existing `<Grid>` element in the file with the following.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/HomePage.xaml" id="HomePageGridSnippet" highlight="2-5":::

1. <span data-ttu-id="c85db-131">Développez **MainPage. Xaml** dans l’Explorateur de solutions, puis ouvrez `MainPage.xaml.cs` .</span><span class="sxs-lookup"><span data-stu-id="c85db-131">Expand **MainPage.xaml** in Solution Explorer and open `MainPage.xaml.cs`.</span></span> <span data-ttu-id="c85db-132">Ajoutez la fonction suivante à la `MainPage` classe pour gérer l’état de l’authentification.</span><span class="sxs-lookup"><span data-stu-id="c85db-132">Add the following function to the `MainPage` class to manage authentication state.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="SetAuthStateSnippet":::

1. <span data-ttu-id="c85db-133">Ajoutez le code suivant au `MainPage()` constructeur **après** la `this.InitializeComponent();` ligne.</span><span class="sxs-lookup"><span data-stu-id="c85db-133">Add the following code to the `MainPage()` constructor **after** the `this.InitializeComponent();` line.</span></span>

    ```csharp
    // Initialize auth state to false
    SetAuthState(false);

    // Configure MSAL provider
    // TEMPORARY
    MsalProvider.ClientId = "11111111-1111-1111-1111-111111111111";

    // Navigate to HomePage.xaml
    RootFrame.Navigate(typeof(HomePage));
    ```

    <span data-ttu-id="c85db-134">Lorsque l’application démarre pour la première fois, elle Initialise l’état d’authentification `false` et accède à la page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="c85db-134">When the app first starts, it will initialize the authentication state to `false` and navigate to the home page.</span></span>

1. <span data-ttu-id="c85db-135">Ajoutez le gestionnaire d’événements suivant pour charger la page demandée lorsque l’utilisateur sélectionne un élément dans l’affichage de navigation.</span><span class="sxs-lookup"><span data-stu-id="c85db-135">Add the following event handler to load the requested page when the user selects an item from the navigation view.</span></span>

    ```csharp
    private void NavView_ItemInvoked(NavigationView sender, NavigationViewItemInvokedEventArgs args)
    {
        var invokedItem = args.InvokedItem as string;

        switch (invokedItem.ToLower())
        {
            case "new event":
                throw new NotImplementedException();
                break;
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

1. <span data-ttu-id="c85db-136">Enregistrez toutes vos modifications, appuyez sur **F5** ou sélectionnez **débogage > démarrer le débogage** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c85db-136">Save all of your changes, then press **F5** or select **Debug > Start Debugging** in Visual Studio.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c85db-137">Assurez-vous que vous sélectionnez la configuration appropriée pour votre ordinateur (ARM, x64, x86).</span><span class="sxs-lookup"><span data-stu-id="c85db-137">Make sure you select the appropriate configuration for your machine (ARM, x64, x86).</span></span>

    ![Capture d’écran de la page d’accueil](./images/create-app-01.png)
