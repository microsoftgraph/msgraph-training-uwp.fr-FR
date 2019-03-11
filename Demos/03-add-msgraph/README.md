# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="1465a-101">Exécution du projet terminé</span><span class="sxs-lookup"><span data-stu-id="1465a-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1465a-102">Conditions requises</span><span class="sxs-lookup"><span data-stu-id="1465a-102">Prerequisites</span></span>

<span data-ttu-id="1465a-103">Pour exécuter le projet terminé dans ce dossier, vous avez besoin des éléments suivants:</span><span class="sxs-lookup"><span data-stu-id="1465a-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="1465a-104">[Visual Studio](https://visualstudio.microsoft.com/vs/) installé sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="1465a-104">[Visual Studio](https://visualstudio.microsoft.com/vs/) installed on your development machine.</span></span> <span data-ttu-id="1465a-105">Si vous ne disposez pas de Visual Studio, reportez-vous au lien précédent pour obtenir les options de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="1465a-105">If you do not have Visual Studio, visit the previous link for download options.</span></span> <span data-ttu-id="1465a-106">(**Remarque:** ce didacticiel a été écrit avec Visual Studio 2017 version 15,81.</span><span class="sxs-lookup"><span data-stu-id="1465a-106">(**Note:** This tutorial was written with Visual Studio 2017 version 15.81.</span></span> <span data-ttu-id="1465a-107">Les étapes de ce guide peuvent fonctionner avec d'autres versions, mais cela n'a pas été testé.)</span><span class="sxs-lookup"><span data-stu-id="1465a-107">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="1465a-108">Soit un compte Microsoft personnel avec une boîte aux lettres sur Outlook.com, soit un compte professionnel ou scolaire Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1465a-108">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="1465a-109">Si vous n'avez pas de compte Microsoft, vous disposez de deux options pour obtenir un compte gratuit:</span><span class="sxs-lookup"><span data-stu-id="1465a-109">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="1465a-110">Vous pouvez vous [inscrire pour obtenir un nouveau compte Microsoft personnel](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span><span class="sxs-lookup"><span data-stu-id="1465a-110">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="1465a-111">Vous pouvez vous [inscrire au programme pour les développeurs office 365](https://developer.microsoft.com/office/dev-program) pour obtenir un abonnement gratuit à Office 365.</span><span class="sxs-lookup"><span data-stu-id="1465a-111">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-a-native-application-with-the-application-registration-portal"></a><span data-ttu-id="1465a-112">Enregistrer une application native avec le portail d'inscription des applications</span><span class="sxs-lookup"><span data-stu-id="1465a-112">Register a native application with the Application Registration Portal</span></span>

1. <span data-ttu-id="1465a-113">Ouvrez un navigateur et accédez au [portail d'inscription des applications](https://apps.dev.microsoft.com) et connectez-vous à l'aide d'un **compte personnel** (alias: Microsoft Account) ou d'un **compte professionnel ou scolaire**.</span><span class="sxs-lookup"><span data-stu-id="1465a-113">Open a browser and navigate to the [Application Registration Portal](https://apps.dev.microsoft.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="1465a-114">Sélectionnez **Ajouter une application** en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="1465a-114">Select **Add an app** at the top of the page.</span></span>

    > <span data-ttu-id="1465a-115">**Remarque:** Si vous voyez plus d'un bouton **Ajouter une application** sur la page, sélectionnez celui qui correspond à la liste **applications** convergées.</span><span class="sxs-lookup"><span data-stu-id="1465a-115">**Note:** If you see more than one **Add an app** button on the page, select the one that corresponds to the **Converged apps** list.</span></span>

1. <span data-ttu-id="1465a-116">Sur la page **inscrire votre application** , définissez le **nom** de l'application sur le **didacticiel Graph UWP** et sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="1465a-116">On the **Register your application** page, set the **Application Name** to **UWP Graph Tutorial** and select **Create**.</span></span>

    ![Capture d'écran de la création d'une nouvelle application dans le site Web du portail d'inscription des applications](../../../Images/arp-create-app-01.png)

1. <span data-ttu-id="1465a-118">Sur la page **d'inscription du didacticiel Graph UWP** , dans la section **Propriétés** , copiez l'ID de l' **application** , car vous en aurez besoin plus tard.</span><span class="sxs-lookup"><span data-stu-id="1465a-118">On the **UWP Graph Tutorial Registration** page, under the **Properties** section, copy the **Application Id** as you will need it later.</span></span>

    ![Capture d'écran de l'ID de l'application nouvellement créée](../../../Images/arp-create-app-02.png)

1. <span data-ttu-id="1465a-120">Faites déFiler \*\*\*\* vers le bas jusqu'à la section plateformes.</span><span class="sxs-lookup"><span data-stu-id="1465a-120">Scroll down to the **Platforms** section.</span></span>

    1. <span data-ttu-id="1465a-121">Sélectionnez **Ajouter une plateforme**.</span><span class="sxs-lookup"><span data-stu-id="1465a-121">Select **Add Platform**.</span></span>
    1. <span data-ttu-id="1465a-122">Dans la boîte de dialogue **Ajouter une plateforme** , sélectionnez **application native**.</span><span class="sxs-lookup"><span data-stu-id="1465a-122">In the **Add Platform** dialog, select **Native Application**.</span></span>

        ![Capture d'écran création d'une plateforme pour l'application](../../../Images/arp-create-app-03.png)

1. <span data-ttu-id="1465a-124">Faites déFiler la page jusqu'en bas et sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1465a-124">Scroll to the bottom of the page and select **Save**.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="1465a-125">Configurer l'exemple</span><span class="sxs-lookup"><span data-stu-id="1465a-125">Configure the sample</span></span>

1. <span data-ttu-id="1465a-126">Renommez `OAuth.resw.example` le fichier `OAuth.resw`.</span><span class="sxs-lookup"><span data-stu-id="1465a-126">Rename the `OAuth.resw.example` file to `OAuth.resw`.</span></span>
1. <span data-ttu-id="1465a-127">Ouvrez `graph-tutorial.sln` dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1465a-127">Open `graph-tutorial.sln` in Visual Studio.</span></span>
1. <span data-ttu-id="1465a-128">Modifiez le `OAuth.resw` fichier dans Visual Studio. Remplacez `YOUR_APP_ID_HERE` par l' **ID d'application** que vous avez obtenu à partir du portail d'inscription des applications.</span><span class="sxs-lookup"><span data-stu-id="1465a-128">Edit the `OAuth.resw` file in visual studio.Replace `YOUR_APP_ID_HERE` with the **Application Id** you got from the App Registration Portal.</span></span>
1. <span data-ttu-id="1465a-129">Dans l'Explorateur de solutions, cliquez avec le bouton droit sur la solution **Graph-Tutorial** , puis choisissez **restaurer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1465a-129">In Solution Explorer, right-click the **graph-tutorial** solution and choose **Restore NuGet Packages**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="1465a-130">Exécution de l’exemple</span><span class="sxs-lookup"><span data-stu-id="1465a-130">Run the sample</span></span>

<span data-ttu-id="1465a-131">Dans Visual Studio, appuyez sur **F5** ou choisissez **débogage > démarrer**le débogage.</span><span class="sxs-lookup"><span data-stu-id="1465a-131">In Visual Studio, press **F5** or choose **Debug > Start Debugging**.</span></span>