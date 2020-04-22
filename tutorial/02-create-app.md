<!-- markdownlint-disable MD002 MD041 -->

Dans cette section, vous allez créer une application UWP.

1. Ouvrez Visual Studio et sélectionnez **Créer un projet**. Choisissez l’option **application vierge (Windows universel)** qui utilise C#, puis sélectionnez **suivant**.

    ![Boîte de dialogue créer un nouveau projet dans Visual Studio 2019](./images/vs-create-new-project.png)

1. Dans la boîte de dialogue **configurer votre nouveau projet** , entrez `GraphTutorial` dans le champ **nom du projet** et sélectionnez **créer**.

    ![Boîte de dialogue Configurer un nouveau projet de Visual Studio 2019](./images/vs-configure-new-project.png)

    > [!IMPORTANT]
    > Assurez-vous d’entrer exactement le même nom pour le projet Visual Studio spécifié dans ces instructions d’atelier. Le nom du projet Visual Studio fait alors partie de l’espace de noms dans le code. Le code figurant dans ces instructions dépend de l’espace de noms qui correspond au nom de projet Visual Studio spécifié dans celles-ci. Si vous utilisez un autre nom de projet, celui-ci n’est pas compilé sauf si vous ajustez tous les espaces de noms pour qu’ils correspondent au nom de projet Visual Studio saisi à la création du projet.

1. Sélectionnez **OK**. Dans la boîte de dialogue **nouveau projet de plateforme Windows universelle** , vérifiez que la **version minimale** est définie sur `Windows 10, Version 1809 (10.0; Build 17763)` ou version ultérieure, puis sélectionnez **OK**.

## <a name="install-nuget-packages"></a>Installation de packages NuGet

Avant de poursuivre, installez des packages NuGet supplémentaires que vous utiliserez plus tard.

- [Microsoft. Toolkit. UWP. UI. Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls/) pour ajouter des contrôles d’interface utilisateur pour les notifications et les indicateurs de chargement dans l’application.
- [Microsoft. Toolkit. UWP. UI. Controls. DataGrid](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid/) pour afficher les informations renvoyées par Microsoft Graph.
- [Microsoft. Toolkit. Graph. Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Graph.Controls) pour gérer la récupération de la connexion et du jeton d’accès.

1. Sélectionnez **Outils > Gestionnaire de package NuGet > Console Gestionnaire de package**. Dans le menu Console du Gestionnaire de package, saisissez les commandes suivantes.

    ```powershell
    Install-Package Microsoft.Toolkit.Uwp.Ui.Controls -Version 6.0.0
    Install-Package Microsoft.Toolkit.Uwp.Ui.Controls.DataGrid -Version 6.0.0
    Install-Package Microsoft.Toolkit.Graph.Controls -IncludePrerelease
    ```

## <a name="design-the-app"></a>Concevoir l’application

Dans cette section, vous allez créer l’interface utilisateur de l’application.

1. Commencez par ajouter une variable au niveau de l’application pour effectuer le suivi de l’état d’authentification. Dans l’Explorateur de solutions, développez **app. Xaml** et ouvrez **app.Xaml.cs**. Ajoutez la propriété ci-dessous à la classe `App`.

    ```csharp
    public bool IsAuthenticated { get; set; }
    ```

1. Définir la disposition de la page principale. Ouvrez `MainPage.xaml` et remplacez l’intégralité de son contenu par ce qui suit.

    :::code language="xaml" source="../demo/GraphTutorial/MainPage.xaml" id="MainPageXamlSnippet":::

    Cela définit un [NavigationView](/uwp/api/windows.ui.xaml.controls.navigationview) de base avec des liens de navigation **Accueil** et **calendrier** pour agir en tant que vue principale de l’application. Il ajoute également un contrôle [LoginButton](https://github.com/windows-toolkit/Graph-Controls) dans l’en-tête de la vue. Ce contrôle permettra à l’utilisateur de se connecter et de se déconnecter. Le contrôle n’est pas encore entièrement activé, vous le configurerez dans un exercice ultérieur.

1. Cliquez avec le bouton droit sur le projet du **didacticiel Graph** dans l’Explorateur de solutions et sélectionnez **Ajouter > nouvel élément...**. Choisissez **page vierge**, entrez `HomePage.xaml` dans le champ **nom** , puis sélectionnez **Ajouter**. Remplacez l’élément `<Grid>` existant dans le fichier par ce qui suit.

    :::code language="xaml" source="../demo/GraphTutorial/HomePage.xaml" id="HomePageGridSnippet" highlight="2-5":::

1. Développez **MainPage. Xaml** dans l’Explorateur de `MainPage.xaml.cs`solutions, puis ouvrez. Ajoutez la fonction suivante à la `MainPage` classe pour gérer l’état de l’authentification.

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="SetAuthStateSnippet":::

1. Ajoutez le code suivant au `MainPage()` constructeur **après** la `this.InitializeComponent();` ligne.

    ```csharp
    // Initialize auth state to false
    SetAuthState(false);

    // Configure MSAL provider
    // TEMPORARY
    MsalProvider.ClientId = "11111111-1111-1111-1111-111111111111";

    // Navigate to HomePage.xaml
    RootFrame.Navigate(typeof(HomePage));
    ```

    Lorsque l’application démarre pour la première fois, elle Initialise l’état d' `false` authentification et accède à la page d’accueil.

1. Ajoutez le gestionnaire d’événements suivant pour charger la page demandée lorsque l’utilisateur sélectionne un élément dans l’affichage de navigation.

    ```csharp
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

1. Enregistrez toutes vos modifications, appuyez sur **F5** ou sélectionnez **débogage > démarrer le débogage** dans Visual Studio.

    > [!NOTE]
    > Assurez-vous que vous sélectionnez la configuration appropriée pour votre ordinateur (ARM, x64, x86).

    ![Capture d’écran de la page d’accueil](./images/create-app-01.png)
