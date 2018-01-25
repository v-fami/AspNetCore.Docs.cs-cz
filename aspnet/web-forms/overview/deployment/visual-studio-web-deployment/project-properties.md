---
uid: web-forms/overview/deployment/visual-studio-web-deployment/project-properties
title: "Nasazení webu ASP.NET pomocí sady Visual Studio: vlastnosti projektu | Microsoft Docs"
author: tdykstra
description: "Tato řada kurzu se dozvíte, jak nasadit (publikovat) technologie ASP.NET webové aplikace do Azure App Service Web Apps nebo do hostujícího zprostředkovatele třetí strany podle usin..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: ec1cec4c-a75f-47af-a2ba-b1e2f971d24b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/project-properties
msc.type: authoredcontent
ms.openlocfilehash: 68a1892dcf8055d8cc898f471a96d86e8abb64de
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-web-deployment-using-visual-studio-project-properties"></a><span data-ttu-id="76faf-103">Nasazení webu ASP.NET pomocí sady Visual Studio: vlastnosti projektu</span><span class="sxs-lookup"><span data-stu-id="76faf-103">ASP.NET Web Deployment using Visual Studio: Project Properties</span></span>
====================
<span data-ttu-id="76faf-104">podle [tní Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="76faf-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="76faf-105">Stáhněte si úvodní projekt</span><span class="sxs-lookup"><span data-stu-id="76faf-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="76faf-106">Tato řada kurzu se dozvíte, jak nasadit (publikovat) technologie ASP.NET webové aplikace do Azure App Service Web Apps nebo k poskytovateli hostingu třetích stran, pomocí sady Visual Studio 2012 nebo Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="76faf-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="76faf-107">Informace o řadě najdete v tématu [z prvního kurzu řady](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="76faf-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="76faf-108">Přehled</span><span class="sxs-lookup"><span data-stu-id="76faf-108">Overview</span></span>

<span data-ttu-id="76faf-109">Některé možnosti nasazení jsou nakonfigurované ve vlastnostech projektu, které jsou uložené v souboru projektu ( *.csproj* nebo *.vbproj* souboru).</span><span class="sxs-lookup"><span data-stu-id="76faf-109">Some deployment options are configured in project properties that are stored in the project file (the *.csproj* or *.vbproj* file).</span></span> <span data-ttu-id="76faf-110">Ve většině případů výchozí hodnoty těchto nastavení jsou, co chcete použít, ale můžete použít **vlastnosti projektu** uživatelského rozhraní, které jsou součástí sady Visual Studio pro práci s těmito nastaveními, pokud budete muset změnit.</span><span class="sxs-lookup"><span data-stu-id="76faf-110">In most cases, the default values of these settings are what you want, but you can use the **Project Properties** UI built into Visual Studio to work with these settings if you have to change them.</span></span> <span data-ttu-id="76faf-111">V tomto kurzu můžete zkontrolovat nastavení nasazení v **vlastnosti projektu**.</span><span class="sxs-lookup"><span data-stu-id="76faf-111">In this tutorial you review the deployment settings in **Project Properties**.</span></span> <span data-ttu-id="76faf-112">Můžete také vytvořit zástupný soubor, který vede k prázdné složce pro nasazení.</span><span class="sxs-lookup"><span data-stu-id="76faf-112">You also create a placeholder file that causes an empty folder to be deployed.</span></span>

## <a name="configure-deployment-settings-in-the-project-properties-window"></a><span data-ttu-id="76faf-113">Konfigurace nastavení nasazení v okně Vlastnosti projektu</span><span class="sxs-lookup"><span data-stu-id="76faf-113">Configure deployment settings in the project properties window</span></span>

<span data-ttu-id="76faf-114">Většina nastavení, které ovlivňuje, co se stane, že při nasazení jsou součástí profil publikování, jak uvidíte v následujících kurzech.</span><span class="sxs-lookup"><span data-stu-id="76faf-114">Most settings that affect what happens during deployment are included in the publish profile, as you'll see in the following tutorials.</span></span> <span data-ttu-id="76faf-115">Několik nastavení, které byste měli vědět, jsou umístěné v **nasadit** kartách **vlastnosti projektu** okno.</span><span class="sxs-lookup"><span data-stu-id="76faf-115">A few settings that you should be aware of are located in the **Package/Publish** tabs of the **Project Properties** window.</span></span> <span data-ttu-id="76faf-116">Tato nastavení jsou určena pro každou konfiguraci sestavení – to znamená, mohou mít různá nastavení pro sestavení pro vydání, než kolik máte sestavení pro ladění.</span><span class="sxs-lookup"><span data-stu-id="76faf-116">These settings are specified for each build configuration — that is, you can have different settings for a Release build than you have for a Debug build.</span></span>

<span data-ttu-id="76faf-117">V **Průzkumníku řešení**, klikněte pravým tlačítkem myši **ContosoUniversity** projekt, vyberte **vlastnosti**a pak vyberte **balení/publikování webu**kartě.</span><span class="sxs-lookup"><span data-stu-id="76faf-117">In **Solution Explorer**, right-click the **ContosoUniversity** project, select **Properties**, and then select the **Package/Publish Web** tab.</span></span>

![Kartě Balení/publikování webu](project-properties/_static/image1.png)

<span data-ttu-id="76faf-119">Když se zobrazí okno, bude výchozí s nastavením pro kteroukoli konfigurace sestavení je aktuálně aktivní řešení.</span><span class="sxs-lookup"><span data-stu-id="76faf-119">When the window is displayed, it defaults to showing settings for whichever build configuration is currently active for the solution.</span></span> <span data-ttu-id="76faf-120">Pokud **konfigurace** pole neindikuje **aktivní (verze)**, vyberte **verze** aby bylo možné zobrazit nastavení pro konfiguraci sestavení verze.</span><span class="sxs-lookup"><span data-stu-id="76faf-120">If the **Configuration** box does not indicate **Active (Release)**, select **Release** in order to display settings for the Release build configuration.</span></span> <span data-ttu-id="76faf-121">Nasadíte verze sestavení pro testovací a produkční prostředí.</span><span class="sxs-lookup"><span data-stu-id="76faf-121">You'll deploy Release builds to both your test and production environments.</span></span>

![Výběr konfigurace verze sestavení](project-properties/_static/image2.png)

<span data-ttu-id="76faf-123">S **aktivní (verze)** nebo **verze** vybrali, zobrazí hodnoty, které jsou platné, když nasadíte pomocí konfigurace sestavení verze:</span><span class="sxs-lookup"><span data-stu-id="76faf-123">With **Active (Release)** or **Release** selected, you see the values that are effective when you deploy using the Release build configuration:</span></span>

- <span data-ttu-id="76faf-124">V **položky k nasazení** pole **pouze soubory potřebné ke spuštění aplikace** je vybrána.</span><span class="sxs-lookup"><span data-stu-id="76faf-124">In the **Items to deploy** box, **Only files needed to run the application** is selected.</span></span> <span data-ttu-id="76faf-125">Ostatní možnosti patří **všechny soubory v tomto projektu** nebo **všechny soubory v této složce projektu**.</span><span class="sxs-lookup"><span data-stu-id="76faf-125">Other options are **All files in this project** or **All files in this project folder**.</span></span> <span data-ttu-id="76faf-126">Ponechat výchozí výběr beze změny vyhnete soubory zdrojového kódu, například nasazení.</span><span class="sxs-lookup"><span data-stu-id="76faf-126">By leaving the default selection unchanged you avoid deploying source code files, for example.</span></span> <span data-ttu-id="76faf-127">Toto nastavení je důvod, proč složky, které obsahují systém SQL Server Compact binární soubory musí být zahrnutý v projektu.</span><span class="sxs-lookup"><span data-stu-id="76faf-127">This setting is the reason why the folders that contain the SQL Server Compact binary files had to be included in the project.</span></span> <span data-ttu-id="76faf-128">Další informace o tomto nastavení najdete v tématu **proč si všechny soubory ve složce projektu nasadí?** v [ASP.NET webové aplikace projektu nasazení – nejčastější dotazy](https://msdn.microsoft.com/en-us/library/ee942158.aspx).</span><span class="sxs-lookup"><span data-stu-id="76faf-128">For more information about this setting, see **Why don't all of the files in my project folder get deployed?** in [ASP.NET Web Application Project Deployment FAQ](https://msdn.microsoft.com/en-us/library/ee942158.aspx).</span></span>
- <span data-ttu-id="76faf-129">**Vyloučit generované symboly ladění** je vybrána.</span><span class="sxs-lookup"><span data-stu-id="76faf-129">**Exclude generated debug symbols** is selected.</span></span> <span data-ttu-id="76faf-130">Při použití této konfigurace sestavení, nebude možné ladění.</span><span class="sxs-lookup"><span data-stu-id="76faf-130">You won't be debugging when you use this build configuration.</span></span>
- <span data-ttu-id="76faf-131">**Zahrnout všechny databáze nakonfigurované na kartě Balení/publikování kódu SQL** je vybrána.</span><span class="sxs-lookup"><span data-stu-id="76faf-131">**Include all databases configured in Package/Publish SQL tab** is selected.</span></span> <span data-ttu-id="76faf-132">Určuje, zda bude databáze a také soubory nasazení sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="76faf-132">Specifies whether Visual Studio will deploy databases as well as files.</span></span> <span data-ttu-id="76faf-133">I když políčko popisku pouze zmínkami **balení/publikování kódu SQL** kartě, zrušíte zaškrtnutí tohoto políčka by také zakázat nasazení databáze, který je nakonfigurovaný v profilu publikování.</span><span class="sxs-lookup"><span data-stu-id="76faf-133">Although the check box label only mentions the **Package/Publish SQL** tab, clearing this check box would also disable database deployment that is configured in the publish profile.</span></span> <span data-ttu-id="76faf-134">Můžete se to, který později, tak pole musí zůstat vybrané.</span><span class="sxs-lookup"><span data-stu-id="76faf-134">You will be doing that later, so the check box must remain selected.</span></span> <span data-ttu-id="76faf-135">**Balení/publikování kódu SQL** karta slouží k publikování metoda, která nebudete používat v těchto kurzech starší verze databáze.</span><span class="sxs-lookup"><span data-stu-id="76faf-135">The **Package/Publish SQL** tab is used for a legacy database publishing method that you won't be using in these tutorials.</span></span>
- <span data-ttu-id="76faf-136">**Nastavení balíčku pro nasazení webových** oddíl nelze použít, protože používáte jedním kliknutím publikovat v těchto kurzech.</span><span class="sxs-lookup"><span data-stu-id="76faf-136">The **Web Deployment Package Settings** section does not apply because you're using one-click publish in these tutorials.</span></span>

<span data-ttu-id="76faf-137">Změna **konfigurace** rozevíracího seznamu pro ladění zobrazíte výchozí nastavení pro ladění.</span><span class="sxs-lookup"><span data-stu-id="76faf-137">Change the **Configuration** drop-down box to Debug to see the default settings for Debug builds.</span></span> <span data-ttu-id="76faf-138">Hodnoty jsou stejné, s výjimkou **Vynechat generované symboly ladění** je prázdná, takže můžete ladit, když nasazujete sestavení ladicí verze.</span><span class="sxs-lookup"><span data-stu-id="76faf-138">The values are the same, except **Exclude generated debug symbols** is cleared so that you can debug when you deploy a Debug build.</span></span>

## <a name="make-sure-that-the-elmah-folder-gets-deployed"></a><span data-ttu-id="76faf-139">Získá nasazení složce Elmah</span><span class="sxs-lookup"><span data-stu-id="76faf-139">Make sure that the Elmah folder gets deployed</span></span>

<span data-ttu-id="76faf-140">Jak už jste viděli v tomto kurzu předchozí [balíček Elmah NuGet](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) poskytuje funkce pro chybu protokolování a vytváření sestav.</span><span class="sxs-lookup"><span data-stu-id="76faf-140">As you saw in the previous tutorial, the [Elmah NuGet package](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) provides functionality for error logging and reporting.</span></span> <span data-ttu-id="76faf-141">V aplikaci Contoso univerzity Elmah nakonfigurován, aby podrobnosti o chybě uložit do složky s názvem *Elmah*:</span><span class="sxs-lookup"><span data-stu-id="76faf-141">In the Contoso University application Elmah has been configured to store error details in a folder named *Elmah*:</span></span>

![Elmah složky](project-properties/_static/image3.png)

<span data-ttu-id="76faf-143">S výjimkou určité soubory nebo složky z nasazení je běžné požadavek; Dalším příkladem může být do složky, které mohou uživatelé odeslat soubory do.</span><span class="sxs-lookup"><span data-stu-id="76faf-143">Excluding specific files or folders from deployment is a common requirement; another example would be a folder that users can upload files to.</span></span> <span data-ttu-id="76faf-144">Nechcete, aby se soubory protokolu nebo nahrát soubory, které byly vytvořeny ve vašem vývojovém prostředí pro nasazení do produkčního prostředí.</span><span class="sxs-lookup"><span data-stu-id="76faf-144">You don't want log files or uploaded files that were created in your development environment to be deployed to production.</span></span> <span data-ttu-id="76faf-145">A Pokud nasazujete aktualizace do produkčního prostředí nechcete, aby proces nasazení k odstranění souborů, které existují v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="76faf-145">And if you are deploying an update to production you don't want the deployment process to delete files that exist in production.</span></span> <span data-ttu-id="76faf-146">(V závislosti na tom, jak nastavit možnost nasazení, pokud soubor existuje v cílové lokalitě, ale není zdrojové lokality při nasazení, Web Deploy neodstraní z cílového.)</span><span class="sxs-lookup"><span data-stu-id="76faf-146">(Depending on how you set a deployment option, if a file exists in the destination site but not the source site when you deploy, Web Deploy deletes it from the destination.)</span></span>

<span data-ttu-id="76faf-147">Jak už jste viděli dříve v tomto kurzu **položky k nasazení** možnost **balení/publikování webu** karta je nastaven na **pouze soubory potřebné ke spuštění této aplikace**.</span><span class="sxs-lookup"><span data-stu-id="76faf-147">As you saw earlier in this tutorial, the **Items to deploy** option in the **Package/Publish Web** tab is set to **Only Files Needed to run this application**.</span></span> <span data-ttu-id="76faf-148">Výsledkem je soubory protokolů, které jsou vytvořené pomocí Elmah vývojem nebude nasazen, který se má stát.</span><span class="sxs-lookup"><span data-stu-id="76faf-148">As a result, log files that are created by Elmah in development will not be deployed, which is what you want to happen.</span></span> <span data-ttu-id="76faf-149">(Chcete-li být nasazen, by musel být zahrnutý v projektu a jejich **akce sestavení** vlastnost musel být nastavena na **obsahu**.</span><span class="sxs-lookup"><span data-stu-id="76faf-149">(To be deployed, they would have to be included in the project and their **Build Action** property would have to be set to **Content**.</span></span> <span data-ttu-id="76faf-150">Další informace najdete v tématu **proč si všechny soubory ve složce projektu nasadí?** v [ASP.NET webové aplikace projektu nasazení – nejčastější dotazy](https://msdn.microsoft.com/en-us/library/ee942158.aspx)).</span><span class="sxs-lookup"><span data-stu-id="76faf-150">For more information, see **Why don't all of the files in my project folder get deployed?** in [ASP.NET Web Application Project Deployment FAQ](https://msdn.microsoft.com/en-us/library/ee942158.aspx)).</span></span> <span data-ttu-id="76faf-151">Ale Web Deploy nebude vytvořte složku v cílové lokalitě pokud existuje alespoň jeden soubor zkopírujte do něj.</span><span class="sxs-lookup"><span data-stu-id="76faf-151">However, Web Deploy will not create a folder in the destination site unless there's at least one file to copy to it.</span></span> <span data-ttu-id="76faf-152">Proto přidáte *.txt* soubor do složky tak, aby fungoval jako zástupný znak, aby se zkopírují na složku.</span><span class="sxs-lookup"><span data-stu-id="76faf-152">Therefore, you'll add a *.txt* file to the folder to act as a placeholder so that the folder will be copied.</span></span>

<span data-ttu-id="76faf-153">V **Průzkumníku řešení**, klikněte pravým tlačítkem myši *Elmah* složky, vyberte **přidat novou položku**a vytvořte textový soubor s názvem *Placeholder.txt*.</span><span class="sxs-lookup"><span data-stu-id="76faf-153">In **Solution Explorer**, right-click the *Elmah* folder, select **Add New Item**, and create a text file named *Placeholder.txt*.</span></span> <span data-ttu-id="76faf-154">Zadejte následující text v něm: "Toto je soubor zástupný symbol zajistit, že složce nasadí."</span><span class="sxs-lookup"><span data-stu-id="76faf-154">Put the following text in it: "This is a placeholder file to ensure that the folder gets deployed."</span></span> <span data-ttu-id="76faf-155">A uložte soubor.</span><span class="sxs-lookup"><span data-stu-id="76faf-155">and save the file.</span></span> <span data-ttu-id="76faf-156">To je všechno, budete muset udělat, pokud chcete mít jistotu, že Visual Studio nasadí tento soubor a složka je v, protože **akce sestavení** vlastnost *.txt* soubory nastavena na **obsahu**ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="76faf-156">That's all you have to do in order to make sure that Visual Studio deploys this file and the folder it's in, because the **Build Action** property of *.txt* files is set to **Content** by default.</span></span>

## <a name="summary"></a><span data-ttu-id="76faf-157">Souhrn</span><span class="sxs-lookup"><span data-stu-id="76faf-157">Summary</span></span>

<span data-ttu-id="76faf-158">Teď jste dokončili všechny úlohy, nastavení nasazení.</span><span class="sxs-lookup"><span data-stu-id="76faf-158">You have now completed all of the deployment set-up tasks.</span></span> <span data-ttu-id="76faf-159">V dalším kurzu budete nasazení webu společnosti Contoso univerzity do testovacího prostředí a otestovat ji.</span><span class="sxs-lookup"><span data-stu-id="76faf-159">In the next tutorial, you'll deploy the Contoso University site to the test environment and test it there.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="76faf-160">[Předchozí](web-config-transformations.md)
[další](deploying-to-iis.md)</span><span class="sxs-lookup"><span data-stu-id="76faf-160">[Previous](web-config-transformations.md)
[Next](deploying-to-iis.md)</span></span>