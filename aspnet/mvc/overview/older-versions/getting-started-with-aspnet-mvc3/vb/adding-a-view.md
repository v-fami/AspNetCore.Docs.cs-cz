---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
title: "Přidání zobrazení (VB) | Microsoft Docs"
author: Rick-Anderson
description: "V tomto kurzu naučit se základy vytváření ASP.NET MVC webovou aplikaci pomocí Microsoft Visual Web Developer 2010 Express Service Pack 1, který je..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: d3633f64-5d3c-45c9-ae4b-cb1563e3739f
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: 7e8564c743510780b93d56bc1215f4c5b1faeb43
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/10/2017
---
<a name="adding-a-view-vb"></a><span data-ttu-id="5646d-103">Přidání zobrazení (VB)</span><span class="sxs-lookup"><span data-stu-id="5646d-103">Adding a View (VB)</span></span>
====================
<span data-ttu-id="5646d-104">Podle [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="5646d-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="5646d-105">V tomto kurzu naučit se základy vytváření ASP.NET MVC webovou aplikaci pomocí Microsoft Visual Web Developer 2010 Express Service Pack 1, který je bezplatnou verzi sady Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5646d-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="5646d-106">Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="5646d-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="5646d-107">Kliknutím na následující odkaz můžete nainstalovat všechny z nich: [instalačního programu webové platformy](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="5646d-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="5646d-108">Alternativně můžete nainstalovat jednotlivě požadavky pomocí následujících odkazů:</span><span class="sxs-lookup"><span data-stu-id="5646d-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="5646d-109">Visual Studio Web Developer Express SP1 požadavky</span><span class="sxs-lookup"><span data-stu-id="5646d-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="5646d-110">Aktualizace nástrojů rozhraní ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="5646d-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="5646d-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podporu runtime + nástroje)</span><span class="sxs-lookup"><span data-stu-id="5646d-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="5646d-112">Pokud používáte Visual Studio 2010 místo Visual Web Developer 2010, nainstalujte součásti kliknutím na následující odkaz: [požadavky sady Visual Studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="5646d-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="5646d-113">Projekt Visual Web Developer se VB.NET zdrojový kód je k dispozici v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="5646d-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="5646d-114">[Stáhnout verzi VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span><span class="sxs-lookup"><span data-stu-id="5646d-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="5646d-115">Pokud dáváte přednost C#, přepnout [C# verze](../cs/adding-a-view.md) tohoto kurzu.</span><span class="sxs-lookup"><span data-stu-id="5646d-115">If you prefer C#, switch to the [C# version](../cs/adding-a-view.md) of this tutorial.</span></span>


<span data-ttu-id="5646d-116">V této části vytvoříme upravit `HelloWorldController` třídu se má použít zobrazení souboru šablony do této aplikace zapouzdření proces generování odpovědi HTML pro klienta.</span><span class="sxs-lookup"><span data-stu-id="5646d-116">In this section we're going to modify the `HelloWorldController` class to use a view template file to cleanly encapsulate the process of generating HTML responses to a client.</span></span>

<span data-ttu-id="5646d-117">Začněme pomocí šablony zobrazení s `Index` metoda v `HelloWorldController` třídy.</span><span class="sxs-lookup"><span data-stu-id="5646d-117">Let's start by using a view template with the `Index` method in the `HelloWorldController` class.</span></span> <span data-ttu-id="5646d-118">Aktuálně `Index` metoda vrátí řetězec s zprávu, která je pevně zakódovaná v rámci třídy kontroleru.</span><span class="sxs-lookup"><span data-stu-id="5646d-118">Currently the `Index` method returns a string with a message that is hard-coded within the controller class.</span></span> <span data-ttu-id="5646d-119">Změna `Index` metoda vrátí `View` objektu, jak je znázorněno v následujícím:</span><span class="sxs-lookup"><span data-stu-id="5646d-119">Change the `Index` method to return a `View` object, as shown in the following:</span></span>

[!code-vb[Main](adding-a-view/samples/sample1.vb)]

<span data-ttu-id="5646d-120">Pojďme teď přidejte šablonu a zobrazení pro naše projekt, který jsme můžete volat pomocí `Index` metoda.</span><span class="sxs-lookup"><span data-stu-id="5646d-120">Let's now add a view template to our project that we can invoke with the `Index` method.</span></span> <span data-ttu-id="5646d-121">Chcete-li to provést, klikněte pravým tlačítkem uvnitř `Index` metoda a klikněte na tlačítko **přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="5646d-121">To do this, right-click inside the `Index` method and click **Add View**.</span></span>

<span data-ttu-id="5646d-122">[![IndexAddView](adding-a-view/_static/image2.png "IndexAddView")](adding-a-view/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5646d-122">[![IndexAddView](adding-a-view/_static/image2.png "IndexAddView")](adding-a-view/_static/image1.png)</span></span>

<span data-ttu-id="5646d-123">**Přidat zobrazení** zobrazí se dialogové okno.</span><span class="sxs-lookup"><span data-stu-id="5646d-123">The **Add View** dialog box appears.</span></span> <span data-ttu-id="5646d-124">Nechte výchozí položky a klikněte na **přidat** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="5646d-124">Leave the default entries and click the **Add** button.</span></span>

<span data-ttu-id="5646d-125">[![3addView](adding-a-view/_static/image4.png "3addView")](adding-a-view/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="5646d-125">[![3addView](adding-a-view/_static/image4.png "3addView")](adding-a-view/_static/image3.png)</span></span>

<span data-ttu-id="5646d-126">*MvcMovie\Views\HelloWorld* složky a *MvcMovie\Views\HelloWorld\Index.vbhtml* soubor se vytvoří.</span><span class="sxs-lookup"><span data-stu-id="5646d-126">The *MvcMovie\Views\HelloWorld* folder and the *MvcMovie\Views\HelloWorld\Index.vbhtml* file are created.</span></span> <span data-ttu-id="5646d-127">Zobrazí se jim v **Průzkumníku řešení**:</span><span class="sxs-lookup"><span data-stu-id="5646d-127">You can see them in **Solution Explorer**:</span></span>

<span data-ttu-id="5646d-128">[![SolnExpHelloWorldIndx](adding-a-view/_static/image6.png "SolnExpHelloWorldIndx")](adding-a-view/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="5646d-128">[![SolnExpHelloWorldIndx](adding-a-view/_static/image6.png "SolnExpHelloWorldIndx")](adding-a-view/_static/image5.png)</span></span>

<span data-ttu-id="5646d-129">Přidat kód HTML v části `<h2>` značky.</span><span class="sxs-lookup"><span data-stu-id="5646d-129">Add some HTML under the `<h2>` tag.</span></span> <span data-ttu-id="5646d-130">Upravenou *MvcMovie\Views\HelloWorld\Index.vbhtml* souboru je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="5646d-130">The modified *MvcMovie\Views\HelloWorld\Index.vbhtml* file is shown below.</span></span>

[!code-vbhtml[Main](adding-a-view/samples/sample2.vbhtml)]

<span data-ttu-id="5646d-131">Spusťte aplikaci a přejděte do &quot;hello, world&quot; řadiče (`http://localhost:xxxx/HelloWorld`).</span><span class="sxs-lookup"><span data-stu-id="5646d-131">Run the application and browse to the &quot;hello world&quot; controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="5646d-132">`Index` Metoda do kontroleru nebyla práci mnohem; jednoduše byl spuštěn příkaz `return View()`, který uvedené, že jsme chtěli použít soubor šablony zobrazení k vykreslení odpovědi klientovi.</span><span class="sxs-lookup"><span data-stu-id="5646d-132">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which indicated that we wanted to use a view template file to render a response to the client.</span></span> <span data-ttu-id="5646d-133">Protože jsme explicitně nezadali název souboru šablony zobrazení používat, ASP.NET MVC uvedena pomocí *Index.vbhtml* zobrazení souborů v rámci *\Views\HelloWorld* složky.</span><span class="sxs-lookup"><span data-stu-id="5646d-133">Because we did not explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.vbhtml* view file within the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="5646d-134">Následující obrázek ukazuje řetězec pevně v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5646d-134">The image below shows the string hard-coded in the view.</span></span>

<span data-ttu-id="5646d-135">[![3HelloWorld](adding-a-view/_static/image8.png "3HelloWorld")](adding-a-view/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="5646d-135">[![3HelloWorld](adding-a-view/_static/image8.png "3HelloWorld")](adding-a-view/_static/image7.png)</span></span>

<span data-ttu-id="5646d-136">Vypadá poměrně funkční.</span><span class="sxs-lookup"><span data-stu-id="5646d-136">Looks pretty good.</span></span> <span data-ttu-id="5646d-137">Všimněte si však, že v prohlížeči záhlaví říká &quot;Index&quot; a uvádí velký nadpis na stránce &quot;Moje aplikace MVC.&quot; Umožňuje změnit ty.</span><span class="sxs-lookup"><span data-stu-id="5646d-137">However, notice that the browser's title bar says &quot;Index&quot; and the big title on the page says &quot;My MVC Application.&quot; Let's change those.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="5646d-138">Změna zobrazení a rozložení stránky</span><span class="sxs-lookup"><span data-stu-id="5646d-138">Changing views and layout pages</span></span>

<span data-ttu-id="5646d-139">Nejprve změňte text &quot;Moje aplikace MVC.&quot; Tento text se sdílí a se zobrazí na každé stránce.</span><span class="sxs-lookup"><span data-stu-id="5646d-139">First, let's change the text &quot;My MVC Application.&quot; That text is shared and appears on every page.</span></span> <span data-ttu-id="5646d-140">Ve skutečnosti zobrazí se na jenom jednom místě v našem projektu, i když je na každé stránce v naší aplikaci.</span><span class="sxs-lookup"><span data-stu-id="5646d-140">It actually appears in only one place in our project, even though it's on every page in our application.</span></span> <span data-ttu-id="5646d-141">Přejděte na */zobrazení/sdílené* složky v **Průzkumníku řešení** a otevřete  *\_Layout.vbhtml* souboru.</span><span class="sxs-lookup"><span data-stu-id="5646d-141">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.vbhtml* file.</span></span> <span data-ttu-id="5646d-142">Tento soubor se nazývá ke stránce rozložení a je sdílený &quot;prostředí&quot; , všechny ostatní stránky použít.</span><span class="sxs-lookup"><span data-stu-id="5646d-142">This file is called a layout page and it's the shared &quot;shell&quot; that all other pages use.</span></span>

<span data-ttu-id="5646d-143">Poznámka: `@RenderBody()` řádek kódu v dolní části souboru.</span><span class="sxs-lookup"><span data-stu-id="5646d-143">Note the `@RenderBody()` line of code near the bottom of the file.</span></span> <span data-ttu-id="5646d-144">`RenderBody`slouží jako zástupný text, kde zobrazit všechny stránky, které vytvoříte, &quot;zabalené&quot; na stránce rozložení.</span><span class="sxs-lookup"><span data-stu-id="5646d-144">`RenderBody` is a placeholder where all the pages you create show up, &quot;wrapped&quot; in the layout page.</span></span> <span data-ttu-id="5646d-145">Změna `<h1>` nadpis z  **&quot;**  Moje aplikace MVC&quot; k &quot;filmová aplikace MVC&quot;.</span><span class="sxs-lookup"><span data-stu-id="5646d-145">Change the `<h1>` heading from **&quot;** My MVC Application&quot; to &quot;MVC Movie App&quot;.</span></span>

[!code-html[Main](adding-a-view/samples/sample3.html)]

<span data-ttu-id="5646d-146">Spusťte aplikaci a poznamenejte si teď uvádí &quot;filmová aplikace MVC&quot;.</span><span class="sxs-lookup"><span data-stu-id="5646d-146">Run the application and note it now says &quot;MVC Movie App&quot;.</span></span> <span data-ttu-id="5646d-147">Klikněte **o** odkaz a že stránka zobrazuje &quot;filmová aplikace MVC&quot;, příliš.</span><span class="sxs-lookup"><span data-stu-id="5646d-147">Click the **About** link, and that page shows &quot;MVC Movie App&quot;, too.</span></span>

<span data-ttu-id="5646d-148">Kompletní  *\_Layout.vbhtml* souboru jsou uvedeny níže:</span><span class="sxs-lookup"><span data-stu-id="5646d-148">The complete *\_Layout.vbhtml* file is shown below:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="5646d-149">Nyní změňte název stránky indexu (zobrazení).</span><span class="sxs-lookup"><span data-stu-id="5646d-149">Now, let's change the title of the Index page (view).</span></span>

[!code-vbhtml[Main](adding-a-view/samples/sample5.vbhtml)]

<span data-ttu-id="5646d-150">Otevřete *MvcMovie\Views\HelloWorld\Index.vbhtml*.</span><span class="sxs-lookup"><span data-stu-id="5646d-150">Open *MvcMovie\Views\HelloWorld\Index.vbhtml*.</span></span> <span data-ttu-id="5646d-151">Existují dvě místa změnit: nejdřív, zobrazí se text v názvu prohlížeče a pak v hlavičce sekundární ( `<h2>` element).</span><span class="sxs-lookup"><span data-stu-id="5646d-151">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="5646d-152">Vytočit je mírně lišit, abyste viděli, které bit kódu změní kterou částí aplikace.</span><span class="sxs-lookup"><span data-stu-id="5646d-152">We'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

<span data-ttu-id="5646d-153">Spusťte aplikaci a přejděte do`http://localhost:xx/HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="5646d-153">Run the application and browse to`http://localhost:xx/HelloWorld`.</span></span> <span data-ttu-id="5646d-154">Všimněte si, že došlo ke změně záhlaví prohlížeče, záhlaví primární a sekundární záhlaví.</span><span class="sxs-lookup"><span data-stu-id="5646d-154">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="5646d-155">Je snadné provést big změny ve vaší aplikaci s malým změnám zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5646d-155">It's easy to make big changes in your application with small changes to a view.</span></span> <span data-ttu-id="5646d-156">(Pokud nevidíte změny v prohlížeči, může být zobrazil obsah uložený v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="5646d-156">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="5646d-157">Stisknutím kláves Ctrl + F5 v prohlížeči na vynucení odpovědi ze serveru načíst.)</span><span class="sxs-lookup"><span data-stu-id="5646d-157">Press Ctrl+F5 in your browser to force the response from the server to be loaded.)</span></span>

<span data-ttu-id="5646d-158">[![3_MyMovieList](adding-a-view/_static/image10.png "3_MyMovieList")](adding-a-view/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="5646d-158">[![3_MyMovieList](adding-a-view/_static/image10.png "3_MyMovieList")](adding-a-view/_static/image9.png)</span></span>

<span data-ttu-id="5646d-159">Naše trocha &quot;data&quot; (v tomto případě &quot;Hello, World!&quot; zpráva) je pevně zakódovaná, přestože.</span><span class="sxs-lookup"><span data-stu-id="5646d-159">Our little bit of &quot;data&quot; (in this case the &quot;Hello World!&quot; message) is hard-coded, though.</span></span> <span data-ttu-id="5646d-160">Naše aplikace MVC má V (zobrazení) a My jsme C (řadiče), ale žádné M (modelu) ještě.</span><span class="sxs-lookup"><span data-stu-id="5646d-160">Our MVC application has V (views) and we've got C (controllers), but no M (model) yet.</span></span> <span data-ttu-id="5646d-161">Zanedlouho, provedeme procesem vytvoření databáze a načíst data modelu z něj.</span><span class="sxs-lookup"><span data-stu-id="5646d-161">Shortly, we'll walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="5646d-162">Předání dat z řadiče zobrazení</span><span class="sxs-lookup"><span data-stu-id="5646d-162">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="5646d-163">Před jsme přejděte k databázi a mluvit o modely, ale umožňuje nejprve mluvit o předání informací z řadiče zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5646d-163">Before we go to a database and talk about models, though, let's first talk about passing information from the Controller to a View.</span></span> <span data-ttu-id="5646d-164">Chceme předat šablonu zobrazení vyžaduje k vykreslení odpovědi HTML pro klienta.</span><span class="sxs-lookup"><span data-stu-id="5646d-164">We want to pass what a view template requires in order to render an HTML response to a client.</span></span> <span data-ttu-id="5646d-165">Tyto objekty se obvykle vytváří a předaná do zobrazení šablony třídy kontroleru a měly by obsahovat pouze data, která vyžaduje zobrazit šablonu – a žádné další.</span><span class="sxs-lookup"><span data-stu-id="5646d-165">These objects are typically created and passed by a controller class to a view template, and they should contain only the data that the view template requires — and no more.</span></span>

<span data-ttu-id="5646d-166">Dříve se `HelloWorldController` třídy, `Welcome` trvalo metody akce `name` a `numTimes` parametr a potom výstupní parametr hodnoty do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="5646d-166">Previously with the `HelloWorldController` class, the `Welcome` action method took a `name` and a `numTimes` parameter and then output the parameter values to the browser.</span></span> <span data-ttu-id="5646d-167">Spíše než mít řadič pokračovat k vykreslení této odpovědi přímo, místo toho jsme budete přidejme tato data v kontejner pro zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5646d-167">Rather than have the controller continue to render this response directly, let's instead we'll put that data in a bag for the View.</span></span> <span data-ttu-id="5646d-168">Kontrolery a zobrazení můžete použít `ViewBag` objekt pro uložení dat.</span><span class="sxs-lookup"><span data-stu-id="5646d-168">Controllers and Views can use a `ViewBag` object to hold that data.</span></span> <span data-ttu-id="5646d-169">Který se předává do šablony zobrazení automaticky a použije k vykreslení odpovědi HTML pomocí obsah kontejneru objektů a dat jako data.</span><span class="sxs-lookup"><span data-stu-id="5646d-169">That will be passed over to a view template automatically, and used to render the HTML response using the contents of the bag as data.</span></span> <span data-ttu-id="5646d-170">Tímto způsobem se týká jednou z věcí a zobrazení šablony s jiným řadičem – to nám umožňuje udržovat čistou &quot;oddělené oblasti zájmu&quot; v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="5646d-170">That way the controller is concerned with one thing and the view template with another — enabling us to maintain clean &quot;separation of concerns&quot; within the application.</span></span>

<span data-ttu-id="5646d-171">Alternativně jsme může definovat vlastní třídu, pak vytvoření instance tohoto objektu na vlastní, vyplňte v něm s daty a předejte ji do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5646d-171">Alternatively, we could define a custom class, then create an instance of that object on our own, fill it with data and pass it to the View.</span></span> <span data-ttu-id="5646d-172">ViewModel, který se často nazývá protože se jedná vlastní Model pro zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5646d-172">That is often called a ViewModel, because it's a custom Model for the View.</span></span> <span data-ttu-id="5646d-173">Pro malé množství dat ale objekt ViewBag vyhovující postup.</span><span class="sxs-lookup"><span data-stu-id="5646d-173">For small amounts of data, however, the ViewBag works great.</span></span>

<span data-ttu-id="5646d-174">Vraťte se do *HelloWorldController.vb* souboru změn `Welcome` metodu řadičem převést zprávu a NumTimes do objekt ViewBag.</span><span class="sxs-lookup"><span data-stu-id="5646d-174">Return to the *HelloWorldController.vb* file change the `Welcome` method inside the controller to put the Message and NumTimes into the ViewBag.</span></span> <span data-ttu-id="5646d-175">Objekt ViewBag je dynamický objekt.</span><span class="sxs-lookup"><span data-stu-id="5646d-175">The ViewBag is a dynamic object.</span></span> <span data-ttu-id="5646d-176">To znamená, že můžete dát všechno k němu.</span><span class="sxs-lookup"><span data-stu-id="5646d-176">That means you can put whatever you want in to it.</span></span> <span data-ttu-id="5646d-177">Objekt ViewBag nemá žádné definované vlastnosti, dokud vložíte něco uvnitř ho.</span><span class="sxs-lookup"><span data-stu-id="5646d-177">The ViewBag has no defined properties until you put something inside it.</span></span>

<span data-ttu-id="5646d-178">Kompletní `HelloWorldController.vb` s novou třídu ve stejném souboru.</span><span class="sxs-lookup"><span data-stu-id="5646d-178">The complete `HelloWorldController.vb` with the new class in the same file.</span></span>

[!code-vb[Main](adding-a-view/samples/sample6.vb)]

<span data-ttu-id="5646d-179">Naše ViewBag nyní obsahuje data, která se předá zobrazení automaticky.</span><span class="sxs-lookup"><span data-stu-id="5646d-179">Now our ViewBag contains data that will be passed over to the View automatically.</span></span> <span data-ttu-id="5646d-180">Opakujte případně jsme může mít předaná vlastní objekt takto Pokud jsme líbilo:</span><span class="sxs-lookup"><span data-stu-id="5646d-180">Again, alternatively we could have passed in our own object like this if we liked:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

<span data-ttu-id="5646d-181">Nyní potřebujeme `WelcomeView` šablony!</span><span class="sxs-lookup"><span data-stu-id="5646d-181">Now we need a `WelcomeView` template!</span></span> <span data-ttu-id="5646d-182">Spuštění aplikace, takže kompiluje nový kód.</span><span class="sxs-lookup"><span data-stu-id="5646d-182">Run the application so the new code is compiled.</span></span> <span data-ttu-id="5646d-183">Zavřete prohlížeč, klepněte pravým tlačítkem myši `Welcome` metoda a pak klikněte na tlačítko **přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="5646d-183">Close the browser, right-click inside the `Welcome` method, and then click **Add View**.</span></span>

<span data-ttu-id="5646d-184">Tady je co vaše **přidat zobrazení** dialogové okno bude vypadat takto.</span><span class="sxs-lookup"><span data-stu-id="5646d-184">Here's what your **Add View** dialog box looks like.</span></span>

<span data-ttu-id="5646d-185">[![3AddWelcomeView](adding-a-view/_static/image12.png "3AddWelcomeView")](adding-a-view/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="5646d-185">[![3AddWelcomeView](adding-a-view/_static/image12.png "3AddWelcomeView")](adding-a-view/_static/image11.png)</span></span>

<span data-ttu-id="5646d-186">Přidejte následující kód pod `<h2>` element v novém *úvodní.* vbhtml soubor.</span><span class="sxs-lookup"><span data-stu-id="5646d-186">Add the following code under the `<h2>` element in the new *Welcome.*vbhtml file.</span></span> <span data-ttu-id="5646d-187">Jsme budete zkontrolujte smyčku a vyslovte &quot;Hello&quot; tolikrát, kolikrát uživatel zvolí jsme měli!</span><span class="sxs-lookup"><span data-stu-id="5646d-187">We'll make a loop and say &quot;Hello&quot; as many times as the user says we should!</span></span>

[!code-vbhtml[Main](adding-a-view/samples/sample8.vbhtml)]

<span data-ttu-id="5646d-188">Spusťte aplikaci a přejděte do`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`</span><span class="sxs-lookup"><span data-stu-id="5646d-188">Run the application and browse to `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`</span></span>

<span data-ttu-id="5646d-189">Data se nyní prováděné z adresy URL a automaticky předaný kontroleru.</span><span class="sxs-lookup"><span data-stu-id="5646d-189">Now data is taken from the URL and passed to the controller automatically.</span></span> <span data-ttu-id="5646d-190">Řadičem zabalí dat do `Model` objekt a předává, které objektu do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="5646d-190">The controller packages up the data into a `Model` object and passes that object to the view.</span></span> <span data-ttu-id="5646d-191">Zobrazení, než se zobrazí data jako kód HTML pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="5646d-191">The view than displays the data as HTML to the user.</span></span>

<span data-ttu-id="5646d-192">[![3Hello_Scott_4](adding-a-view/_static/image14.png "3Hello_Scott_4")](adding-a-view/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="5646d-192">[![3Hello_Scott_4](adding-a-view/_static/image14.png "3Hello_Scott_4")](adding-a-view/_static/image13.png)</span></span>

<span data-ttu-id="5646d-193">Také, který byl typ služby &quot;M&quot; modelu, ale není typ databáze.</span><span class="sxs-lookup"><span data-stu-id="5646d-193">Well, that was a kind of an &quot;M&quot; for model, but not the database kind.</span></span> <span data-ttu-id="5646d-194">Podívejme se, co jsme jste se naučili a vytvořit databázi filmy.</span><span class="sxs-lookup"><span data-stu-id="5646d-194">Let's take what we've learned and create a database of movies.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="5646d-195">[Předchozí](adding-a-controller.md)
[další](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="5646d-195">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>