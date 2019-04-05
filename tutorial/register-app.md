<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="2571c-101">Dans cet exercice, vous allez créer une application native Azure AD à l'aide du centre d'administration Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2571c-101">In this exercise you will create a new Azure AD native application using the Azure Active Directory admin center.</span></span>

1. <span data-ttu-id="2571c-102">Ouvrez un navigateur et accédez au [Centre d'administration Azure Active Directory](https://aad.portal.azure.com) et ouvrez une session à l'aide d'un compte **personnel** (alias Microsoft) ou d'un **compte professionnel ou scolaire**.</span><span class="sxs-lookup"><span data-stu-id="2571c-102">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com) and login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="2571c-103">Sélectionnez **Azure Active Directory** dans le volet de navigation de gauche, puis sélectionnez **inscriptions des applications (aperçu)** sous **gérer**.</span><span class="sxs-lookup"><span data-stu-id="2571c-103">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations (Preview)** under **Manage**.</span></span>

    ![<span data-ttu-id="2571c-104">Capture d'écran des inscriptions d'application</span><span class="sxs-lookup"><span data-stu-id="2571c-104">A screenshot of the App registrations</span></span> ](./images/aad-portal-app-registrations.png)

1. <span data-ttu-id="2571c-105">Sélectionnez **nouvelle inscription**.</span><span class="sxs-lookup"><span data-stu-id="2571c-105">Select **New registration**.</span></span> <span data-ttu-id="2571c-106">Sur la page **inscrire une application** , définissez les valeurs comme suit.</span><span class="sxs-lookup"><span data-stu-id="2571c-106">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="2571c-107">Définissez **nom** sur `UWP Graph Tutorial`.</span><span class="sxs-lookup"><span data-stu-id="2571c-107">Set **Name** to `UWP Graph Tutorial`.</span></span>
    - <span data-ttu-id="2571c-108">Définissez les types de comptes **pris en charge** sur **les comptes de tous les comptes d'annuaire et de Microsoft personnels**.</span><span class="sxs-lookup"><span data-stu-id="2571c-108">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="2571c-109">Laissez l' **URI** de redirection vide.</span><span class="sxs-lookup"><span data-stu-id="2571c-109">Leave **Redirect URI** empty.</span></span>

    ![Capture d'écran de la page inscrire une application](./images/aad-register-an-app.png)

1. <span data-ttu-id="2571c-111">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2571c-111">Choose **Register**.</span></span> <span data-ttu-id="2571c-112">Sur la page **didacticiel Graph UWP** , copiez la valeur de l' **ID d'application (client)** et enregistrez-la, vous en aurez besoin à l'étape suivante.</span><span class="sxs-lookup"><span data-stu-id="2571c-112">On the **UWP Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Capture d'écran de l'ID d'application de la nouvelle inscription de l'application](./images/aad-application-id.png)

1. <span data-ttu-id="2571c-114">Sélectionnez le lien **Ajouter un URI de redirection** .</span><span class="sxs-lookup"><span data-stu-id="2571c-114">Select the **Add a Redirect URI** link.</span></span> <span data-ttu-id="2571c-115">Sur la page **URI** de redirection, recherchez la section **URI de redirection suggérée pour les clients publics (mobile, bureau)** .</span><span class="sxs-lookup"><span data-stu-id="2571c-115">On the **Redirect URIs** page, locate the **Suggested Redirect URIs for public clients (mobile, desktop)** section.</span></span> <span data-ttu-id="2571c-116">Sélectionnez l' `urn:ietf:wg:oauth:2.0:oob` URI, puis **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2571c-116">Select the `urn:ietf:wg:oauth:2.0:oob` URI, then choose **Save**.</span></span>

    ![Capture d'écran de la page des URI de redirection](./images/aad-redirect-uris.png)