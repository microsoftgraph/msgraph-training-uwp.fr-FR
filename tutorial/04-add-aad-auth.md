<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="eea7d-101">Dans cet exercice, vous allez étendre l’application de l’exercice précédent pour prendre en charge l’authentification avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eea7d-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="eea7d-102">Cela est nécessaire pour obtenir le jeton d’accès OAuth nécessaire pour appeler Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="eea7d-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph.</span></span> <span data-ttu-id="eea7d-103">Dans cette étape, vous allez intégrer le contrôle **LoginButton** des [contrôles Windows Graph](https://github.com/windows-toolkit/Graph-Controls) dans l’application.</span><span class="sxs-lookup"><span data-stu-id="eea7d-103">In this step you will integrate the **LoginButton** control from the [Windows Graph Controls](https://github.com/windows-toolkit/Graph-Controls) into the application.</span></span>

1. <span data-ttu-id="eea7d-104">Cliquez avec le bouton droit sur le projet **GraphTutorial** dans l’Explorateur de solutions et sélectionnez **Ajouter > nouvel élément...**. Sélectionnez le **fichier de ressources (. resw)**, nommez le fichier `OAuth.resw` , puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="eea7d-104">Right-click the **GraphTutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Resources File (.resw)**, name the file `OAuth.resw` and select **Add**.</span></span> <span data-ttu-id="eea7d-105">Lorsque le nouveau fichier s’ouvre dans Visual Studio, créez deux ressources comme suit.</span><span class="sxs-lookup"><span data-stu-id="eea7d-105">When the new file opens in Visual Studio, create two resources as follows.</span></span>

    - <span data-ttu-id="eea7d-106">**Name :** `AppId`, **value :** l’ID d’application que vous avez généré dans le portail d’inscription d’application</span><span class="sxs-lookup"><span data-stu-id="eea7d-106">**Name:** `AppId`, **Value:** the app ID you generated in Application Registration Portal</span></span>
    - <span data-ttu-id="eea7d-107">**Nom :** `Scopes`, **valeur :**`User.Read Calendars.Read`</span><span class="sxs-lookup"><span data-stu-id="eea7d-107">**Name:** `Scopes`, **Value:** `User.Read Calendars.Read`</span></span>

    ![Capture d’écran du fichier OAuth. resw dans l’éditeur Visual Studio](./images/edit-resources-01.png)

    > [!IMPORTANT]
    > <span data-ttu-id="eea7d-109">Si vous utilisez le contrôle de code source tel que git, il est maintenant recommandé d’exclure le `OAuth.resw` fichier du contrôle de code source afin d’éviter une fuite accidentelle de votre ID d’application.</span><span class="sxs-lookup"><span data-stu-id="eea7d-109">If you're using source control such as git, now would be a good time to exclude the `OAuth.resw` file from source control to avoid inadvertently leaking your app ID.</span></span>

## <a name="configure-the-loginbutton-control"></a><span data-ttu-id="eea7d-110">Configurer le contrôle LoginButton</span><span class="sxs-lookup"><span data-stu-id="eea7d-110">Configure the LoginButton control</span></span>

1. <span data-ttu-id="eea7d-111">Ouvrez `MainPage.xaml.cs` et ajoutez l’instruction `using` suivante en haut du fichier.</span><span class="sxs-lookup"><span data-stu-id="eea7d-111">Open `MainPage.xaml.cs` and add the following `using` statement to the top of the file.</span></span>

    ```csharp
    using Microsoft.Toolkit.Graph.Providers;
    ```

1. <span data-ttu-id="eea7d-112">Remplacez le constructeur existant par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="eea7d-112">Replace the existing constructor with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="ConstructorSnippet":::

    <span data-ttu-id="eea7d-113">Ce code charge les paramètres à `OAuth.resw` partir de et initialise le fournisseur MSAL avec ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="eea7d-113">This code loads the settings from `OAuth.resw` and initializes the MSAL provider with those values.</span></span>

1. <span data-ttu-id="eea7d-114">À présent, ajoutez un gestionnaire d' `ProviderUpdated` événements pour l' `ProviderManager`événement sur le.</span><span class="sxs-lookup"><span data-stu-id="eea7d-114">Now add an event handler for the `ProviderUpdated` event on the `ProviderManager`.</span></span> <span data-ttu-id="eea7d-115">Ajoutez la fonction suivante à la classe `MainPage`.</span><span class="sxs-lookup"><span data-stu-id="eea7d-115">Add the following function to the `MainPage` class.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/MainPage.xaml.cs" id="ProviderUpdatedSnippet":::

    <span data-ttu-id="eea7d-116">Cet événement se déclenche lorsque le fournisseur change ou lorsque l’état du fournisseur change.</span><span class="sxs-lookup"><span data-stu-id="eea7d-116">This event triggers when the provider changes, or when the provider state changes.</span></span>

1. <span data-ttu-id="eea7d-117">Dans l’Explorateur de solutions, développez **homepage. Xaml** et ouvrez `HomePage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="eea7d-117">In Solution Explorer, expand **HomePage.xaml** and open `HomePage.xaml.cs`.</span></span> <span data-ttu-id="eea7d-118">Remplacez le constructeur existant par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="eea7d-118">Replace the existing constructor with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/HomePage.xaml.cs" id="ConstructorSnippet":::

1. <span data-ttu-id="eea7d-119">Redémarrez l’application et cliquez sur le contrôle **de connexion** en haut de l’application.</span><span class="sxs-lookup"><span data-stu-id="eea7d-119">Restart the app and click the **Sign In** control at the top of the app.</span></span> <span data-ttu-id="eea7d-120">Une fois que vous êtes connecté, l’interface utilisateur doit changer pour indiquer que vous avez réussi à vous connecter.</span><span class="sxs-lookup"><span data-stu-id="eea7d-120">Once you've signed in, the UI should change to indicate that you've successfully signed-in.</span></span>

    ![Capture d’écran de l’application après la connexion](./images/add-aad-auth-01.png)

    > [!NOTE]
    > <span data-ttu-id="eea7d-122">Le `ButtonLogin` contrôle implémente la logique de stockage et d’actualisation du jeton d’accès pour vous.</span><span class="sxs-lookup"><span data-stu-id="eea7d-122">The `ButtonLogin` control implements the logic of storing and refreshing the access token for you.</span></span> <span data-ttu-id="eea7d-123">Les jetons sont stockés dans un emplacement de stockage sécurisé et actualisés en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="eea7d-123">The tokens are stored in secure storage and refreshed as needed.</span></span>
