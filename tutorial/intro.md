<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="faddb-101">Ce didacticiel vous apprend à créer une application de plateforme Windows universelle (UWP) qui utilise l’API Microsoft Graph pour récupérer des informations de calendrier pour un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="faddb-101">This tutorial teaches you how to build a Universal Windows Platform (UWP) app that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="faddb-102">Si vous préférez télécharger simplement le didacticiel terminé, vous pouvez télécharger ou cloner le [référentiel GitHub](https://github.com/microsoftgraph/msgraph-training-uwp).</span><span class="sxs-lookup"><span data-stu-id="faddb-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-uwp).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="faddb-103">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="faddb-103">Prerequisites</span></span>

<span data-ttu-id="faddb-104">Avant de commencer ce didacticiel, [Visual Studio](https://visualstudio.microsoft.com/vs/) doit être installé sur un ordinateur exécutant Windows 10 avec [le mode développeur activé](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development).</span><span class="sxs-lookup"><span data-stu-id="faddb-104">Before you start this tutorial, you should have [Visual Studio](https://visualstudio.microsoft.com/vs/) installed on a computer running Windows 10 with [Developer mode turned on](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development).</span></span> <span data-ttu-id="faddb-105">Si vous ne disposez pas de Visual Studio, reportez-vous au lien précédent pour obtenir les options de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="faddb-105">If you do not have Visual Studio, visit the previous link for download options.</span></span>

> [!NOTE]
> <span data-ttu-id="faddb-106">Ce didacticiel a été écrit avec Visual Studio 2017 version 15.8.1.</span><span class="sxs-lookup"><span data-stu-id="faddb-106">This tutorial was written with Visual Studio 2017 version 15.8.1.</span></span> <span data-ttu-id="faddb-107">Les étapes de ce guide peuvent fonctionner avec d’autres versions, mais cela n’a pas été testé.</span><span class="sxs-lookup"><span data-stu-id="faddb-107">The steps in this guide may work with other versions, but that has not been tested.</span></span>

## <a name="feedback"></a><span data-ttu-id="faddb-108">Commentaires</span><span class="sxs-lookup"><span data-stu-id="faddb-108">Feedback</span></span>

<span data-ttu-id="faddb-109">Veuillez fournir des commentaires sur ce didacticiel dans le [référentiel GitHub](https://github.com/microsoftgraph/msgraph-training-uwp).</span><span class="sxs-lookup"><span data-stu-id="faddb-109">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-uwp).</span></span>