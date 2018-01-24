---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: "ASP.NET MVC 4 modely a přístup k datům | Microsoft Docs"
author: rick-anderson
description: "Poznámka: Toto testovací prostředí Hands-on předpokládá, že máte základní znalosti o architektuře ASP.NET MVC. Pokud jste nepoužili ASP.NET MVC před, doporučujeme si projít ASP.NET MVC 4..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: bf4bb5c6f9ad8339c3597b0d6666c7077ac476e0
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/10/2017
---
<a name="aspnet-mvc-4-models-and-data-access"></a><span data-ttu-id="c0d09-104">ASP.NET MVC 4 modely a přístup k datům</span><span class="sxs-lookup"><span data-stu-id="c0d09-104">ASP.NET MVC 4 Models and Data Access</span></span>
====================
<span data-ttu-id="c0d09-105">podle [webové táborech Team](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="c0d09-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> [!NOTE]
> <span data-ttu-id="c0d09-106">Toto testovací prostředí Hands-on předpokládá, že máte základní znalosti o **ASP.NET MVC**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-106">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="c0d09-107">Pokud jste nepoužili **ASP.NET MVC** před, doporučujeme si projít **ASP.NET MVC 4 Základy** Hands-on testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="c0d09-107">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>
> 
> <span data-ttu-id="c0d09-108">Tato laboratoř vás provede procesem vylepšení a nových funkcí popsaných výše použitím malých změn na ukázkové webové aplikaci ve zdrojové složce zadané.</span><span class="sxs-lookup"><span data-stu-id="c0d09-108">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>
> 
> <span data-ttu-id="c0d09-109">Všechny ukázky kódu a fragmenty kódu jsou součástí webové táborech školení sady, k dispozici na [https://www.microsoft.com/en-us/download/29843](https://www.microsoft.com/en-us/download/29843).</span><span class="sxs-lookup"><span data-stu-id="c0d09-109">All sample code and snippets are included in the Web Camps Training Kit, available at [https://www.microsoft.com/en-us/download/29843](https://www.microsoft.com/en-us/download/29843).</span></span>


<span data-ttu-id="c0d09-110">V **ASP.NET MVC Základy** Hands-on testovací prostředí, můžete mít byla předávání pevně dat z řadičů šablon zobrazení.</span><span class="sxs-lookup"><span data-stu-id="c0d09-110">In **ASP.NET MVC Fundamentals** Hands-on Lab, you have been passing hard-coded data from the Controllers to the View templates.</span></span> <span data-ttu-id="c0d09-111">Ale, aby bylo možné vytvořit skutečné webové aplikace, můžete chtít použít skutečné databázi.</span><span class="sxs-lookup"><span data-stu-id="c0d09-111">But, in order to build a real Web application, you might want to use a real database.</span></span>

<span data-ttu-id="c0d09-112">Toto testovací prostředí Hands-on vám ukáže, jak používat databázový stroj, aby bylo možné ukládají a načítají data potřebná pro aplikaci služby obchodu Hudba.</span><span class="sxs-lookup"><span data-stu-id="c0d09-112">This Hands-on Lab will show you how to use a database engine in order to store and retrieve the data needed for the Music Store application.</span></span> <span data-ttu-id="c0d09-113">Provést tuto akci, bude začínat existující databázi a z něj vytvořit datového modelu Entity.</span><span class="sxs-lookup"><span data-stu-id="c0d09-113">To accomplish that, you will start with an existing database and create the Entity Data Model from it.</span></span> <span data-ttu-id="c0d09-114">V tomto testovacím prostředí bude vyhovovat **Database First** přístup a taky **Code First** přístup.</span><span class="sxs-lookup"><span data-stu-id="c0d09-114">Throughout this lab, you will meet the **Database First** approach as well as the **Code First** approach.</span></span>

<span data-ttu-id="c0d09-115">Ale můžete také použít **Model First** přístupu, vytvořte stejný model pomocí nástroje a potom z něj generovat databázi.</span><span class="sxs-lookup"><span data-stu-id="c0d09-115">However, you can also use the **Model First** approach, create the same model using the tools, and then generate the database from it.</span></span>

<span data-ttu-id="c0d09-116">![První vs databáze. Model první](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. Nejprve modelu")</span><span class="sxs-lookup"><span data-stu-id="c0d09-116">![Database First vs. Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. Model First")</span></span>

<span data-ttu-id="c0d09-117">*První vs databáze. Nejprve modelu*</span><span class="sxs-lookup"><span data-stu-id="c0d09-117">*Database First vs. Model First*</span></span>

<span data-ttu-id="c0d09-118">Po generování modelu, budou správné úpravy v StoreController poskytnout zobrazení úložiště dat získaných z databáze, místo použití pevně data.</span><span class="sxs-lookup"><span data-stu-id="c0d09-118">After generating the Model, you will make the proper adjustments in the StoreController to provide the Store Views with the data taken from the database, instead of using hard-coded data.</span></span> <span data-ttu-id="c0d09-119">Nebudete muset provádět všechny změny šablony zobrazení protože StoreController se vrátí stejné ViewModels zobrazení šablony, ale tentokrát data budou pocházet z databáze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-119">You will not need to make any change to the View templates because the StoreController will be returning the same ViewModels to the View templates, although this time the data will come from the database.</span></span>

<span data-ttu-id="c0d09-120">**Přístupu Code First**</span><span class="sxs-lookup"><span data-stu-id="c0d09-120">**The Code First Approach**</span></span>

<span data-ttu-id="c0d09-121">Code First přístup umožňuje definovat model z kódu bez generování tříd, které jsou obecně kombinaci s rozhraní.</span><span class="sxs-lookup"><span data-stu-id="c0d09-121">The Code First approach allows us to define the model from the code without generating classes that are generally coupled with the framework.</span></span>

<span data-ttu-id="c0d09-122">V kódu nejprve objekty modelu jsou definovány s POCOs, &quot;prostý staré objekty CLR&quot;.</span><span class="sxs-lookup"><span data-stu-id="c0d09-122">In code first, model objects are defined with POCOs, &quot;Plain Old CLR Objects&quot;.</span></span> <span data-ttu-id="c0d09-123">POCOs jsou jednoduché prostý třídy, které mají žádné dědičnosti a neimplementuje rozhraní.</span><span class="sxs-lookup"><span data-stu-id="c0d09-123">POCOs are simple plain classes that have no inheritance and do not implement interfaces.</span></span> <span data-ttu-id="c0d09-124">Jsme může automaticky generovat databázi z nich nebo můžeme použít existující databázi a generovat mapování třídy z kódu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-124">We can automatically generate the database from them, or we can use an existing database and generate the class mapping from the code.</span></span>

<span data-ttu-id="c0d09-125">Výhody použití tohoto přístupu je, aby zůstala modelu nezávisle trvalost framework (v tomto případě Entity Framework), jak POCOs třídy nejsou kombinaci s rozhraní mapování.</span><span class="sxs-lookup"><span data-stu-id="c0d09-125">The benefits of using this approach is that the Model remains independent from the persistence framework (in this case, Entity Framework), as the POCOs classes are not coupled with the mapping framework.</span></span>

> [!NOTE]
> <span data-ttu-id="c0d09-126">Toto testovací prostředí je založena na technologii ASP.NET MVC 4 a verzi Hudba úložiště ukázkovou aplikaci přizpůsobit a minimalizuje podle pouze funkce uvedené v tomto testovacím prostředí Hands-On.</span><span class="sxs-lookup"><span data-stu-id="c0d09-126">This Lab is based on ASP.NET MVC 4 and a version of the Music Store sample application customized and minimized to fit only the features shown in this Hands-On Lab.</span></span>
> 
> <span data-ttu-id="c0d09-127">Pokud chcete prozkoumat celek **Hudba úložiště** aplikace najdete ji v [MVC. Hudba úložiště](https://github.com/evilDave/MVC-Music-Store).</span><span class="sxs-lookup"><span data-stu-id="c0d09-127">If you wish to explore the whole **Music Store** tutorial application you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>


<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="c0d09-128">Požadavky</span><span class="sxs-lookup"><span data-stu-id="c0d09-128">Prerequisites</span></span>

<span data-ttu-id="c0d09-129">Musíte mít následující položky k dokončení tohoto testovacího prostředí:</span><span class="sxs-lookup"><span data-stu-id="c0d09-129">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="c0d09-130">[Microsoft Visual Studio Express 2012 pro Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) nebo i vyšší (čtení [příloha A](#AppendixA) pokyny o tom, jak ji nainstalovat).</span><span class="sxs-lookup"><span data-stu-id="c0d09-130">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="c0d09-131">Instalace</span><span class="sxs-lookup"><span data-stu-id="c0d09-131">Setup</span></span>

<span data-ttu-id="c0d09-132">**Instalace fragmenty kódu**</span><span class="sxs-lookup"><span data-stu-id="c0d09-132">**Installing Code Snippets**</span></span>

<span data-ttu-id="c0d09-133">Pro usnadnění práce většinu kódu, který bude spravovat podél toto testovací prostředí je k dispozici jako fragmenty kódu v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c0d09-133">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="c0d09-134">K instalaci fragmenty kódu spustit **.\Source\Setup\CodeSnippets.vsi** souboru.</span><span class="sxs-lookup"><span data-stu-id="c0d09-134">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="c0d09-135">Pokud si nejste obeznámeni s fragmenty kódu Visual Studio a chcete se dozvíte, jak používat, můžete odkazovat na příloze z tohoto dokumentu &quot; [fragmenty kódu pomocí příloha C:](#AppendixC)&quot;.</span><span class="sxs-lookup"><span data-stu-id="c0d09-135">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="c0d09-136">Cvičení</span><span class="sxs-lookup"><span data-stu-id="c0d09-136">Exercises</span></span>

<span data-ttu-id="c0d09-137">Toto testovací prostředí Hands-on se skládá ve cvičeních následující:</span><span class="sxs-lookup"><span data-stu-id="c0d09-137">This Hands-on Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="c0d09-138">Cvičení 1: Přidání databáze</span><span class="sxs-lookup"><span data-stu-id="c0d09-138">Exercise 1: Adding a Database</span></span>](#Exercise1)
2. [<span data-ttu-id="c0d09-139">Cvičení 2: Vytvoření databáze pomocí Code First</span><span class="sxs-lookup"><span data-stu-id="c0d09-139">Exercise 2: Creating a Database using Code First</span></span>](#Exercise2)
3. [<span data-ttu-id="c0d09-140">Cvičení 3: Dotaz na databázi s parametry</span><span class="sxs-lookup"><span data-stu-id="c0d09-140">Exercise 3: Querying the Database with Parameters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="c0d09-141">Každý úkol je přiložena **End** složku obsahující výsledné řešení by si měly opatřit po dokončení cvičeních.</span><span class="sxs-lookup"><span data-stu-id="c0d09-141">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="c0d09-142">Toto řešení můžete použít jako vodítko, pokud potřebujete další pomoc při procházení cvičeních.</span><span class="sxs-lookup"><span data-stu-id="c0d09-142">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="c0d09-143">Odhadovaný čas dokončení tohoto testovacího prostředí: **35 minut**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-143">Estimated time to complete this lab: **35 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a><span data-ttu-id="c0d09-144">Cvičení 1: Přidání databáze</span><span class="sxs-lookup"><span data-stu-id="c0d09-144">Exercise 1: Adding a Database</span></span>

<span data-ttu-id="c0d09-145">V tomto cvičení se dozvíte, jak přidat databáze s tabulkami aplikace MusicStore k řešení, aby bylo možné využívat jeho data.</span><span class="sxs-lookup"><span data-stu-id="c0d09-145">In this exercise, you will learn how to add a database with the tables of the MusicStore application to the solution in order to consume its data.</span></span> <span data-ttu-id="c0d09-146">Jakmile databáze je generována s modelem a k řešení přidat, upraví třídě StoreController zobrazit šablonu poskytnout dat získaných z databáze, místo pevně definovaných hodnot.</span><span class="sxs-lookup"><span data-stu-id="c0d09-146">Once the database is generated with the model, and added to the solution, you will modify the StoreController class to provide the View template with the data taken from the database, instead of using hard-coded values.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a><span data-ttu-id="c0d09-147">Úloha 1 – přidání databáze</span><span class="sxs-lookup"><span data-stu-id="c0d09-147">Task 1 - Adding a Database</span></span>

<span data-ttu-id="c0d09-148">V této úloze budete přidávat již vytvořené databáze s hlavní tabulky MusicStore aplikace k řešení.</span><span class="sxs-lookup"><span data-stu-id="c0d09-148">In this task, you will add an already created database with the main tables of the MusicStore application to the solution.</span></span>

1. <span data-ttu-id="c0d09-149">Otevřete **začít** řešení nacházející se v **zdroj/Ex1-AddingADatabaseDBFirst/počáteční/** složky.</span><span class="sxs-lookup"><span data-stu-id="c0d09-149">Open the **Begin** solution located at **Source/Ex1-AddingADatabaseDBFirst/Begin/** folder.</span></span>

    1. <span data-ttu-id="c0d09-150">Budete muset stáhnout některé chybějící balíčky NuGet než budete pokračovat.</span><span class="sxs-lookup"><span data-stu-id="c0d09-150">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c0d09-151">Chcete-li to provést, klikněte na tlačítko **projektu** nabídku a vyberte **spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-151">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="c0d09-152">V **spravovat balíčky NuGet** dialogové okno, klikněte na tlačítko **obnovení** Chcete-li stáhnout chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="c0d09-152">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="c0d09-153">Nakonec sestavte řešení kliknutím **sestavení** | **sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-153">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0d09-154">Jednou z výhod použití NuGet je, že nemáte pro odeslání všech knihoven v projektu, zmenšení velikosti projektu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-154">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c0d09-155">Napájení nástroje NuGet zadáním verze balíčku v souboru Packages.config, nebudete moct stáhnout všechny požadované knihovny při prvním spuštění projektu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-155">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c0d09-156">Z tohoto důvodu je nutné provést tyto kroky po otevření existujícího řešení z tohoto testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="c0d09-156">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="c0d09-157">Přidat **MvcMusicStore** soubor databáze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-157">Add **MvcMusicStore** database file.</span></span> <span data-ttu-id="c0d09-158">V tomto testovacím prostředí Hands-on budete používat již vytvořené databáze názvem **MvcMusicStore.mdf**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-158">In this Hands-on Lab, you will use an already created database called **MvcMusicStore.mdf**.</span></span> <span data-ttu-id="c0d09-159">To lze provést, klikněte pravým tlačítkem na **aplikace\_Data** složku, přejděte na příkaz **přidat** a pak klikněte na **existující položka**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-159">To do that, right-click **App\_Data** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="c0d09-160">Přejděte do **\Source\Assets** a vyberte **MvcMusicStore.mdf** souboru.</span><span class="sxs-lookup"><span data-stu-id="c0d09-160">Browse to **\Source\Assets** and select the **MvcMusicStore.mdf** file.</span></span>

    <span data-ttu-id="c0d09-161">![Přidat existující položku](aspnet-mvc-4-models-and-data-access/_static/image2.png "přidání existující položky")</span><span class="sxs-lookup"><span data-stu-id="c0d09-161">![Adding an Existing Item](aspnet-mvc-4-models-and-data-access/_static/image2.png "Adding an Existing Item")</span></span>

    <span data-ttu-id="c0d09-162">*Přidání existující položky*</span><span class="sxs-lookup"><span data-stu-id="c0d09-162">*Adding an Existing Item*</span></span>

    <span data-ttu-id="c0d09-163">![Soubor databáze MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf databázový soubor")</span><span class="sxs-lookup"><span data-stu-id="c0d09-163">![MvcMusicStore.mdf database file](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf database file")</span></span>

    <span data-ttu-id="c0d09-164">*Soubor databáze MvcMusicStore.mdf*</span><span class="sxs-lookup"><span data-stu-id="c0d09-164">*MvcMusicStore.mdf database file*</span></span>

    <span data-ttu-id="c0d09-165">Databáze byla přidána do projektu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-165">The database has been added to the project.</span></span> <span data-ttu-id="c0d09-166">I v případě, že databáze se nachází uvnitř řešení, se můžete dotazovat a aktualizovat ji jako byla hostované v jiné databázi serveru.</span><span class="sxs-lookup"><span data-stu-id="c0d09-166">Even when the database is located inside the solution, you can query and update it as it was hosted in a different database server.</span></span>

    <span data-ttu-id="c0d09-167">![MvcMusicStore databáze v Průzkumníku řešení](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore databáze v Průzkumníku řešení")</span><span class="sxs-lookup"><span data-stu-id="c0d09-167">![MvcMusicStore database in Solution Explorer](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore database in Solution Explorer")</span></span>

    <span data-ttu-id="c0d09-168">*MvcMusicStore databáze v Průzkumníku řešení*</span><span class="sxs-lookup"><span data-stu-id="c0d09-168">*MvcMusicStore database in Solution Explorer*</span></span>
3. <span data-ttu-id="c0d09-169">Ověřte připojení k databázi.</span><span class="sxs-lookup"><span data-stu-id="c0d09-169">Verify the connection to the database.</span></span> <span data-ttu-id="c0d09-170">Chcete-li to provést, dvakrát klikněte na **MvcMusicStore.mdf** k navázání připojení.</span><span class="sxs-lookup"><span data-stu-id="c0d09-170">To do this, double-click **MvcMusicStore.mdf** to establish a connection.</span></span>

    <span data-ttu-id="c0d09-171">![Připojení k MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "připojení k MvcMusicStore.mdf")</span><span class="sxs-lookup"><span data-stu-id="c0d09-171">![Connecting to MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "Connecting to MvcMusicStore.mdf")</span></span>

    <span data-ttu-id="c0d09-172">*Připojení k MvcMusicStore.mdf*</span><span class="sxs-lookup"><span data-stu-id="c0d09-172">*Connecting to MvcMusicStore.mdf*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a><span data-ttu-id="c0d09-173">Úloha 2 – vytváření datového modelu</span><span class="sxs-lookup"><span data-stu-id="c0d09-173">Task 2 - Creating a Data Model</span></span>

<span data-ttu-id="c0d09-174">V této úloze vytvoří datový model pro interakci s databází přidali v předchozí úloze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-174">In this task, you will create a data model to interact with the database added in the previous task.</span></span>

1. <span data-ttu-id="c0d09-175">Vytvoření datového modelu, která bude představovat databáze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-175">Create a data model that will represent the database.</span></span> <span data-ttu-id="c0d09-176">Chcete-li to provést, v Průzkumníku řešení klikněte pravým tlačítkem **modely** složku, přejděte na příkaz **přidat** a pak klikněte na **novou položku**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-176">To do this, in Solution Explorer right-click the **Models** folder, point to **Add** and then click **New Item**.</span></span> <span data-ttu-id="c0d09-177">V **přidat novou položku** dialogovém okně, vyberte **Data** šablony a potom **ADO.NET Entity Data Model** položky.</span><span class="sxs-lookup"><span data-stu-id="c0d09-177">In the **Add New Item** dialog, select the **Data** template and then the **ADO.NET Entity Data Model** item.</span></span> <span data-ttu-id="c0d09-178">Změňte název modelu dat **StoreDB.edmx** a klikněte na tlačítko **přidat**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-178">Change the data model name to **StoreDB.edmx** and click **Add**.</span></span>

    <span data-ttu-id="c0d09-179">![Přidání StoreDB ADO.NET Entity Data Model](aspnet-mvc-4-models-and-data-access/_static/image6.png "přidání StoreDB ADO.NET Entity Data Model")</span><span class="sxs-lookup"><span data-stu-id="c0d09-179">![Adding the StoreDB ADO.NET Entity Data Model](aspnet-mvc-4-models-and-data-access/_static/image6.png "Adding the StoreDB ADO.NET Entity Data Model")</span></span>

    <span data-ttu-id="c0d09-180">*Přidání StoreDB ADO.NET Entity Data Model*</span><span class="sxs-lookup"><span data-stu-id="c0d09-180">*Adding the StoreDB ADO.NET Entity Data Model*</span></span>
2. <span data-ttu-id="c0d09-181">**Entity Data Model Wizard** se zobrazí.</span><span class="sxs-lookup"><span data-stu-id="c0d09-181">The **Entity Data Model Wizard** will appear.</span></span> <span data-ttu-id="c0d09-182">Tento průvodce vás provede vytvoření vrstvy modelu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-182">This wizard will guide you through the creation of the model layer.</span></span> <span data-ttu-id="c0d09-183">Vzhledem k tomu, že model by měl být na základě vytvořit existující databáze recentyl přidat, vyberte **generování z databáze** a klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-183">Since the model should be created based on the existing database recentyl added, select **Generate from database** and click **Next**.</span></span>

    <span data-ttu-id="c0d09-184">![Výběr obsah modelu](aspnet-mvc-4-models-and-data-access/_static/image7.png "výběr obsah modelu")</span><span class="sxs-lookup"><span data-stu-id="c0d09-184">![Choosing the model content](aspnet-mvc-4-models-and-data-access/_static/image7.png "Choosing the model content")</span></span>

    <span data-ttu-id="c0d09-185">*Výběr obsah modelu*</span><span class="sxs-lookup"><span data-stu-id="c0d09-185">*Choosing the model content*</span></span>
3. <span data-ttu-id="c0d09-186">Vzhledem k tomu, že chcete generovat model z databáze, musíte zadat připojení používat.</span><span class="sxs-lookup"><span data-stu-id="c0d09-186">Since you are generating a model from a database, you will need to specify the connection to use.</span></span> <span data-ttu-id="c0d09-187">Klikněte na tlačítko **nové připojení**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-187">Click **New Connection**.</span></span>
4. <span data-ttu-id="c0d09-188">Vyberte **soubor databáze Microsoft SQL Server** a klikněte na tlačítko **pokračovat**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-188">Select **Microsoft SQL Server Database File** and click **Continue**.</span></span>

    <span data-ttu-id="c0d09-189">![Vyberte zdroj dat](aspnet-mvc-4-models-and-data-access/_static/image8.png "vybrat zdroj dat")</span><span class="sxs-lookup"><span data-stu-id="c0d09-189">![Choose data source](aspnet-mvc-4-models-and-data-access/_static/image8.png "Choose data source")</span></span>

    <span data-ttu-id="c0d09-190">*Vyberte zdroj dat dialogové okno*</span><span class="sxs-lookup"><span data-stu-id="c0d09-190">*Choose data source dialog*</span></span>
5. <span data-ttu-id="c0d09-191">Klikněte na tlačítko **Procházet** a vyberte databázi **MvcMusicStore.mdf** jste vyhledali v **aplikace\_Data** složky a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-191">Click **Browse** and select the database **MvcMusicStore.mdf** you located in the **App\_Data** folder and click **OK**.</span></span>

    <span data-ttu-id="c0d09-192">![Vlastnosti připojení](aspnet-mvc-4-models-and-data-access/_static/image9.png "vlastnosti připojení")</span><span class="sxs-lookup"><span data-stu-id="c0d09-192">![Connection properties](aspnet-mvc-4-models-and-data-access/_static/image9.png "Connection properties")</span></span>

    <span data-ttu-id="c0d09-193">*Vlastnosti připojení*</span><span class="sxs-lookup"><span data-stu-id="c0d09-193">*Connection properties*</span></span>
6. <span data-ttu-id="c0d09-194">Generovaná třída by měla mít stejný název jako připojovací řetězec entity, takže změňte její název **MusicStoreEntities** a klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-194">The generated class should have the same name as the entity connection string, so change its name to **MusicStoreEntities** and click **Next**.</span></span>

    <span data-ttu-id="c0d09-195">![Výběr datové připojení](aspnet-mvc-4-models-and-data-access/_static/image10.png "vybrat datové připojení")</span><span class="sxs-lookup"><span data-stu-id="c0d09-195">![Choosing the data connection](aspnet-mvc-4-models-and-data-access/_static/image10.png "Choosing the data connection")</span></span>

    <span data-ttu-id="c0d09-196">*Výběr datové připojení*</span><span class="sxs-lookup"><span data-stu-id="c0d09-196">*Choosing the data connection*</span></span>
7. <span data-ttu-id="c0d09-197">Vyberte objekty databáze, které chcete použít.</span><span class="sxs-lookup"><span data-stu-id="c0d09-197">Choose the database objects to use.</span></span> <span data-ttu-id="c0d09-198">Entity Model používat jenom databázové tabulky, vyberte **tabulky** možnost a ujistěte se, že **zahrnout do modelu sloupce cizích klíčů** a **množně nebo singularizovat generované názvy objektů** jsou vybrané možnosti.</span><span class="sxs-lookup"><span data-stu-id="c0d09-198">As the Entity Model will use just the database's tables, select the **Tables** option, and make sure that the **Include foreign key columns in the model** and **Pluralize or singularize generated object names** options are also selected.</span></span> <span data-ttu-id="c0d09-199">Změňte Model Namespace k **MvcMusicStore.Model** a klikněte na tlačítko **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-199">Change the Model Namespace to **MvcMusicStore.Model** and click **Finish**.</span></span>

    <span data-ttu-id="c0d09-200">![Výběr databázové objekty](aspnet-mvc-4-models-and-data-access/_static/image11.png "výběr databázové objekty")</span><span class="sxs-lookup"><span data-stu-id="c0d09-200">![Choosing the database objects](aspnet-mvc-4-models-and-data-access/_static/image11.png "Choosing the database objects")</span></span>

    <span data-ttu-id="c0d09-201">*Výběr databázové objekty*</span><span class="sxs-lookup"><span data-stu-id="c0d09-201">*Choosing the database objects*</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0d09-202">Pokud se zobrazí dialogové okno upozornění zabezpečení, klikněte na tlačítko **OK** spustit šablonu a vygenerovat třídy pro model entity.</span><span class="sxs-lookup"><span data-stu-id="c0d09-202">If a Security Warning dialog is shown, click **OK** to run the template and generate the classes for the model entities.</span></span>
8. <span data-ttu-id="c0d09-203">Diagramu entity pro databázi se zobrazí, když se vytvoří samostatnou třídu, která mapuje každou tabulku do databáze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-203">An entity diagram for the database will appear, while a separate class that maps each table to the database will be created.</span></span> <span data-ttu-id="c0d09-204">Například **alb** budou odpovídat tabulky **Album** třídy, kde bude každý sloupec v tabulce mapovat vlastnosti třídy.</span><span class="sxs-lookup"><span data-stu-id="c0d09-204">For example, the **Albums** table will be represented by an **Album** class, where each column in the table will map to a class property.</span></span> <span data-ttu-id="c0d09-205">To vám umožní pro dotazování a práce s objekty, které představují řádků v databázi.</span><span class="sxs-lookup"><span data-stu-id="c0d09-205">This will allow you to query and work with objects that represent rows in the database.</span></span>

    <span data-ttu-id="c0d09-206">![Entity diagram](aspnet-mvc-4-models-and-data-access/_static/image12.png "diagramu Entity")</span><span class="sxs-lookup"><span data-stu-id="c0d09-206">![Entity diagram](aspnet-mvc-4-models-and-data-access/_static/image12.png "Entity diagram")</span></span>

    <span data-ttu-id="c0d09-207">*Entity diagram*</span><span class="sxs-lookup"><span data-stu-id="c0d09-207">*Entity diagram*</span></span>

> [!NOTE]
> <span data-ttu-id="c0d09-208">Šablony T4 (.tt) spustit kód vygenerovat třídy entity a přepíše existující třídy se stejným názvem.</span><span class="sxs-lookup"><span data-stu-id="c0d09-208">The T4 templates (.tt) run code to generate the entities classes and will overwrite the existing classes with the same name.</span></span> <span data-ttu-id="c0d09-209">V tomto příkladu třídy &quot;Album&quot;, &quot;Genre&quot; a &quot;umělcem&quot; měla přepsat generovaného kódu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-209">In this example, the classes &quot;Album&quot;, &quot;Genre&quot; and &quot;Artist&quot; were overwritten with the generated code.</span></span>


<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a><span data-ttu-id="c0d09-210">Úloha 3 – vytvoření aplikace</span><span class="sxs-lookup"><span data-stu-id="c0d09-210">Task 3 - Building the Application</span></span>

<span data-ttu-id="c0d09-211">V této úloze bude zaškrtnete, i když generování modelu odebraly **Album**, **Genre** a **umělcem** třídy modelu, sestavení projektu úspěšně pomocí nové třídy datového modelu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-211">In this task, you will check that, although the model generation have removed the **Album**, **Genre** and **Artist** model classes, the project builds successfully by using the new data model classes.</span></span>

1. <span data-ttu-id="c0d09-212">Sestavení projektu výběrem **sestavení** položky nabídky a pak **sestavení MvcMusicStore**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-212">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="c0d09-213">![Sestavení projektu](aspnet-mvc-4-models-and-data-access/_static/image13.png "sestavení projektu")</span><span class="sxs-lookup"><span data-stu-id="c0d09-213">![Building the project](aspnet-mvc-4-models-and-data-access/_static/image13.png "Building the project")</span></span>

    <span data-ttu-id="c0d09-214">*Sestavení projektu*</span><span class="sxs-lookup"><span data-stu-id="c0d09-214">*Building the project*</span></span>
2. <span data-ttu-id="c0d09-215">Sestavení projektu úspěšně.</span><span class="sxs-lookup"><span data-stu-id="c0d09-215">The project builds successfully.</span></span> <span data-ttu-id="c0d09-216">Proč to stále funguje?</span><span class="sxs-lookup"><span data-stu-id="c0d09-216">Why does it still work?</span></span> <span data-ttu-id="c0d09-217">Funguje, protože tabulky databáze, které mají pole obsahující vlastnosti, které jste používali v odstraněné třídy **Album** a **Genre**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-217">It works because the database tables have fields that include the properties that you were using in the removed classes **Album** and **Genre**.</span></span>

    <span data-ttu-id="c0d09-218">![Sestavení bylo úspěšné](aspnet-mvc-4-models-and-data-access/_static/image14.png "sestavení bylo úspěšné")</span><span class="sxs-lookup"><span data-stu-id="c0d09-218">![Builds succeeded](aspnet-mvc-4-models-and-data-access/_static/image14.png "Builds succeeded")</span></span>

    <span data-ttu-id="c0d09-219">*Sestavení bylo úspěšné*</span><span class="sxs-lookup"><span data-stu-id="c0d09-219">*Builds succeeded*</span></span>
3. <span data-ttu-id="c0d09-220">Při návrháře zobrazí entity ve formátu diagramu, jsou skutečně třídy jazyka C#.</span><span class="sxs-lookup"><span data-stu-id="c0d09-220">While the designer displays the entities in a diagram format, they are really C# classes.</span></span> <span data-ttu-id="c0d09-221">Rozbalte **StoreDB.edmx** uzlu v Průzkumníku řešení a potom **StoreDB.tt**, zobrazí se nové generovaného entity.</span><span class="sxs-lookup"><span data-stu-id="c0d09-221">Expand the **StoreDB.edmx** node in the Solution Explorer and then **StoreDB.tt**, you will see the new generated entities.</span></span>

    <span data-ttu-id="c0d09-222">![Generované soubory](aspnet-mvc-4-models-and-data-access/_static/image15.png "generované soubory")</span><span class="sxs-lookup"><span data-stu-id="c0d09-222">![Generated files](aspnet-mvc-4-models-and-data-access/_static/image15.png "Generated files")</span></span>

    <span data-ttu-id="c0d09-223">*Generované soubory*</span><span class="sxs-lookup"><span data-stu-id="c0d09-223">*Generated files*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="c0d09-224">Úloha 4 – dotazování databáze</span><span class="sxs-lookup"><span data-stu-id="c0d09-224">Task 4 - Querying the Database</span></span>

<span data-ttu-id="c0d09-225">V této úloze tak, aby místo použití pevně zakódované data, se bude dotazovat databáze načíst informace o aktualizujte StoreController třídy.</span><span class="sxs-lookup"><span data-stu-id="c0d09-225">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will query the database to retrieve the information.</span></span>

1. <span data-ttu-id="c0d09-226">Otevřete **Controllers\StoreController.cs** a přidejte následující pole do třídy pro uložení instance **MusicStoreEntities** třídy s názvem **storeDB**:</span><span class="sxs-lookup"><span data-stu-id="c0d09-226">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="c0d09-227">(Code fragment kódu - *modely a přístup k datům - Ex1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="c0d09-227">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. <span data-ttu-id="c0d09-228">**MusicStoreEntities** třída zpřístupňuje vlastnost kolekce pro každou tabulku v databázi.</span><span class="sxs-lookup"><span data-stu-id="c0d09-228">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="c0d09-229">Aktualizace **Procházet** metody akce k načtení Genre se všemi **alb**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-229">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="c0d09-230">(Code fragment kódu - *modely a přístup k datům - Ex1 úložiště Procházet*)</span><span class="sxs-lookup"><span data-stu-id="c0d09-230">(Code Snippet - *Models And Data Access - Ex1 Store Browse*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > <span data-ttu-id="c0d09-231">Používáte funkce .NET názvem **LINQ** (language-integrated query) pro zápis výrazy silného typu dotazů vůči tyto kolekce – které bude spouštění kódu v databázi a vrátit objekty, které můžete naprogramovat proti.</span><span class="sxs-lookup"><span data-stu-id="c0d09-231">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="c0d09-232">Další informace o LINQ, naleznete [webu msdn](https://msdn.microsoft.com/en-us/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0d09-232">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/en-us/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx).</span></span>
3. <span data-ttu-id="c0d09-233">Aktualizace **Index** metody akce k načtení všech žánry.</span><span class="sxs-lookup"><span data-stu-id="c0d09-233">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="c0d09-234">(Code fragment kódu - *modely a Data Access – Index úložiště Ex1*)</span><span class="sxs-lookup"><span data-stu-id="c0d09-234">(Code Snippet - *Models And Data Access - Ex1 Store Index*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. <span data-ttu-id="c0d09-235">Aktualizace **Index** metody akce k načtení všech žánry a transformace kolekce do seznamu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-235">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="c0d09-236">(Code fragment kódu - *modely a přístup k datům - Ex1 úložiště GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="c0d09-236">(Code Snippet - *Models And Data Access - Ex1 Store GenreMenu*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="c0d09-237">Úloha 5: spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="c0d09-237">Task 5 - Running the Application</span></span>

<span data-ttu-id="c0d09-238">V této úloze zkontroluje se, že na stránce Index úložiště se nyní zobrazí žánry uloženy v databázi místo pevně zakódované ty, které jsou.</span><span class="sxs-lookup"><span data-stu-id="c0d09-238">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="c0d09-239">Není třeba měnit zobrazit šablonu, protože **StoreController** vrací stejné entity jako předtím, ale tentokrát data budou pocházet z databáze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-239">There is no need to change the View template because the **StoreController** is returning the same entities as before, although this time the data will come from the database.</span></span>

1. <span data-ttu-id="c0d09-240">Znovu sestavte řešení a stiskněte klávesu **F5** ke spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="c0d09-240">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c0d09-241">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="c0d09-241">The project starts in the Home page.</span></span> <span data-ttu-id="c0d09-242">Ověřte, že v nabídce **žánry** již není seznamu pevně zakódované a přímo načtena data z databáze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-242">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    <span data-ttu-id="c0d09-244">*Procházení žánry z databáze*</span><span class="sxs-lookup"><span data-stu-id="c0d09-244">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="c0d09-245">Nyní přejděte do jakékoli genre a ověřte, zda že alb budou naplněny z databáze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-245">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="c0d09-246">![Procházení alb z databáze](aspnet-mvc-4-models-and-data-access/_static/image17.png "procházení alb z databáze")</span><span class="sxs-lookup"><span data-stu-id="c0d09-246">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image17.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="c0d09-247">*Procházení alb z databáze*</span><span class="sxs-lookup"><span data-stu-id="c0d09-247">*Browsing Albums from the database*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a><span data-ttu-id="c0d09-248">Cvičení 2: Vytvoření databáze nejdřív pomocí kódu</span><span class="sxs-lookup"><span data-stu-id="c0d09-248">Exercise 2: Creating a Database Using Code First</span></span>

<span data-ttu-id="c0d09-249">V tomto cvičení se dozvíte, jak použít Code First přístup k vytvoření databáze s tabulkami aplikace MusicStore a jak pro přístup k jeho data.</span><span class="sxs-lookup"><span data-stu-id="c0d09-249">In this exercise, you will learn how to use the Code First approach to create a database with the tables of the MusicStore application, and how to access its data.</span></span>

<span data-ttu-id="c0d09-250">Po vygenerování modelu upravíte StoreController poskytnout dat získaných z databáze, místo použití hodnot pevně zakódované zobrazit šablonu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-250">Once the model is generated, you will modify the StoreController to provide the View template with the data taken from the database, instead of using hardcoded values.</span></span>

> [!NOTE]
> <span data-ttu-id="c0d09-251">Pokud jste dokončili cvičení 1 a už pracovali s databáze prvním přístupem, se teď Další informace o získání stejné výsledky s jiným procesem.</span><span class="sxs-lookup"><span data-stu-id="c0d09-251">If you have completed Exercise 1 and have already worked with the Database First approach, you will now learn how to get the same results with a different process.</span></span> <span data-ttu-id="c0d09-252">Úlohy, které jsou společné s cvičení 1 bylo označeno k usnadnění vaší čtení.</span><span class="sxs-lookup"><span data-stu-id="c0d09-252">The tasks that are in common with Exercise 1 have been marked to make your reading easier.</span></span> <span data-ttu-id="c0d09-253">Pokud jste nedokončili prověření 1, ale chtěli dozvědět Code First přístup, můžete spustit z tohoto cvičení a získat úplné vysvětlení tohoto tématu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-253">If you have not completed Exercise 1 but would like to learn the Code First approach, you can start from this exercise and get a full coverage of the topic.</span></span>


<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a><span data-ttu-id="c0d09-254">Úloha 1 - naplnění ukázková Data</span><span class="sxs-lookup"><span data-stu-id="c0d09-254">Task 1 - Populating Sample Data</span></span>

<span data-ttu-id="c0d09-255">V této úloze bude naplnit databázi s ukázkovými daty při výchozímu vytvoření pomocí Code First.</span><span class="sxs-lookup"><span data-stu-id="c0d09-255">In this task, you will populate the database with sample data when it is intially created using Code-First.</span></span>

1. <span data-ttu-id="c0d09-256">Otevřete **začít** řešení nacházející se v **zdroj/Ex2-CreatingADatabaseCodeFirst/počáteční/** složky.</span><span class="sxs-lookup"><span data-stu-id="c0d09-256">Open the **Begin** solution located at **Source/Ex2-CreatingADatabaseCodeFirst/Begin/** folder.</span></span> <span data-ttu-id="c0d09-257">Jinak, může pokračovat, pomocí **End** řešení získat provedením předchozím cvičení.</span><span class="sxs-lookup"><span data-stu-id="c0d09-257">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="c0d09-258">Pokud jste otevřeli poskytnutého **začít** řešení, budete muset stáhnout některé chybějící balíčky NuGet než budete pokračovat.</span><span class="sxs-lookup"><span data-stu-id="c0d09-258">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c0d09-259">Chcete-li to provést, klikněte na tlačítko **projektu** nabídku a vyberte **spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-259">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="c0d09-260">V **spravovat balíčky NuGet** dialogové okno, klikněte na tlačítko **obnovení** Chcete-li stáhnout chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="c0d09-260">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="c0d09-261">Nakonec sestavte řešení kliknutím **sestavení** | **sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-261">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0d09-262">Jednou z výhod použití NuGet je, že nemáte pro odeslání všech knihoven v projektu, zmenšení velikosti projektu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-262">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c0d09-263">Napájení nástroje NuGet zadáním verze balíčku v souboru Packages.config, nebudete moct stáhnout všechny požadované knihovny při prvním spuštění projektu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-263">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c0d09-264">Z tohoto důvodu je nutné provést tyto kroky po otevření existujícího řešení z tohoto testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="c0d09-264">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="c0d09-265">Přidat **SampleData.cs** do souboru **modely** složky.</span><span class="sxs-lookup"><span data-stu-id="c0d09-265">Add the **SampleData.cs** file to the **Models** folder.</span></span> <span data-ttu-id="c0d09-266">To lze provést, klikněte pravým tlačítkem na **modely** složku, přejděte na příkaz **přidat** a pak klikněte na **existující položka**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-266">To do that, right-click **Models** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="c0d09-267">Přejděte do **\Source\Assets** a vyberte **SampleData.cs** souboru.</span><span class="sxs-lookup"><span data-stu-id="c0d09-267">Browse to **\Source\Assets** and select the **SampleData.cs** file.</span></span>

    <span data-ttu-id="c0d09-268">![Ukázková data naplnit kódu](aspnet-mvc-4-models-and-data-access/_static/image18.png "ukázkových dat naplnit kódu")</span><span class="sxs-lookup"><span data-stu-id="c0d09-268">![Sample data populate code](aspnet-mvc-4-models-and-data-access/_static/image18.png "Sample data populate code")</span></span>

    <span data-ttu-id="c0d09-269">*Ukázková data naplnit kódu*</span><span class="sxs-lookup"><span data-stu-id="c0d09-269">*Sample data populate code*</span></span>
3. <span data-ttu-id="c0d09-270">Otevřete **Global.asax.cs** souboru a přidejte následující *pomocí* příkazy.</span><span class="sxs-lookup"><span data-stu-id="c0d09-270">Open the **Global.asax.cs** file and add the following *using* statements.</span></span>

    <span data-ttu-id="c0d09-271">(Code fragment kódu - *modely a přístup k datům - Ex2 globální direktiv Using Asax*)</span><span class="sxs-lookup"><span data-stu-id="c0d09-271">(Code Snippet - *Models And Data Access - Ex2 Global Asax Usings*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. <span data-ttu-id="c0d09-272">V **aplikace\_Start()** metoda přidejte následující řádek k nastavení inicializátoru databáze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-272">In the **Application\_Start()** method add the following line to set the database initializer.</span></span>

    <span data-ttu-id="c0d09-273">(Code fragment kódu - *modely a přístup k datům - Ex2 globální Asax SetInitializer*)</span><span class="sxs-lookup"><span data-stu-id="c0d09-273">(Code Snippet - *Models And Data Access - Ex2 Global Asax SetInitializer*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a><span data-ttu-id="c0d09-274">Úloha 2 – konfigurace připojení k databázi</span><span class="sxs-lookup"><span data-stu-id="c0d09-274">Task 2 - Configuring the connection to the Database</span></span>

<span data-ttu-id="c0d09-275">Teď, když databáze jste už přidali do našich projektu, budete psát **Web.config** souboru připojovací řetězec.</span><span class="sxs-lookup"><span data-stu-id="c0d09-275">Now that you have already added a database to our project, you will write in the **Web.config** file the connection string.</span></span>

1. <span data-ttu-id="c0d09-276">Přidat připojovací řetězec v **Web.config**. Uděláte to tak, že otevřete **Web.config** v kořenu projektu a nahraďte připojovací řetězec s názvem objekt DefaultConnection se tento řádek ve  **&lt;connectionStrings&gt;**  části:</span><span class="sxs-lookup"><span data-stu-id="c0d09-276">Add a connection string at **Web.config**. To do that, open **Web.config** at project root and replace the connection string named DefaultConnection with this line in the **&lt;connectionStrings&gt;** section:</span></span>

    <span data-ttu-id="c0d09-277">![Umístění souboru Web.config](aspnet-mvc-4-models-and-data-access/_static/image19.png "umístění souboru Web.config")</span><span class="sxs-lookup"><span data-stu-id="c0d09-277">![Web.config file location](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config file location")</span></span>

    <span data-ttu-id="c0d09-278">*Umístění souboru Web.config*</span><span class="sxs-lookup"><span data-stu-id="c0d09-278">*Web.config file location*</span></span>


    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a><span data-ttu-id="c0d09-279">Úloha 3 – práci s modelem</span><span class="sxs-lookup"><span data-stu-id="c0d09-279">Task 3 - Working with the Model</span></span>

<span data-ttu-id="c0d09-280">Teď, když už jste nakonfigurovali připojení k databázi, propojíte model s databázových tabulek.</span><span class="sxs-lookup"><span data-stu-id="c0d09-280">Now that you have already configured the connection to the database, you will link the model with the database tables.</span></span> <span data-ttu-id="c0d09-281">V této úloze vytvoříte třídu, která propojí do databáze s Code First.</span><span class="sxs-lookup"><span data-stu-id="c0d09-281">In this task, you will create a class that will be linked to the database with Code First.</span></span> <span data-ttu-id="c0d09-282">Mějte na paměti, že je existující třídy modelu objektů POCO, které by měl být upraven.</span><span class="sxs-lookup"><span data-stu-id="c0d09-282">Remember that there is an existent POCO model class that should be modified.</span></span>

> [!NOTE]
> <span data-ttu-id="c0d09-283">Pokud jste dokončili cvičení 1, Všimněte si, že se tento krok provést pomocí průvodce.</span><span class="sxs-lookup"><span data-stu-id="c0d09-283">If you completed Exercise 1, you will note that this step was performed by a wizard.</span></span> <span data-ttu-id="c0d09-284">Pomocí tohoto postupu Code First, ručně vytvoříte třídy, které budou propojené s dat entity.</span><span class="sxs-lookup"><span data-stu-id="c0d09-284">By doing Code First, you will manually create classes that will be linked to data entities.</span></span>


1. <span data-ttu-id="c0d09-285">Otevřete třídu modelu objektů POCO **Genre** z **modely** projektu složky a obsahovat identifikátor.</span><span class="sxs-lookup"><span data-stu-id="c0d09-285">Open the POCO model class **Genre** from **Models** project folder and include an ID.</span></span> <span data-ttu-id="c0d09-286">Použít interní vlastnost s názvem **GenreId**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-286">Use an int property with the name **GenreId**.</span></span>

    <span data-ttu-id="c0d09-287">(Code fragment kódu - *modely a přístup k datům - Ex2 kód první Genre*)</span><span class="sxs-lookup"><span data-stu-id="c0d09-287">(Code Snippet - *Models And Data Access - Ex2 Code First Genre*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="c0d09-288">Pro práci s Code First názvů, třídy Genre musí mít vlastnost primárního klíče, který bude automaticky zjistit.</span><span class="sxs-lookup"><span data-stu-id="c0d09-288">To work with Code First conventions, the class Genre must have a primary key property that will be automatically detected.</span></span>
    > 
    > <span data-ttu-id="c0d09-289">Další informace o první pravidla týkající se kódu v tomto [článku na webu msdn](https://msdn.microsoft.com/en-us/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0d09-289">You can read more about Code First Conventions in this [msdn article](https://msdn.microsoft.com/en-us/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx).</span></span>
2. <span data-ttu-id="c0d09-290">Nyní otevřete třídu modelu objektů POCO **Album** z **modely** projektu složky a zahrnují cizí klíče, vytvoření vlastností s názvy **GenreId** a  **ArtistId**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-290">Now, open the POCO model class **Album** from **Models** project folder and include the foreign keys, create properties with the names **GenreId** and **ArtistId**.</span></span> <span data-ttu-id="c0d09-291">Tato třída už máte **GenreId** pro primární klíč.</span><span class="sxs-lookup"><span data-stu-id="c0d09-291">This class already have the **GenreId** for the primary key.</span></span>

    <span data-ttu-id="c0d09-292">(Code fragment kódu - *modely a přístup k datům - Ex2 kód prvního alba*)</span><span class="sxs-lookup"><span data-stu-id="c0d09-292">(Code Snippet - *Models And Data Access - Ex2 Code First Album*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. <span data-ttu-id="c0d09-293">Otevřete třídu modelu objektů POCO **umělcem** a zahrnout **ArtistId** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="c0d09-293">Open the POCO model class **Artist** and include the **ArtistId** property.</span></span>

    <span data-ttu-id="c0d09-294">(Code fragment kódu - *modely a přístup k datům - Ex2 kód první umělcem*)</span><span class="sxs-lookup"><span data-stu-id="c0d09-294">(Code Snippet - *Models And Data Access - Ex2 Code First Artist*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. <span data-ttu-id="c0d09-295">Klikněte pravým tlačítkem myši **modely** složky projektu a vyberte **přidat | Třída**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-295">Right-click the **Models** project folder and select **Add | Class**.</span></span> <span data-ttu-id="c0d09-296">Název souboru **MusicStoreEntities.cs**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-296">Name the file **MusicStoreEntities.cs**.</span></span> <span data-ttu-id="c0d09-297">Potom klikněte na **přidat.**</span><span class="sxs-lookup"><span data-stu-id="c0d09-297">Then, click **Add.**</span></span>

    <span data-ttu-id="c0d09-298">![Přidání třídy](aspnet-mvc-4-models-and-data-access/_static/image20.png "přidání třídy")</span><span class="sxs-lookup"><span data-stu-id="c0d09-298">![Adding a class](aspnet-mvc-4-models-and-data-access/_static/image20.png "Adding a class")</span></span>

    <span data-ttu-id="c0d09-299">*Přidání nové položky*</span><span class="sxs-lookup"><span data-stu-id="c0d09-299">*Adding a new item*</span></span>

    <span data-ttu-id="c0d09-300">![Přidání class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "přidávání class2")</span><span class="sxs-lookup"><span data-stu-id="c0d09-300">![Adding a class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "Adding a class2")</span></span>

    <span data-ttu-id="c0d09-301">*Přidání třídy*</span><span class="sxs-lookup"><span data-stu-id="c0d09-301">*Adding a class*</span></span>
5. <span data-ttu-id="c0d09-302">Třída jste právě vytvořili, otevřete **MusicStoreEntities.cs**a přidají obory názvů **System.Data.Entity** a **System.Data.Entity.Infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-302">Open the class you have just created, **MusicStoreEntities.cs**, and include the namespaces **System.Data.Entity** and **System.Data.Entity.Infrastructure**.</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. <span data-ttu-id="c0d09-303">Nahraďte deklaraci třídy rozšířit **DbContext** – třída: deklarovat veřejné **DBSet** a přepsání **OnModelCreating** metoda.</span><span class="sxs-lookup"><span data-stu-id="c0d09-303">Replace the class declaration to extend the **DbContext** class: declare a public **DBSet** and override **OnModelCreating** method.</span></span> <span data-ttu-id="c0d09-304">Po provedení tohoto kroku budete mít domény třídu, která odkaz modelu pomocí rozhraní Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="c0d09-304">After this step you will get a domain class that will link your model with the Entity Framework.</span></span> <span data-ttu-id="c0d09-305">Aby bylo možné provést, nahraďte kód třídy následující:</span><span class="sxs-lookup"><span data-stu-id="c0d09-305">In order to do that, replace the class code with the following:</span></span>

    <span data-ttu-id="c0d09-306">(Code fragment kódu - *modely a přístup k datům - Ex2 kód první MusicStoreEntities*)</span><span class="sxs-lookup"><span data-stu-id="c0d09-306">(Code Snippet - *Models And Data Access - Ex2 Code First MusicStoreEntities*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

    > [!NOTE]
    > <span data-ttu-id="c0d09-307">S platformou Entity Framework **DbContext** a **DBSet** bude moci dotazovat třídu objektů POCO Genre.</span><span class="sxs-lookup"><span data-stu-id="c0d09-307">With Entity Framework **DbContext** and **DBSet** you will be able to query the POCO class Genre.</span></span> <span data-ttu-id="c0d09-308">Tím, že rozšíří **OnModelCreating** metoda, určíte v **kód** mapovány Genre do databázové tabulky.</span><span class="sxs-lookup"><span data-stu-id="c0d09-308">By extending **OnModelCreating** method, you are specifying in the **code** how Genre will be mapped to a database table.</span></span> <span data-ttu-id="c0d09-309">Další informace o DBContext a DBSet najdete v tomto článku msdn: [odkaz](https://msdn.microsoft.com/en-us/library/system.data.entity.dbcontext(v=vs.103).aspx)</span><span class="sxs-lookup"><span data-stu-id="c0d09-309">You can find more information about DBContext and DBSet in this msdn article: [link](https://msdn.microsoft.com/en-us/library/system.data.entity.dbcontext(v=vs.103).aspx)</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="c0d09-310">Úloha 4 – dotazování databáze</span><span class="sxs-lookup"><span data-stu-id="c0d09-310">Task 4 - Querying the Database</span></span>

<span data-ttu-id="c0d09-311">V této úloze bude aktualizace třídy pro StoreController tak, aby místo použití pevně zakódované dat, načte se z databáze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-311">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will retrieve it from the database.</span></span>

> [!NOTE]
> <span data-ttu-id="c0d09-312">Tato úloha je společné s cvičení 1.</span><span class="sxs-lookup"><span data-stu-id="c0d09-312">This task is in common with Exercise 1.</span></span>
> 
> <span data-ttu-id="c0d09-313">Pokud jste dokončili cvičení 1 Všimněte si tyto kroky jsou stejné v obou přístupů (první databáze nebo nejprve Code).</span><span class="sxs-lookup"><span data-stu-id="c0d09-313">If you completed Exercise 1 you will note these steps are the same in both approaches (Database first or Code first).</span></span> <span data-ttu-id="c0d09-314">Liší se v tom, jak data jsou spojena s modelem, ale přístup k data entity je ještě transparentní z řadiče.</span><span class="sxs-lookup"><span data-stu-id="c0d09-314">They are different in how the data is linked with the model, but the access to data entities is yet transparent from the controller.</span></span>


1. <span data-ttu-id="c0d09-315">Otevřete **Controllers\StoreController.cs** a přidejte následující pole do třídy pro uložení instance **MusicStoreEntities** třídy s názvem **storeDB**:</span><span class="sxs-lookup"><span data-stu-id="c0d09-315">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="c0d09-316">(Code fragment kódu - *modely a přístup k datům - Ex1 storeDB*)</span><span class="sxs-lookup"><span data-stu-id="c0d09-316">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. <span data-ttu-id="c0d09-317">**MusicStoreEntities** třída zpřístupňuje vlastnost kolekce pro každou tabulku v databázi.</span><span class="sxs-lookup"><span data-stu-id="c0d09-317">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="c0d09-318">Aktualizace **Procházet** metody akce k načtení Genre se všemi **alb**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-318">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="c0d09-319">(Code fragment kódu - *modely a přístup k datům - procházet úložiště Ex2*)</span><span class="sxs-lookup"><span data-stu-id="c0d09-319">(Code Snippet - *Models And Data Access - Ex2 Store Browse*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="c0d09-320">Používáte funkce .NET názvem **LINQ** (language-integrated query) pro zápis výrazy silného typu dotazů vůči tyto kolekce – které bude spouštění kódu v databázi a vrátit objekty, které můžete naprogramovat proti.</span><span class="sxs-lookup"><span data-stu-id="c0d09-320">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="c0d09-321">Další informace o LINQ, naleznete [webu msdn](https://msdn.microsoft.com/en-us/library/bb397926(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="c0d09-321">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/en-us/library/bb397926(v=vs.110).aspx).</span></span>
3. <span data-ttu-id="c0d09-322">Aktualizace **Index** metody akce k načtení všech žánry.</span><span class="sxs-lookup"><span data-stu-id="c0d09-322">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="c0d09-323">(Code fragment kódu - *modely a Data Access – Index úložiště Ex2*)</span><span class="sxs-lookup"><span data-stu-id="c0d09-323">(Code Snippet - *Models And Data Access - Ex2 Store Index*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. <span data-ttu-id="c0d09-324">Aktualizace **Index** metody akce k načtení všech žánry a transformace kolekce do seznamu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-324">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="c0d09-325">(Code fragment kódu - *modely a přístup k datům - Ex2 úložiště GenreMenu*)</span><span class="sxs-lookup"><span data-stu-id="c0d09-325">(Code Snippet - *Models And Data Access - Ex2 Store GenreMenu*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="c0d09-326">Úloha 5: spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="c0d09-326">Task 5 - Running the Application</span></span>

<span data-ttu-id="c0d09-327">V této úloze zkontroluje se, že na stránce Index úložiště se nyní zobrazí žánry uloženy v databázi místo pevně zakódované ty, které jsou.</span><span class="sxs-lookup"><span data-stu-id="c0d09-327">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="c0d09-328">Není třeba měnit zobrazit šablonu, protože **StoreController** vrací stejné **StoreIndexViewModel** jako předtím, ale tentokrát budou pocházet data z databáze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-328">There is no need to change the View template because the **StoreController** is returning the same **StoreIndexViewModel** as before, but this time the data will come from the database.</span></span>

1. <span data-ttu-id="c0d09-329">Znovu sestavte řešení a stiskněte klávesu **F5** ke spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="c0d09-329">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c0d09-330">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="c0d09-330">The project starts in the Home page.</span></span> <span data-ttu-id="c0d09-331">Ověřte, že v nabídce **žánry** již není seznamu pevně zakódované a přímo načtena data z databáze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-331">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    <span data-ttu-id="c0d09-333">*Procházení žánry z databáze*</span><span class="sxs-lookup"><span data-stu-id="c0d09-333">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="c0d09-334">Nyní přejděte do jakékoli genre a ověřte, zda že alb budou naplněny z databáze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-334">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="c0d09-335">![Procházení alb z databáze](aspnet-mvc-4-models-and-data-access/_static/image23.png "procházení alb z databáze")</span><span class="sxs-lookup"><span data-stu-id="c0d09-335">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image23.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="c0d09-336">*Procházení alb z databáze*</span><span class="sxs-lookup"><span data-stu-id="c0d09-336">*Browsing Albums from the database*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a><span data-ttu-id="c0d09-337">Cvičení 3: Dotaz na databázi s parametry</span><span class="sxs-lookup"><span data-stu-id="c0d09-337">Exercise 3: Querying the Database with Parameters</span></span>

<span data-ttu-id="c0d09-338">V tomto cvičení se dozvíte, jak k dotazování databáze pomocí parametrů a jak používat službu Shaping výsledků dotazu, funkce, která snižuje počet databáze přistupuje k načítání dat v efektivnější.</span><span class="sxs-lookup"><span data-stu-id="c0d09-338">In this exercise, you will learn how to query the database using parameters, and how to use Query Result Shaping, a feature that reduces the number database accesses retrieving data in a more efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="c0d09-339">Další informace o Shaping výsledek dotazu naleznete na následujícím [článku na webu msdn](https://msdn.microsoft.com/en-us/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0d09-339">For further information on Query Result Shaping, visit the following [msdn article](https://msdn.microsoft.com/en-us/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx).</span></span>


<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a><span data-ttu-id="c0d09-340">Úloha 1 – změny StoreController alb načíst z databáze</span><span class="sxs-lookup"><span data-stu-id="c0d09-340">Task 1 - Modifying StoreController to Retrieve Albums from Database</span></span>

<span data-ttu-id="c0d09-341">V této úloze se změní **StoreController** třídy pro přístup k databázi načíst alb z konkrétní genre.</span><span class="sxs-lookup"><span data-stu-id="c0d09-341">In this task, you will change the **StoreController** class to access the database to retrieve albums from a specific genre.</span></span>

1. <span data-ttu-id="c0d09-342">Otevřete **začít** řešení nacházející se v **Source\Ex3 QueryingTheDatabaseWithParametersCodeFirst\Begin** složky, pokud chcete použít první kód nebo **Source\ EX3. QueryingTheDatabaseWithParametersDBFirst\Begin** složky, pokud chcete použít první databáze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-342">Open the **Begin** solution located at the **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin** folder if you want to use Code-First approach or **Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin** folder if you want to use Database-First approach.</span></span> <span data-ttu-id="c0d09-343">Jinak, může pokračovat, pomocí **End** řešení získat provedením předchozím cvičení.</span><span class="sxs-lookup"><span data-stu-id="c0d09-343">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="c0d09-344">Pokud jste otevřeli poskytnutého **začít** řešení, budete muset stáhnout některé chybějící balíčky NuGet než budete pokračovat.</span><span class="sxs-lookup"><span data-stu-id="c0d09-344">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="c0d09-345">Chcete-li to provést, klikněte na tlačítko **projektu** nabídku a vyberte **spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-345">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="c0d09-346">V **spravovat balíčky NuGet** dialogové okno, klikněte na tlačítko **obnovení** Chcete-li stáhnout chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="c0d09-346">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="c0d09-347">Nakonec sestavte řešení kliknutím **sestavení** | **sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-347">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0d09-348">Jednou z výhod použití NuGet je, že nemáte pro odeslání všech knihoven v projektu, zmenšení velikosti projektu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-348">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="c0d09-349">Napájení nástroje NuGet zadáním verze balíčku v souboru Packages.config, nebudete moct stáhnout všechny požadované knihovny při prvním spuštění projektu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-349">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="c0d09-350">Z tohoto důvodu je nutné provést tyto kroky po otevření existujícího řešení z tohoto testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="c0d09-350">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="c0d09-351">Otevřete **StoreController** třída změnit **Procházet** metody akce.</span><span class="sxs-lookup"><span data-stu-id="c0d09-351">Open the **StoreController** class to change the **Browse** action method.</span></span> <span data-ttu-id="c0d09-352">Chcete-li to provést, v **Průzkumníku řešení**, rozbalte **řadiče** složku a dvojím kliknutím **StoreController.cs**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-352">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
3. <span data-ttu-id="c0d09-353">Změna **Procházet** metody akce k načtení alb pro konkrétní genre.</span><span class="sxs-lookup"><span data-stu-id="c0d09-353">Change the **Browse** action method to retrieve albums for a specific genre.</span></span> <span data-ttu-id="c0d09-354">Chcete-li to provést, nahraďte následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="c0d09-354">To do this, replace the following code:</span></span>

    <span data-ttu-id="c0d09-355">(Code fragment kódu - *modely a přístup k datům - EX3. StoreController BrowseMethod*)</span><span class="sxs-lookup"><span data-stu-id="c0d09-355">(Code Snippet - *Models And Data Access - Ex3 StoreController BrowseMethod*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

    > [!NOTE]
    > <span data-ttu-id="c0d09-356">K naplnění kolekce entit, budete muset použít **zahrnout** metoda k určení, můžete obnovit alb příliš.</span><span class="sxs-lookup"><span data-stu-id="c0d09-356">To populate a collection of the entity, you need to use the **Include** method to specify you want to retrieve the albums too.</span></span> <span data-ttu-id="c0d09-357">Můžete použít. **Single()** rozšíření v technologii LINQ protože v takovém případě je očekávána pouze jedna genre pro album.</span><span class="sxs-lookup"><span data-stu-id="c0d09-357">You can use the .**Single()** extension in LINQ because in this case only one genre is expected for an album.</span></span> <span data-ttu-id="c0d09-358">**Single()** metoda přebírá jako parametr, který v tomto případě Určuje jeden objekt Genre tak, aby jeho název odpovídá definovanou hodnotu výrazu Lambda.</span><span class="sxs-lookup"><span data-stu-id="c0d09-358">The **Single()** method takes a Lambda expression as a parameter, which in this case specifies a single Genre object such that its name matches the value defined.</span></span>
    > 
    > <span data-ttu-id="c0d09-359">Bude využít výhod funkce, která umožňuje určit další, které chcete také načíst, když je načíst objekt Genre entit v relaci.</span><span class="sxs-lookup"><span data-stu-id="c0d09-359">You will take advantage of a feature that allows you to indicate other related entities you want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="c0d09-360">Tato funkce je volána **Shaping výsledek dotazu**a umožňuje snížit počet pokusů, které jsou potřebné pro přístup k databázi k načtení informací.</span><span class="sxs-lookup"><span data-stu-id="c0d09-360">This feature is called **Query Result Shaping**, and enables you to reduce the number of times needed to access the database to retrieve information.</span></span> <span data-ttu-id="c0d09-361">V tomto scénáři můžete předem načíst alba pro Genre je načíst.</span><span class="sxs-lookup"><span data-stu-id="c0d09-361">In this scenario, you will want to pre-fetch the Albums for the Genre you retrieve.</span></span>
    > 
    > <span data-ttu-id="c0d09-362">Dotaz obsahuje **Genres.Include (&quot;alb&quot;)** k označení, že chcete také související alb.</span><span class="sxs-lookup"><span data-stu-id="c0d09-362">The query includes **Genres.Include(&quot;Albums&quot;)** to indicate that you want related albums as well.</span></span> <span data-ttu-id="c0d09-363">Výsledkem bude efektivnější aplikaci, vzhledem k tomu, že ho načte Genre a Album data v požadavku jedné databáze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-363">This will result in a more efficient application, since it will retrieve both Genre and Album data in a single database request.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="c0d09-364">Úloha 2 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="c0d09-364">Task 2 - Running the Application</span></span>

<span data-ttu-id="c0d09-365">V této úloze se spustit aplikaci a načtení alb konkrétní genre z databáze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-365">In this task, you will run the application and retrieve albums of a specific genre from the database.</span></span>

1. <span data-ttu-id="c0d09-366">Stiskněte klávesu **F5** ke spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="c0d09-366">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c0d09-367">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="c0d09-367">The project starts in the Home page.</span></span> <span data-ttu-id="c0d09-368">Změňte adresu URL na **/úložiště/procházet? genre = Pop** k ověření, že výsledky jsou načítány z databáze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-368">Change the URL to **/Store/Browse?genre=Pop** to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="c0d09-369">![Procházení podle genre](aspnet-mvc-4-models-and-data-access/_static/image24.png "procházení podle genre")</span><span class="sxs-lookup"><span data-stu-id="c0d09-369">![Browsing by genre](aspnet-mvc-4-models-and-data-access/_static/image24.png "Browsing by genre")</span></span>

    <span data-ttu-id="c0d09-370">*Procházení/úložiště/procházet? genre = Pop*</span><span class="sxs-lookup"><span data-stu-id="c0d09-370">*Browsing /Store/Browse?genre=Pop*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a><span data-ttu-id="c0d09-371">Úloha 3 – přístup k alb podle Id</span><span class="sxs-lookup"><span data-stu-id="c0d09-371">Task 3 - Accessing Albums by Id</span></span>

<span data-ttu-id="c0d09-372">V této úloze bude opakujte předchozí postup k získání alb podle jejich Id.</span><span class="sxs-lookup"><span data-stu-id="c0d09-372">In this task, you will repeat the previous procedure to get albums by their Id.</span></span>

1. <span data-ttu-id="c0d09-373">Zavřete prohlížeč v případě potřeby se vraťte do sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c0d09-373">Close the browser if needed, to return to Visual Studio.</span></span> <span data-ttu-id="c0d09-374">Otevřete **StoreController** třída změnit **podrobnosti** metody akce.</span><span class="sxs-lookup"><span data-stu-id="c0d09-374">Open the **StoreController** class to change the **Details** action method.</span></span> <span data-ttu-id="c0d09-375">Chcete-li to provést, v **Průzkumníku řešení**, rozbalte **řadiče** složku a dvojím kliknutím **StoreController.cs**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-375">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
2. <span data-ttu-id="c0d09-376">Změna **podrobnosti** metoda akce se načíst podrobnosti o alb na základě jejich **Id**. Chcete-li to provést, nahraďte následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="c0d09-376">Change the **Details** action method to retrieve albums details based on their **Id**. To do this, replace the following code:</span></span>

    <span data-ttu-id="c0d09-377">(Code fragment kódu - *modely a přístup k datům - EX3. StoreController DetailsMethod*)</span><span class="sxs-lookup"><span data-stu-id="c0d09-377">(Code Snippet - *Models And Data Access - Ex3 StoreController DetailsMethod*)</span></span>


    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="c0d09-378">Úloha 4 – spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="c0d09-378">Task 4 - Running the Application</span></span>

<span data-ttu-id="c0d09-379">V této úloze se spustit aplikaci ve webovém prohlížeči a získat podrobnosti o album podle jejich Id.</span><span class="sxs-lookup"><span data-stu-id="c0d09-379">In this task, you will run the Application in a web browser and obtain album details by their Id.</span></span>

1. <span data-ttu-id="c0d09-380">Stiskněte klávesu **F5** ke spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="c0d09-380">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="c0d09-381">Projekt se spustí na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="c0d09-381">The project starts in the Home page.</span></span> <span data-ttu-id="c0d09-382">Změňte adresu URL na **/Store/Details/51** nebo žánry Procházet a vyberte album k ověření, že výsledky jsou načítány z databáze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-382">Change the URL to **/Store/Details/51** or browse the genres and select an album to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="c0d09-383">![Procházení podrobností](aspnet-mvc-4-models-and-data-access/_static/image25.png "procházení podrobností")</span><span class="sxs-lookup"><span data-stu-id="c0d09-383">![Browsing Details](aspnet-mvc-4-models-and-data-access/_static/image25.png "Browsing Details")</span></span>

    <span data-ttu-id="c0d09-384">*Procházení /Store/Details/51*</span><span class="sxs-lookup"><span data-stu-id="c0d09-384">*Browsing /Store/Details/51*</span></span>

> [!NOTE]
> <span data-ttu-id="c0d09-385">Kromě toho můžete nasadit tuto aplikaci do následující weby systému Windows Azure [příloha B: publikování aplikace ASP.NET MVC 4 pomocí nástroje nasazení webu](#AppendixB).</span><span class="sxs-lookup"><span data-stu-id="c0d09-385">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>


* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="c0d09-386">Souhrn</span><span class="sxs-lookup"><span data-stu-id="c0d09-386">Summary</span></span>

<span data-ttu-id="c0d09-387">Pomocí dokončení tohoto testovacího prostředí Hands-on jste se naučili základy modely ASP.NET MVC a přístup k datům, pomocí **Database First** přístup a taky **Code First** přístup:</span><span class="sxs-lookup"><span data-stu-id="c0d09-387">By completing this Hands-on Lab you have learned the fundamentals of ASP.NET MVC Models and Data Access, using the **Database First** approach as well as the **Code First** Approach:</span></span>

- <span data-ttu-id="c0d09-388">Jak přidat databáze do řešení, aby bylo možné využívat svá data</span><span class="sxs-lookup"><span data-stu-id="c0d09-388">How to add a database to the solution in order to consume its data</span></span>
- <span data-ttu-id="c0d09-389">Postup aktualizace řadičů poskytnout šablon zobrazení dat získaných z databáze místo pevně jeden</span><span class="sxs-lookup"><span data-stu-id="c0d09-389">How to update Controllers to provide View templates with the data taken from the database instead of hard-coded one</span></span>
- <span data-ttu-id="c0d09-390">Postup dotazování databáze pomocí parametrů</span><span class="sxs-lookup"><span data-stu-id="c0d09-390">How to query the database using parameters</span></span>
- <span data-ttu-id="c0d09-391">Jak používat dotazu výsledek tvarování, funkce, která snižuje počet přístupům do databáze, načítání dat v efektivnější</span><span class="sxs-lookup"><span data-stu-id="c0d09-391">How to use the Query Result Shaping, a feature that reduces the number of database accesses, retrieving data in a more efficient way</span></span>
- <span data-ttu-id="c0d09-392">Jak používat první databáze a Code First přístupy v Microsoft Entity Framework propojení databáze s modelem</span><span class="sxs-lookup"><span data-stu-id="c0d09-392">How to use both Database First and Code First approaches in Microsoft Entity Framework to link the database with the model</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="c0d09-393">Příloha A: instalaci sady Visual Studio Express 2012 pro Web</span><span class="sxs-lookup"><span data-stu-id="c0d09-393">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="c0d09-394">Můžete nainstalovat **Microsoft Visual Studio Express 2012 pro Web** nebo jiný &quot;Express&quot; pomocí verze  **[instalačního programu webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="c0d09-394">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="c0d09-395">Následující pokyny vás provede kroky potřebné k instalaci *Visual studio Express 2012 pro Web* pomocí *instalačního programu webové platformy Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="c0d09-395">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="c0d09-396">Přejděte na [ [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="c0d09-396">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="c0d09-397">Případně, pokud jste již nainstalovali instalačního programu webové platformy, můžete otevřít a vyhledejte produktu &quot; *Visual Studio Express 2012 pro Web se sadou Windows Azure SDK*&quot;.</span><span class="sxs-lookup"><span data-stu-id="c0d09-397">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*Visual Studio Express 2012 for Web with Windows Azure SDK*&quot;.</span></span>
2. <span data-ttu-id="c0d09-398">Klikněte na **nyní nainstalovat**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-398">Click on **Install Now**.</span></span> <span data-ttu-id="c0d09-399">Pokud nemáte **instalačního programu webové platformy** budete přesměrováni na stáhněte a nainstalujte ji jako první.</span><span class="sxs-lookup"><span data-stu-id="c0d09-399">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="c0d09-400">Jednou **instalačního programu webové platformy** je otevřený, klikněte na tlačítko **nainstalovat** zahájíte instalaci.</span><span class="sxs-lookup"><span data-stu-id="c0d09-400">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="c0d09-401">![Nainstalovat Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "nainstalovat Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="c0d09-401">![Install Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="c0d09-402">*Nainstalovat Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="c0d09-402">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="c0d09-403">Číst všechny produkty se licence a podmínky a klikněte na tlačítko **souhlasím** pokračujte.</span><span class="sxs-lookup"><span data-stu-id="c0d09-403">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Vyjádření souhlasu s podmínkami licence](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    <span data-ttu-id="c0d09-405">*Vyjádření souhlasu s podmínkami licence*</span><span class="sxs-lookup"><span data-stu-id="c0d09-405">*Accepting the license terms*</span></span>
5. <span data-ttu-id="c0d09-406">Počkejte na dokončení procesu stahování a instalaci.</span><span class="sxs-lookup"><span data-stu-id="c0d09-406">Wait until the downloading and installation process completes.</span></span>

    ![Průběh instalace](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    <span data-ttu-id="c0d09-408">*Průběh instalace*</span><span class="sxs-lookup"><span data-stu-id="c0d09-408">*Installation progress*</span></span>
6. <span data-ttu-id="c0d09-409">Po dokončení instalace, klikněte na tlačítko **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-409">When the installation completes, click **Finish**.</span></span>

    ![Instalace byla dokončena.](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    <span data-ttu-id="c0d09-411">*Instalace byla dokončena.*</span><span class="sxs-lookup"><span data-stu-id="c0d09-411">*Installation completed*</span></span>
7. <span data-ttu-id="c0d09-412">Klikněte na tlačítko **ukončení** ukončíte instalační program webové platformy.</span><span class="sxs-lookup"><span data-stu-id="c0d09-412">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="c0d09-413">Chcete-li spustit nástroj Visual Studio Express pro Web, přejděte na **spustit** obrazovky a začít psát &quot; **VS Express**&quot;, klikněte na **VS Express pro Web** dlaždice.</span><span class="sxs-lookup"><span data-stu-id="c0d09-413">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express pro Web dlaždice](aspnet-mvc-4-models-and-data-access/_static/image30.png)

    <span data-ttu-id="c0d09-415">*VS Express pro Web dlaždice*</span><span class="sxs-lookup"><span data-stu-id="c0d09-415">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="c0d09-416">Příloha B: publikování aplikace ASP.NET MVC 4 pomocí nástroje nasazení webu</span><span class="sxs-lookup"><span data-stu-id="c0d09-416">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="c0d09-417">Tento dodatek vám ukáže, jak vytvořit nový web z portálu Windows Azure Management Portal a publikovat aplikace, kterou jste získali podle testovacím prostředí, využívat výhod nasazení webu publikování funkce poskytované služby Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="c0d09-417">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="c0d09-418">Úloha 1 – Vytvoření nového webu ze systému Windows Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c0d09-418">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="c0d09-419">Přejděte na [Windows Azure Management Portal](https://manage.windowsazure.com/) a přihlaste se pomocí přihlašovacích údajů společnosti Microsoft, které jsou spojené s vaším předplatným.</span><span class="sxs-lookup"><span data-stu-id="c0d09-419">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0d09-420">S Windows Azure můžete bezplatné hostování 10 webů ASP.NET a pak škálujte podle rozšiřujícího se provozu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-420">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="c0d09-421">Můžete si zaregistrovat [zde](http://aka.ms/aspnet-hol-azure).</span><span class="sxs-lookup"><span data-stu-id="c0d09-421">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="c0d09-422">![Přihlaste se k portálu Windows Azure](aspnet-mvc-4-models-and-data-access/_static/image31.png "Přihlaste se k portálu Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="c0d09-422">![Log on to Windows Azure portal](aspnet-mvc-4-models-and-data-access/_static/image31.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="c0d09-423">*Přihlaste se k Windows Azure Management Portal*</span><span class="sxs-lookup"><span data-stu-id="c0d09-423">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="c0d09-424">Klikněte na tlačítko **nový** na panelu příkazů.</span><span class="sxs-lookup"><span data-stu-id="c0d09-424">Click **New** on the command bar.</span></span>

    <span data-ttu-id="c0d09-425">![Vytvoření nového webu](aspnet-mvc-4-models-and-data-access/_static/image32.png "vytváření nového webu")</span><span class="sxs-lookup"><span data-stu-id="c0d09-425">![Creating a new Web Site](aspnet-mvc-4-models-and-data-access/_static/image32.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="c0d09-426">*Vytvoření nového webu*</span><span class="sxs-lookup"><span data-stu-id="c0d09-426">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="c0d09-427">Klikněte na tlačítko **výpočetní** | **webu**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-427">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="c0d09-428">Potom vyberte **rychle vytvořit** možnost.</span><span class="sxs-lookup"><span data-stu-id="c0d09-428">Then select **Quick Create** option.</span></span> <span data-ttu-id="c0d09-429">Zadejte adresu URL k dispozici pro nový web a klikněte na tlačítko **vytvoření webu**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-429">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0d09-430">Web systému Windows Azure je hostitel pro spouštění v cloudu, ve kterém můžete řídit a spravovat webovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="c0d09-430">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="c0d09-431">Možnost rychle vytvořit můžete nasadit hotové webové aplikace na Windows Azure web z mimo portál.</span><span class="sxs-lookup"><span data-stu-id="c0d09-431">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="c0d09-432">Postup pro nastavení databáze neobsahuje.</span><span class="sxs-lookup"><span data-stu-id="c0d09-432">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="c0d09-433">![Vytvoření nového webu pomocí metody rychlého vytvoření](aspnet-mvc-4-models-and-data-access/_static/image33.png "vytváření nového webu pomocí metody rychlého vytvoření")</span><span class="sxs-lookup"><span data-stu-id="c0d09-433">![Creating a new Web Site using Quick Create](aspnet-mvc-4-models-and-data-access/_static/image33.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="c0d09-434">*Vytvoření nového webu pomocí metody rychlého vytvoření*</span><span class="sxs-lookup"><span data-stu-id="c0d09-434">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="c0d09-435">Počkejte, dokud nové **webu** je vytvořena.</span><span class="sxs-lookup"><span data-stu-id="c0d09-435">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="c0d09-436">Po vytvoření webu klikněte na odkaz v části **URL** sloupce.</span><span class="sxs-lookup"><span data-stu-id="c0d09-436">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="c0d09-437">Zkontrolujte, zda je funkční nový web.</span><span class="sxs-lookup"><span data-stu-id="c0d09-437">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="c0d09-438">![Procházení na nový web](aspnet-mvc-4-models-and-data-access/_static/image34.png "procházení na nový web")</span><span class="sxs-lookup"><span data-stu-id="c0d09-438">![Browsing to the new web site](aspnet-mvc-4-models-and-data-access/_static/image34.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="c0d09-439">*Procházení na nový web*</span><span class="sxs-lookup"><span data-stu-id="c0d09-439">*Browsing to the new web site*</span></span>

    <span data-ttu-id="c0d09-440">![Webový server spuštěn](aspnet-mvc-4-models-and-data-access/_static/image35.png "webu systémem")</span><span class="sxs-lookup"><span data-stu-id="c0d09-440">![Web site running](aspnet-mvc-4-models-and-data-access/_static/image35.png "Web site running")</span></span>

    <span data-ttu-id="c0d09-441">*Spuštění webu*</span><span class="sxs-lookup"><span data-stu-id="c0d09-441">*Web site running*</span></span>
6. <span data-ttu-id="c0d09-442">Přejděte zpět na portál a klikněte na název webu v části **název** sloupec pro zobrazení stránky pro správu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-442">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="c0d09-443">![Otevření stránky Správa webu](aspnet-mvc-4-models-and-data-access/_static/image36.png "otevření stránek správu webového serveru")</span><span class="sxs-lookup"><span data-stu-id="c0d09-443">![Opening the web site management pages](aspnet-mvc-4-models-and-data-access/_static/image36.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="c0d09-444">*Otevření stránek správu webového serveru*</span><span class="sxs-lookup"><span data-stu-id="c0d09-444">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="c0d09-445">V **řídicí panel** v části **rychlého přehledu** klikněte na položku **stažení profilu publikování** odkaz.</span><span class="sxs-lookup"><span data-stu-id="c0d09-445">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0d09-446">*Profilu publikování* obsahuje všechny informace požadované pro publikování webové aplikace na web služby Windows Azure pro každou metodu povoleno publikace.</span><span class="sxs-lookup"><span data-stu-id="c0d09-446">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="c0d09-447">Profil publikování obsahuje adresy URL, přihlašovací údaje uživatele a řetězců databází, které jsou potřebné k připojení k a ověřování na základě těchto koncových bodů, pro které je metoda publikace povolena.</span><span class="sxs-lookup"><span data-stu-id="c0d09-447">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="c0d09-448">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express pro Web** a **sadu Microsoft Visual Studio 2012** podporu čtení publikační profily k automatické konfiguraci těchto programů pro publikování webové aplikace na weby služby Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="c0d09-448">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="c0d09-449">![Na webu stažení profilu publikování](aspnet-mvc-4-models-and-data-access/_static/image37.png "stahování webové stránky profilu publikování")</span><span class="sxs-lookup"><span data-stu-id="c0d09-449">![Downloading the web site publish profile](aspnet-mvc-4-models-and-data-access/_static/image37.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="c0d09-450">*Na webu stažení profilu publikování*</span><span class="sxs-lookup"><span data-stu-id="c0d09-450">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="c0d09-451">Stáhněte si soubor profil publikování do vhodného umístění.</span><span class="sxs-lookup"><span data-stu-id="c0d09-451">Download the publish profile file to a known location.</span></span> <span data-ttu-id="c0d09-452">Dále v tomto cvičení uvidíte jak používat tento soubor k publikování webové aplikace na weby systému Windows Azure ze sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c0d09-452">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="c0d09-453">![Ukládání souboru profilu publikování](aspnet-mvc-4-models-and-data-access/_static/image38.png "ukládání profilu publikování")</span><span class="sxs-lookup"><span data-stu-id="c0d09-453">![Saving the publish profile file](aspnet-mvc-4-models-and-data-access/_static/image38.png "Saving the publish profile")</span></span>

    <span data-ttu-id="c0d09-454">*Ukládání souboru profilu publikování*</span><span class="sxs-lookup"><span data-stu-id="c0d09-454">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="c0d09-455">Úloha 2 – konfigurování serveru databáze</span><span class="sxs-lookup"><span data-stu-id="c0d09-455">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="c0d09-456">Pokud vaše aplikace využívá systému SQL Server, databáze, budete muset vytvořit databázi SQL server.</span><span class="sxs-lookup"><span data-stu-id="c0d09-456">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="c0d09-457">Pokud chcete nasadit jednoduchou aplikaci, která nepoužívá systém SQL Server může tuto úlohu přeskočit.</span><span class="sxs-lookup"><span data-stu-id="c0d09-457">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="c0d09-458">Budete potřebovat databázi SQL serveru pro ukládání databázi aplikace.</span><span class="sxs-lookup"><span data-stu-id="c0d09-458">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="c0d09-459">Databáze SQL servery můžete zobrazit ze svého předplatného na portál Windows Azure Management **databází Sql** | **servery** | **serveru Řídicí panel**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-459">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="c0d09-460">Pokud nemáte server vytvořeno, můžete vytvořit jeden pomocí **přidat** tlačítka na panelu příkazů.</span><span class="sxs-lookup"><span data-stu-id="c0d09-460">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="c0d09-461">Poznamenejte si **název serveru a adresa URL, správce přihlašovací jméno a heslo**, jako je použijete v další úkoly.</span><span class="sxs-lookup"><span data-stu-id="c0d09-461">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="c0d09-462">Nevytvářejte databáze ještě, jak bude vytvořen v pozdější fázi.</span><span class="sxs-lookup"><span data-stu-id="c0d09-462">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="c0d09-463">![Řídicí panel serveru databáze SQL](aspnet-mvc-4-models-and-data-access/_static/image39.png "řídicího panelu serveru databáze SQL")</span><span class="sxs-lookup"><span data-stu-id="c0d09-463">![SQL Database Server Dashboard](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="c0d09-464">*Řídicí panel serveru databáze SQL*</span><span class="sxs-lookup"><span data-stu-id="c0d09-464">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="c0d09-465">V dalším úkolem budete testovat připojení k databázi ze sady Visual Studio, proto je nutné zahrnout místní IP adresa serveru seznamu **povolené IP adresy**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-465">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="c0d09-466">To lze provést, klikněte na tlačítko **konfigurace**, vyberte IP adresu z **aktuální IP adresa klienta** a vkládání na **počáteční IP adresa** a **Koncová IP adresa** textová pole a kliknutím ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) tlačítko.</span><span class="sxs-lookup"><span data-stu-id="c0d09-466">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) button.</span></span>

    ![Přidávání IP adresy klienta](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    <span data-ttu-id="c0d09-468">*Přidávání IP adresy klienta*</span><span class="sxs-lookup"><span data-stu-id="c0d09-468">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="c0d09-469">Jednou **IP adresa klienta** je povolené IP adresy do seznamu, klikněte na **Uložit** potvrďte změny.</span><span class="sxs-lookup"><span data-stu-id="c0d09-469">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Potvrzení změn](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    <span data-ttu-id="c0d09-471">*Potvrzení změn*</span><span class="sxs-lookup"><span data-stu-id="c0d09-471">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="c0d09-472">Úloha 3 – publikování aplikace ASP.NET MVC 4 pomocí nástroje nasazení webu</span><span class="sxs-lookup"><span data-stu-id="c0d09-472">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="c0d09-473">Přejděte zpět na ASP.NET MVC 4 řešení.</span><span class="sxs-lookup"><span data-stu-id="c0d09-473">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="c0d09-474">V **Průzkumníku řešení**, klikněte pravým tlačítkem na webový projekt a vyberte **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-474">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="c0d09-475">![Publikování aplikace](aspnet-mvc-4-models-and-data-access/_static/image43.png "publikování aplikace")</span><span class="sxs-lookup"><span data-stu-id="c0d09-475">![Publishing the Application](aspnet-mvc-4-models-and-data-access/_static/image43.png "Publishing the Application")</span></span>

    <span data-ttu-id="c0d09-476">*Publikování webu*</span><span class="sxs-lookup"><span data-stu-id="c0d09-476">*Publishing the web site*</span></span>
2. <span data-ttu-id="c0d09-477">Umožňuje naimportujte profil publikování, který jste uložili v první úloze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-477">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="c0d09-478">![Import profilu publikování](aspnet-mvc-4-models-and-data-access/_static/image44.png "import profilu publikování")</span><span class="sxs-lookup"><span data-stu-id="c0d09-478">![Importing the publish profile](aspnet-mvc-4-models-and-data-access/_static/image44.png "Importing the publish profile")</span></span>

    <span data-ttu-id="c0d09-479">*Import profilu publikování*</span><span class="sxs-lookup"><span data-stu-id="c0d09-479">*Importing publish profile*</span></span>
3. <span data-ttu-id="c0d09-480">Klikněte na tlačítko **ověření připojení**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-480">Click **Validate Connection**.</span></span> <span data-ttu-id="c0d09-481">Po dokončení ověření klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-481">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0d09-482">Ověření je hotová, jakmile se zobrazí zelené zaškrtnutí zobrazí vedle tlačítko ověřit připojení.</span><span class="sxs-lookup"><span data-stu-id="c0d09-482">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="c0d09-483">![Ověření připojení](aspnet-mvc-4-models-and-data-access/_static/image45.png "ověřování připojení")</span><span class="sxs-lookup"><span data-stu-id="c0d09-483">![Validating connection](aspnet-mvc-4-models-and-data-access/_static/image45.png "Validating connection")</span></span>

    <span data-ttu-id="c0d09-484">*Ověření připojení*</span><span class="sxs-lookup"><span data-stu-id="c0d09-484">*Validating connection*</span></span>
4. <span data-ttu-id="c0d09-485">V **nastavení** v části **databáze** části, klikněte na tlačítko vedle připojení databáze textové pole (tj. **objekt DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="c0d09-485">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="c0d09-486">![Konfigurace nasazení webu](aspnet-mvc-4-models-and-data-access/_static/image46.png "konfigurace nasazení webu")</span><span class="sxs-lookup"><span data-stu-id="c0d09-486">![Web deploy configuration](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web deploy configuration")</span></span>

    <span data-ttu-id="c0d09-487">*Konfigurace nasazení webu*</span><span class="sxs-lookup"><span data-stu-id="c0d09-487">*Web deploy configuration*</span></span>
5. <span data-ttu-id="c0d09-488">Připojení k databázi nakonfigurujte následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="c0d09-488">Configure the database connection as follows:</span></span>

    - <span data-ttu-id="c0d09-489">V **název serveru** zadejte vaše databáze SQL serveru adresu URL pomocí *tcp:* předponu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-489">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
    - <span data-ttu-id="c0d09-490">V **uživatelské jméno** zadejte vaše přihlašovací jméno správce serveru.</span><span class="sxs-lookup"><span data-stu-id="c0d09-490">In **User name** type your server administrator login name.</span></span>
    - <span data-ttu-id="c0d09-491">V **heslo** zadejte přihlašovací heslo správce serveru.</span><span class="sxs-lookup"><span data-stu-id="c0d09-491">In **Password** type your server administrator login password.</span></span>
    - <span data-ttu-id="c0d09-492">Zadejte nový název databáze.</span><span class="sxs-lookup"><span data-stu-id="c0d09-492">Type a new database name.</span></span>

    <span data-ttu-id="c0d09-493">![Konfigurace cílový připojovací řetězec](aspnet-mvc-4-models-and-data-access/_static/image47.png "konfigurace cílový připojovací řetězec")</span><span class="sxs-lookup"><span data-stu-id="c0d09-493">![Configuring destination connection string](aspnet-mvc-4-models-and-data-access/_static/image47.png "Configuring destination connection string")</span></span>

    <span data-ttu-id="c0d09-494">*Konfigurace cílový připojovací řetězec*</span><span class="sxs-lookup"><span data-stu-id="c0d09-494">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="c0d09-495">Pak klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-495">Then click **OK**.</span></span> <span data-ttu-id="c0d09-496">Po zobrazení výzvy k vytvoření databáze, klikněte na tlačítko **Ano**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-496">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="c0d09-497">![Vytvoření databáze](aspnet-mvc-4-models-and-data-access/_static/image48.png "vytváření řetězec databáze")</span><span class="sxs-lookup"><span data-stu-id="c0d09-497">![Creating the database](aspnet-mvc-4-models-and-data-access/_static/image48.png "Creating the database string")</span></span>

    <span data-ttu-id="c0d09-498">*Vytvoření databáze*</span><span class="sxs-lookup"><span data-stu-id="c0d09-498">*Creating the database*</span></span>
7. <span data-ttu-id="c0d09-499">Připojovací řetězec, který budete používat pro připojení k databázi SQL v systému Windows Azure je uvedené v rámci textbox výchozí připojení.</span><span class="sxs-lookup"><span data-stu-id="c0d09-499">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="c0d09-500">Pak klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-500">Then click **Next**.</span></span>

    <span data-ttu-id="c0d09-501">![Připojovací řetězec odkazující na databázi SQL](aspnet-mvc-4-models-and-data-access/_static/image49.png "připojovací řetězec odkazující na databázi SQL")</span><span class="sxs-lookup"><span data-stu-id="c0d09-501">![Connection string pointing to SQL Database](aspnet-mvc-4-models-and-data-access/_static/image49.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="c0d09-502">*Připojovací řetězec odkazující na databázi SQL*</span><span class="sxs-lookup"><span data-stu-id="c0d09-502">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="c0d09-503">V **Preview** klikněte na tlačítko **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-503">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="c0d09-504">![Publikování webové aplikace](aspnet-mvc-4-models-and-data-access/_static/image50.png "publikování webové aplikace")</span><span class="sxs-lookup"><span data-stu-id="c0d09-504">![Publishing the web application](aspnet-mvc-4-models-and-data-access/_static/image50.png "Publishing the web application")</span></span>

    <span data-ttu-id="c0d09-505">*Publikování webové aplikace*</span><span class="sxs-lookup"><span data-stu-id="c0d09-505">*Publishing the web application*</span></span>
9. <span data-ttu-id="c0d09-506">Jakmile proces publikování dokončí, otevře se výchozí prohlížeč publikované webové stránky.</span><span class="sxs-lookup"><span data-stu-id="c0d09-506">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="c0d09-507">Příloha C: používání fragmentů kódu</span><span class="sxs-lookup"><span data-stu-id="c0d09-507">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="c0d09-508">S fragmenty kódu máte všechny kód, který je nutné na dosah ruky.</span><span class="sxs-lookup"><span data-stu-id="c0d09-508">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="c0d09-509">Dokument testovacího prostředí vás bude informovat přesně Pokud můžete, jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="c0d09-509">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="c0d09-510">![Používání fragmentů kódu v sadě Visual Studio pro vložení kódu do projektu](aspnet-mvc-4-models-and-data-access/_static/image51.png "fragmenty kódu pomocí sady Visual Studio pro vložení kódu do projektu")</span><span class="sxs-lookup"><span data-stu-id="c0d09-510">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-models-and-data-access/_static/image51.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="c0d09-511">*Používání fragmentů kódu v sadě Visual Studio pro vložení kódu do projektu*</span><span class="sxs-lookup"><span data-stu-id="c0d09-511">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="c0d09-512">***Chcete-li přidat fragment kódu pomocí klávesnice (C# pouze)***</span><span class="sxs-lookup"><span data-stu-id="c0d09-512">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="c0d09-513">Umístěte kurzor, kam chcete vložit kód.</span><span class="sxs-lookup"><span data-stu-id="c0d09-513">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="c0d09-514">Začněte psát název fragmentu kódu (bez mezery nebo spojovníky).</span><span class="sxs-lookup"><span data-stu-id="c0d09-514">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="c0d09-515">Podívejte se na jako IntelliSense zobrazí odpovídající fragmenty názvy.</span><span class="sxs-lookup"><span data-stu-id="c0d09-515">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="c0d09-516">Vyberte správný fragment kódu (nebo ponechte zadáním dokud je vybraný název celý fragmentu).</span><span class="sxs-lookup"><span data-stu-id="c0d09-516">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="c0d09-517">Stisknutím klávesy Tab dvakrát můžete vložit fragment v umístění kurzoru.</span><span class="sxs-lookup"><span data-stu-id="c0d09-517">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="c0d09-518">![Začněte psát název fragmentu](aspnet-mvc-4-models-and-data-access/_static/image52.png "začněte psát název fragmentu kódu")</span><span class="sxs-lookup"><span data-stu-id="c0d09-518">![Start typing the snippet name](aspnet-mvc-4-models-and-data-access/_static/image52.png "Start typing the snippet name")</span></span>

<span data-ttu-id="c0d09-519">*Začněte psát název fragmentu kódu*</span><span class="sxs-lookup"><span data-stu-id="c0d09-519">*Start typing the snippet name*</span></span>

<span data-ttu-id="c0d09-520">![Stisknutím klávesy Tab vyberte fragmentu zvýrazněná](aspnet-mvc-4-models-and-data-access/_static/image53.png "stisknutím klávesy Tab vyberte zvýrazněný fragmentu kódu")</span><span class="sxs-lookup"><span data-stu-id="c0d09-520">![Press Tab to select the highlighted snippet](aspnet-mvc-4-models-and-data-access/_static/image53.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="c0d09-521">*Stisknutím klávesy Tab vyberte zvýrazněný fragmentu kódu*</span><span class="sxs-lookup"><span data-stu-id="c0d09-521">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="c0d09-522">![Stisknutím klávesy Tab znovu a fragmentu rozšíří](aspnet-mvc-4-models-and-data-access/_static/image54.png "stisknutím klávesy Tab znovu a fragmentu bude rozšiřovat.")</span><span class="sxs-lookup"><span data-stu-id="c0d09-522">![Press Tab again and the snippet will expand](aspnet-mvc-4-models-and-data-access/_static/image54.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="c0d09-523">*Stisknutím klávesy Tab znovu a fragmentu bude rozšiřovat.*</span><span class="sxs-lookup"><span data-stu-id="c0d09-523">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="c0d09-524">***Chcete-li přidat fragment kódu pomocí myši (C#, Visual Basic a XML)*** 1.</span><span class="sxs-lookup"><span data-stu-id="c0d09-524">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="c0d09-525">Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="c0d09-525">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="c0d09-526">Vyberte **Vložit fragment** následuje **Moje fragmenty kódu**.</span><span class="sxs-lookup"><span data-stu-id="c0d09-526">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="c0d09-527">Vyberte relevantní fragment kódu ze seznamu, kliknutím na.</span><span class="sxs-lookup"><span data-stu-id="c0d09-527">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="c0d09-528">![Klikněte pravým tlačítkem, kam chcete vložit fragment kódu a vyberte Vložit fragment](aspnet-mvc-4-models-and-data-access/_static/image55.png "klikněte pravým tlačítkem, kam chcete vložit fragment kódu a vyberte Vložit fragment")</span><span class="sxs-lookup"><span data-stu-id="c0d09-528">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-models-and-data-access/_static/image55.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="c0d09-529">*Klikněte pravým tlačítkem myši, kam chcete vložit fragment kódu a vyberte Vložit fragment*</span><span class="sxs-lookup"><span data-stu-id="c0d09-529">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="c0d09-530">![Vyberte relevantní fragment kódu ze seznamu, kliknutím na](aspnet-mvc-4-models-and-data-access/_static/image56.png "vyberte relevantní fragment kódu ze seznamu, kliknutím na")</span><span class="sxs-lookup"><span data-stu-id="c0d09-530">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-models-and-data-access/_static/image56.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="c0d09-531">*Vyberte relevantní fragment kódu ze seznamu, kliknutím na*</span><span class="sxs-lookup"><span data-stu-id="c0d09-531">*Pick the relevant snippet from the list, by clicking on it*</span></span>