<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="22cf8-101">Dans cette section, vous allez ajouter la possibilité de créer des événements dans le calendrier de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="22cf8-101">In this section you will add the ability to create events on the user's calendar.</span></span>

1. <span data-ttu-id="22cf8-102">Ajoutez une nouvelle page pour la nouvelle vue de l’événement.</span><span class="sxs-lookup"><span data-stu-id="22cf8-102">Add a new page for the new event view.</span></span> <span data-ttu-id="22cf8-103">Cliquez avec le bouton droit sur le projet **GraphTutorial** dans l’Explorateur de solutions et sélectionnez **Ajouter > nouvel élément...**. Choisissez **page vierge**, entrez `NewEventPage.xaml` dans le champ **nom** , puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="22cf8-103">Right-click the **GraphTutorial** project in Solution Explorer and select **Add > New Item...**. Choose **Blank Page**, enter `NewEventPage.xaml` in the **Name** field, and select **Add**.</span></span>

1. <span data-ttu-id="22cf8-104">Ouvrez **NewEventPage. Xaml** et remplacez son contenu par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="22cf8-104">Open **NewEventPage.xaml** and replace its contents with the following.</span></span>

    :::code language="xaml" source="../demo/GraphTutorial/NewEventPage.xaml" id="NewEventPageXamlSnippet":::

1. <span data-ttu-id="22cf8-105">Ouvrez **NewEventPage.Xaml.cs** et ajoutez les `using` instructions suivantes en haut du fichier.</span><span class="sxs-lookup"><span data-stu-id="22cf8-105">Open **NewEventPage.xaml.cs** and add the following `using` statements to the top of the file.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/NewEventPage.xaml.cs" id="UsingStatementsSnippet":::

1. <span data-ttu-id="22cf8-106">Ajoutez l’interface **INotifyPropertyChange** à la classe **NewEventPage** .</span><span class="sxs-lookup"><span data-stu-id="22cf8-106">Add the **INotifyPropertyChange** interface to the **NewEventPage** class.</span></span> <span data-ttu-id="22cf8-107">Remplacez la déclaration de classe existante par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="22cf8-107">Replace the existing class declaration with the following.</span></span>

    ```csharp
    public sealed partial class NewEventPage : Page, INotifyPropertyChanged
    {
        public NewEventPage()
        {
            this.InitializeComponent();
            DataContext = this;
        }
    }
    ```

1. <span data-ttu-id="22cf8-108">Ajoutez les propriétés suivantes à la classe **NewEventPage** .</span><span class="sxs-lookup"><span data-stu-id="22cf8-108">Add the following properties to the **NewEventPage** class.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/NewEventPage.xaml.cs" id="PropertiesSnippet":::

1. <span data-ttu-id="22cf8-109">Ajoutez le code suivant pour obtenir le fuseau horaire de l’utilisateur à partir de Microsoft Graph lors du chargement de la page.</span><span class="sxs-lookup"><span data-stu-id="22cf8-109">Add the following code to get the user's time zone from Microsoft Graph when the page loads.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/NewEventPage.xaml.cs" id="LoadTimeZoneSnippet":::

1. <span data-ttu-id="22cf8-110">Ajoutez le code suivant pour créer l’événement.</span><span class="sxs-lookup"><span data-stu-id="22cf8-110">Add the following code to create the event.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/NewEventPage.xaml.cs" id="CreateEventSnippet":::

1. <span data-ttu-id="22cf8-111">Modifiez la `NavView_ItemInvoked` méthode dans le fichier **MainPage.Xaml.cs** pour remplacer l' `switch` instruction existante par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="22cf8-111">Modify the `NavView_ItemInvoked` method in the **MainPage.xaml.cs** file to replace the existing `switch` statement with the following.</span></span>

    ```csharp
    switch (invokedItem.ToLower())
    {
        case "new event":
            RootFrame.Navigate(typeof(NewEventPage));
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

1. <span data-ttu-id="22cf8-112">Enregistrez vos modifications et exécutez l’application.</span><span class="sxs-lookup"><span data-stu-id="22cf8-112">Save your changes and run the app.</span></span> <span data-ttu-id="22cf8-113">Connectez-vous, sélectionnez l’élément de menu **nouvel événement** , remplissez le formulaire, puis sélectionnez **créer** pour ajouter un événement au calendrier de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="22cf8-113">Sign in, select the **New event** menu item, fill in the form, and select **Create** to add an event to the user's calendar.</span></span>

    ![Capture d’écran de la nouvelle page d’événement](images/create-event-01.png)
