# <a name="how-to-run-the-completed-project"></a>Exécution du projet terminé

## <a name="prerequisites"></a>Conditions préalables

Pour exécuter le projet terminé dans ce dossier, vous avez besoin des éléments suivants:

- [Visual Studio](https://visualstudio.microsoft.com/vs/) installé sur votre ordinateur de développement. Si vous ne disposez pas de Visual Studio, reportez-vous au lien précédent pour obtenir les options de téléchargement. (**Remarque:** ce didacticiel a été écrit avec Visual Studio 2017 version 15,81. Les étapes de ce guide peuvent fonctionner avec d’autres versions, mais cela n’a pas été testé.)
- Soit un compte Microsoft personnel avec une boîte aux lettres sur Outlook.com, soit un compte professionnel ou scolaire Microsoft.

Si vous n’avez pas de compte Microsoft, vous disposez de deux options pour obtenir un compte gratuit:

- Vous pouvez vous [inscrire pour obtenir un nouveau compte Microsoft personnel](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).
- Vous pouvez vous [inscrire au programme pour les développeurs office 365](https://developer.microsoft.com/office/dev-program) pour obtenir un abonnement gratuit à Office 365.

## <a name="register-a-native-application-with-the-azure-active-directory-admin-center"></a>Enregistrer une application native avec le centre d’administration Azure Active Directory

1. Ouvrez un navigateur, accédez au [Centre d’administration Azure Active Directory ](https://aad.portal.azure.com) et connectez-vous à l’aide d’un **compte personnel** (ou compte Microsoft) ou d’un **compte professionnel ou scolaire**.

1. Sélectionnez **Azure Active Directory** dans le volet de navigation de gauche, puis sélectionnez **inscriptions des applications** sous **gérer**.

    ![Capture d’écran des inscriptions d’application ](/tutorial/images/aad-portal-app-registrations.png)

1. Sélectionnez **Nouvelle inscription**. Sur la page **Inscrire une application**, définissez les valeurs comme suit.

    - Définissez le **Nom** sur `UWP Graph Tutorial`.
    - Définissez les **Types de comptes pris en charge** sur **Comptes dans un annuaire organisationnel et comptes personnels Microsoft**.
    - Sous **URI**de redirection, remplacez la liste déroulante par **client Public (mobile & Desktop)** et définissez `urn:ietf:wg:oauth:2.0:oob`la valeur sur.

    ![Capture d’écran de la page inscrire une application](/tutorial/images/aad-register-app.png)

1. Choisissez **Inscrire**. Sur la page **didacticiel Graph UWP** , copiez la valeur de l' **ID d’application (client)** et enregistrez-la, vous en aurez besoin à l’étape suivante.

    ![Capture d’écran de l’ID d’application de la nouvelle inscription de l’application](/tutorial/images/aad-application-id.png)

## <a name="configure-the-sample"></a>Configurer l’exemple

1. Renommez `OAuth.resw.example` le fichier `OAuth.resw`.
1. Ouvrez `graph-tutorial.sln` dans Visual Studio.
1. Modifiez le `OAuth.resw` fichier dans Visual Studio. Remplacez `YOUR_APP_ID_HERE` par l' **ID d’application** que vous avez obtenu à partir du portail d’inscription des applications.
1. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur la solution **Graph-Tutorial** , puis choisissez **restaurer les packages NuGet**.

## <a name="run-the-sample"></a>Exécution de l’exemple

Dans Visual Studio, appuyez sur **F5** ou choisissez **débogage > démarrer**le débogage.
