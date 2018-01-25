---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
title: "Vytváření rozložení stránek s zobrazit stránky předlohy (VB) | Microsoft Docs"
author: microsoft
description: "V tomto kurzu zjistěte, jak vytvořit běžné rozložení stránky pro více stránek v aplikaci a využívají k zobrazení stránky předlohy. Můžete použít..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/16/2008
ms.topic: article
ms.assetid: d34f90a1-6de3-482a-a326-f87fdcbaaaff
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 5466ea8a33bd2ccfe36c0f01b6b474bbb8d540a3
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/10/2017
---
<a name="creating-page-layouts-with-view-master-pages-vb"></a><span data-ttu-id="ada23-104">Vytváření rozložení stránek s zobrazit stránky předlohy (VB)</span><span class="sxs-lookup"><span data-stu-id="ada23-104">Creating Page Layouts with View Master Pages (VB)</span></span>
====================
<span data-ttu-id="ada23-105">podle [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ada23-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="ada23-106">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="ada23-106">Download PDF</span></span>](http://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_VB.pdf)

> <span data-ttu-id="ada23-107">V tomto kurzu zjistěte, jak vytvořit běžné rozložení stránky pro více stránek v aplikaci a využívají k zobrazení stránky předlohy.</span><span class="sxs-lookup"><span data-stu-id="ada23-107">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="ada23-108">Můžete zobrazit stránku předlohy, například definovat rozložení stránky dva sloupce a použití dvou sloupcích rozložení pro všechny stránky ve vaší webové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="ada23-108">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>


## <a name="creating-page-layouts-with-view-master-pages"></a><span data-ttu-id="ada23-109">Vytváření rozložení stránek s zobrazit stránky předlohy</span><span class="sxs-lookup"><span data-stu-id="ada23-109">Creating Page Layouts with View Master Pages</span></span>

<span data-ttu-id="ada23-110">V tomto kurzu zjistěte, jak vytvořit běžné rozložení stránky pro více stránek v aplikaci a využívají k zobrazení stránky předlohy.</span><span class="sxs-lookup"><span data-stu-id="ada23-110">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="ada23-111">Můžete zobrazit stránku předlohy, například definovat rozložení stránky dva sloupce a použití dvou sloupcích rozložení pro všechny stránky ve vaší webové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="ada23-111">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

<span data-ttu-id="ada23-112">Také můžete využít zobrazení stránky předlohy sdílet společný obsah na více stránkách v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="ada23-112">You also can take advantage of view master pages to share common content across multiple pages in your application.</span></span> <span data-ttu-id="ada23-113">Například můžete umístit vaše logo webu, navigačních odkazů a reklamy v zobrazení stránky předlohy.</span><span class="sxs-lookup"><span data-stu-id="ada23-113">For example, you can place your website logo, navigation links, and banner advertisements in a view master page.</span></span> <span data-ttu-id="ada23-114">Tímto způsobem každé stránky v aplikaci by zobrazit tento obsah automaticky.</span><span class="sxs-lookup"><span data-stu-id="ada23-114">That way, every page in your application would display this content automatically.</span></span>

<span data-ttu-id="ada23-115">V tomto kurzu zjistěte, jak vytvořit novou stránku předlohy zobrazení a vytvářet nové stránky obsahu zobrazení v závislosti na hlavní stránce.</span><span class="sxs-lookup"><span data-stu-id="ada23-115">In this tutorial, you learn how to create a new view master page and create a new view content page based on the master page.</span></span>

### <a name="creating-a-view-master-page"></a><span data-ttu-id="ada23-116">Vytvoření stránky hlavního zobrazení</span><span class="sxs-lookup"><span data-stu-id="ada23-116">Creating a View Master Page</span></span>

<span data-ttu-id="ada23-117">Začněme vytvořením zobrazení stránky předlohy, která definuje rozložení dvou sloupců.</span><span class="sxs-lookup"><span data-stu-id="ada23-117">Let's start by creating a view master page that defines a two-column layout.</span></span> <span data-ttu-id="ada23-118">Můžete přidat nové zobrazení stránku předlohy do projektu MVC kliknutím pravým tlačítkem na složku Views\Shared, výběrem možnosti nabídky **přidat, nové položky**a výběrem šablony stránky předlohy pro zobrazení MVC (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="ada23-118">You add a new view master page to an MVC project by right-clicking the Views\Shared folder, selecting the menu option **Add, New Item**, and selecting the  MVC View Master Page template (see Figure 1).</span></span>


<span data-ttu-id="ada23-119">[![Přidání stránky hlavního zobrazení](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ada23-119">[![Adding a view master page](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)</span></span>

<span data-ttu-id="ada23-120">**Obrázek 01**: Přidání stránky hlavního zobrazení ([Kliknutím zobrazit obrázek v plné velikosti](creating-page-layouts-with-view-master-pages-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="ada23-120">**Figure 01**: Adding a view master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-vb/_static/image3.png))</span></span>


<span data-ttu-id="ada23-121">Můžete vytvořit více než jednu stránku předlohy zobrazení v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="ada23-121">You can create more than one view master page in an application.</span></span> <span data-ttu-id="ada23-122">Každé zobrazení hlavní stránce můžete definovat různé stránky rozložení.</span><span class="sxs-lookup"><span data-stu-id="ada23-122">Each view master page can define a different page layout.</span></span> <span data-ttu-id="ada23-123">Můžete například určité stránky tak, aby měl rozložení dvou sloupců a dalších stránek tak, aby měl zobrazení tři sloupce.</span><span class="sxs-lookup"><span data-stu-id="ada23-123">For example, you might want certain pages to have a two-column layout and other pages to have a three-column layout.</span></span>

<span data-ttu-id="ada23-124">Hlavní stránka zobrazení vypadá hodně podobá standardní zobrazení ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="ada23-124">A view master page looks very much like a standard ASP.NET MVC view.</span></span> <span data-ttu-id="ada23-125">Ale na rozdíl od normální zobrazení stránky předlohy zobrazení obsahuje jeden nebo více `<asp:ContentPlaceHolder>` značky.</span><span class="sxs-lookup"><span data-stu-id="ada23-125">However, unlike a normal view, a view master page contains one or more `<asp:ContentPlaceHolder>` tags.</span></span> <span data-ttu-id="ada23-126">`<contentplaceholder>` Značky slouží k označení oblasti hlavní stránky, která mohou být přepsána nastaveními v jednotlivé stránky obsahu.</span><span class="sxs-lookup"><span data-stu-id="ada23-126">The `<contentplaceholder>` tags are used to mark the areas of the master page that can be overridden in an individual content page.</span></span>

<span data-ttu-id="ada23-127">Například stránky předlohy zobrazení v výpis 1 definuje rozložení dvou sloupců.</span><span class="sxs-lookup"><span data-stu-id="ada23-127">For example, the view master page in Listing 1 defines a two-column layout.</span></span> <span data-ttu-id="ada23-128">Obsahuje dva `<contentplaceholder>` značky.</span><span class="sxs-lookup"><span data-stu-id="ada23-128">It contains two `<contentplaceholder>` tags.</span></span> <span data-ttu-id="ada23-129">Jeden `<ContentPlaceHolder>` pro každý sloupec.</span><span class="sxs-lookup"><span data-stu-id="ada23-129">One `<ContentPlaceHolder>` for each column.</span></span>

<span data-ttu-id="ada23-130">**Výpis 1 –`Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="ada23-130">**Listing 1 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample1.aspx)]

<span data-ttu-id="ada23-131">Tělo zobrazení stránky předlohy v výpis 1 obsahuje dva `<div>` značky, které odpovídají dva sloupce.</span><span class="sxs-lookup"><span data-stu-id="ada23-131">The body of the view master page in Listing 1 contains two `<div>` tags that correspond to the two columns.</span></span> <span data-ttu-id="ada23-132">Třídy sloupec stylů CSS je použít pro obě `<div>` značky.</span><span class="sxs-lookup"><span data-stu-id="ada23-132">The Cascading Style Sheet column class is applied to both `<div>` tags.</span></span> <span data-ttu-id="ada23-133">Tato třída je definována v šabloně stylů deklarované v horní části stránky předlohy.</span><span class="sxs-lookup"><span data-stu-id="ada23-133">This class is defined in the style sheet declared at the top of the master page.</span></span> <span data-ttu-id="ada23-134">Můžete zobrazit náhled vykreslení stránky předlohy zobrazení přepnutím do zobrazení návrhu.</span><span class="sxs-lookup"><span data-stu-id="ada23-134">You can preview how the view master page will be rendered by switching to Design view.</span></span> <span data-ttu-id="ada23-135">Klikněte na kartu návrh v levém dolním rohu editoru zdrojového kódu (viz obrázek 2).</span><span class="sxs-lookup"><span data-stu-id="ada23-135">Click the Design tab at the bottom-left of the source code editor (see Figure 2).</span></span>


<span data-ttu-id="ada23-136">[![Zobrazení náhledu na hlavní stránce v Návrháři](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="ada23-136">[![Previewing a master page in the designer](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)</span></span>

<span data-ttu-id="ada23-137">**Obrázek 02**: zobrazení náhledu na hlavní stránce v Návrháři ([Kliknutím zobrazit obrázek v plné velikosti](creating-page-layouts-with-view-master-pages-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="ada23-137">**Figure 02**: Previewing a master page in the designer ([Click to view full-size image](creating-page-layouts-with-view-master-pages-vb/_static/image6.png))</span></span>


### <a name="creating-a-view-content-page"></a><span data-ttu-id="ada23-138">Vytvoření zobrazení stránky obsahu</span><span class="sxs-lookup"><span data-stu-id="ada23-138">Creating a View Content Page</span></span>

<span data-ttu-id="ada23-139">Po vytvoření zobrazení stránky předlohy, můžete vytvořit jeden nebo více zobrazení obsahu stránky v závislosti na hlavní stránku zobrazení.</span><span class="sxs-lookup"><span data-stu-id="ada23-139">After you create a view master page, you can create one or more view content pages based on the view master page.</span></span> <span data-ttu-id="ada23-140">Například můžete vytvořit Index zobrazení obsahu stránku pro řadič domovské kliknutím pravým tlačítkem na složku Views\Home, výběr **přidat, nové položky**, vyberete **obsah stránka zobrazení MVC** šablony, které zadáte Název Index.aspx a kliknutím na tlačítko Přidat tlačítko (viz obrázek 3).</span><span class="sxs-lookup"><span data-stu-id="ada23-140">For example, you can create an Index view content page for the Home controller by right-clicking the Views\Home folder, selecting **Add, New Item**, selecting the **MVC View Content Page** template, entering the name Index.aspx, and clicking the Add button (see Figure 3).</span></span>


<span data-ttu-id="ada23-141">[![Přidání zobrazení obsahu stránky](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="ada23-141">[![Adding a view content page](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)</span></span>

<span data-ttu-id="ada23-142">**Obrázek 03**: Přidání obsahu stránky zobrazení ([Kliknutím zobrazit obrázek v plné velikosti](creating-page-layouts-with-view-master-pages-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="ada23-142">**Figure 03**: Adding a view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-vb/_static/image9.png))</span></span>


<span data-ttu-id="ada23-143">Po kliknutí na tlačítko Přidat dialogové okno Nový zobrazí umožňující vyberte stránku předlohy zobrazení přidružených obsahu stránce zobrazení (viz obrázek 4).</span><span class="sxs-lookup"><span data-stu-id="ada23-143">After you click the Add button, a new dialog appears that enables you to select a view master page to associate with the view content page (see Figure 4).</span></span> <span data-ttu-id="ada23-144">Můžete přejít na stránku předlohy Site.master zobrazení, který jsme vytvořili v předchozí části.</span><span class="sxs-lookup"><span data-stu-id="ada23-144">You can navigate to the Site.master view master page that we created in the previous section.</span></span>


<span data-ttu-id="ada23-145">[![Vyberte stránku předlohy](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="ada23-145">[![Selecting a master page](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)</span></span>

<span data-ttu-id="ada23-146">**Obrázek 04**: Výběr stránky předlohy ([Kliknutím zobrazit obrázek v plné velikosti](creating-page-layouts-with-view-master-pages-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="ada23-146">**Figure 04**: Selecting a master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-vb/_static/image12.png))</span></span>


<span data-ttu-id="ada23-147">Po vytvoření nové stránky obsahu zobrazení v závislosti na hlavní stránce Site.master, můžete si stáhnout soubor v výpis 2.</span><span class="sxs-lookup"><span data-stu-id="ada23-147">After you create a new view content page based on the Site.master master page, you get the file in Listing 2.</span></span>

<span data-ttu-id="ada23-148">**Výpis 2 –`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="ada23-148">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample2.aspx)]

<span data-ttu-id="ada23-149">Všimněte si, že toto zobrazení obsahuje `<asp:Content>` značku, která odpovídá ke každému `<asp:ContentPlaceHolder>` značky v zobrazení stránky předlohy.</span><span class="sxs-lookup"><span data-stu-id="ada23-149">Notice that this view contains a `<asp:Content>` tag that corresponds to each of the `<asp:ContentPlaceHolder>` tags in the view master page.</span></span> <span data-ttu-id="ada23-150">Každý `<asp:Content>` značka zahrnuje ContentPlaceHolderID atribut, který odkazuje na konkrétní `<asp:ContentPlaceHolder>` , přepíše.</span><span class="sxs-lookup"><span data-stu-id="ada23-150">Each `<asp:Content>` tag includes a ContentPlaceHolderID attribute that points to the particular `<asp:ContentPlaceHolder>` that it overrides.</span></span>

<span data-ttu-id="ada23-151">Všimněte si kromě toho, že stránka zobrazení obsahu v výpis 2 neobsahuje žádná normální otevírání a HTML ukončovací značky.</span><span class="sxs-lookup"><span data-stu-id="ada23-151">Notice, furthermore, that the content view page in Listing 2 does not contain any of the normal opening and closing HTML tags.</span></span> <span data-ttu-id="ada23-152">Například neobsahuje otevření a zavření `<html>` nebo `<head>` značky.</span><span class="sxs-lookup"><span data-stu-id="ada23-152">For example, it does not contain the opening and closing `<html>` or `<head>` tags.</span></span> <span data-ttu-id="ada23-153">Všechny normální otevírání a ukončovací značky jsou obsažené v zobrazení stránky předlohy.</span><span class="sxs-lookup"><span data-stu-id="ada23-153">All of the normal opening and closing tags are contained in the view master page.</span></span>

<span data-ttu-id="ada23-154">Veškerý obsah, který chcete zobrazit v zobrazení stránky obsahu musí být umístěny v rámci `<asp:Content>` značky.</span><span class="sxs-lookup"><span data-stu-id="ada23-154">Any content that you want to display in a view content page must be placed within a `<asp:Content>` tag.</span></span> <span data-ttu-id="ada23-155">Pokud jste žádné HTML nebo další obsah i mimo tyto značky, pak bude dojde k chybě při pokusu o zobrazení stránky.</span><span class="sxs-lookup"><span data-stu-id="ada23-155">If you place any HTML or other content outside of these tags, then you will get an error when you attempt to view the page.</span></span>

<span data-ttu-id="ada23-156">Nemusíte přepsání každé `<asp:ContentPlaceHolder>` značky ze stránky předlohy na zobrazení obsahu stránce.</span><span class="sxs-lookup"><span data-stu-id="ada23-156">You don't need to override every `<asp:ContentPlaceHolder>` tag from a master page in a content view page.</span></span> <span data-ttu-id="ada23-157">Potřebujete přepsat `<asp:ContentPlaceHolder>` značky, pokud chcete nahradit konkrétní obsah značky.</span><span class="sxs-lookup"><span data-stu-id="ada23-157">You only need to override a `<asp:ContentPlaceHolder>` tag when you want to replace the tag with particular content.</span></span>

<span data-ttu-id="ada23-158">Například upravené zobrazení indexu v výpis 3 obsahuje pouze dva `<asp:Content>` značky.</span><span class="sxs-lookup"><span data-stu-id="ada23-158">For example, the modified Index view in Listing 3 contains only two `<asp:Content>` tags.</span></span> <span data-ttu-id="ada23-159">Každý z `<asp:Content>` značky zahrnuje nějaký text.</span><span class="sxs-lookup"><span data-stu-id="ada23-159">Each of the `<asp:Content>` tags includes some text.</span></span>

<span data-ttu-id="ada23-160">**Výpis 3 –`Views\Home\Index.aspx (modified)`**</span><span class="sxs-lookup"><span data-stu-id="ada23-160">**Listing 3 – `Views\Home\Index.aspx (modified)`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample3.aspx)]

<span data-ttu-id="ada23-161">Pokud se požaduje zobrazení v výpis 3, vykreslí stránku na obrázku 5.</span><span class="sxs-lookup"><span data-stu-id="ada23-161">When the view in Listing 3 is requested, it renders the page in Figure 5.</span></span> <span data-ttu-id="ada23-162">Všimněte si, že zobrazení vykreslí stránku s dva sloupce.</span><span class="sxs-lookup"><span data-stu-id="ada23-162">Notice that the view renders a page with two columns.</span></span> <span data-ttu-id="ada23-163">Všimněte si kromě toho, že obsah ze stránky obsahu zobrazení je sloučen s obsah ze stránky hlavního zobrazení.</span><span class="sxs-lookup"><span data-stu-id="ada23-163">Notice, furthermore, that the content from the view content page is merged with the content from the view master page.</span></span>


<span data-ttu-id="ada23-164">[![Index stránky zobrazení obsahu](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="ada23-164">[![The Index view content page](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)</span></span>

<span data-ttu-id="ada23-165">**Obrázek 05**: indexu zobrazení obsahu stránce ([Kliknutím zobrazit obrázek v plné velikosti](creating-page-layouts-with-view-master-pages-vb/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="ada23-165">**Figure 05**: The Index view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-vb/_static/image15.png))</span></span>


### <a name="modifying-view-master-page-content"></a><span data-ttu-id="ada23-166">Úprava obsahu stránky hlavního zobrazení</span><span class="sxs-lookup"><span data-stu-id="ada23-166">Modifying View Master Page Content</span></span>

<span data-ttu-id="ada23-167">Jedním z problémů, dojde k téměř okamžitě při práci s hlavní stránky zobrazení je problém úpravy zobrazení stránky předlohy obsahu, pokud jsou požadovány jiné zobrazení obsahu stránky.</span><span class="sxs-lookup"><span data-stu-id="ada23-167">One issue that you encounter almost immediately when working with view master pages is the problem of modifying view master page content when different view content pages are requested.</span></span> <span data-ttu-id="ada23-168">Například chcete každé stránce ve vaší webové aplikaci tak, aby měl jedinečný název.</span><span class="sxs-lookup"><span data-stu-id="ada23-168">For example, you want each page in your web application to have a unique title.</span></span> <span data-ttu-id="ada23-169">Název je však uvedená v zobrazení stránky předlohy a není v zobrazení stránky obsahu.</span><span class="sxs-lookup"><span data-stu-id="ada23-169">However, the title is declared in the view master page and not in the view content page.</span></span> <span data-ttu-id="ada23-170">Ano jak můžete přizpůsobit název stránky pro jednotlivé stránky zobrazení obsahu?</span><span class="sxs-lookup"><span data-stu-id="ada23-170">So, how do you customize the page title for each view content page?</span></span>

<span data-ttu-id="ada23-171">Existují dva způsoby, které lze upravit nadpis zobrazí při zobrazení stránky obsahu.</span><span class="sxs-lookup"><span data-stu-id="ada23-171">There are two ways that you can modify the title displayed by a view content page.</span></span> <span data-ttu-id="ada23-172">Nejprve je možné přiřadit název stránky do atribut title `<%@ page %>` – direktiva deklarované v horní části stránky obsahu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="ada23-172">First, you can assign a page title to the title attribute of the `<%@ page %>` directive declared at the top of a view content page.</span></span> <span data-ttu-id="ada23-173">Například pokud chcete přiřadit název stránky "Super skvělé webu" zobrazení Index, potom můžete zahrnout následující – direktiva v horní části zobrazení Index:</span><span class="sxs-lookup"><span data-stu-id="ada23-173">For example, if you want to assign the page title "Super Great Website" to the Index view, then you can include the following directive at the top of the Index view:</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample4.aspx)]

<span data-ttu-id="ada23-174">Když zobrazení indexu je vykresleno do prohlížeče, požadovaný název se zobrazí v záhlaví prohlížeče:</span><span class="sxs-lookup"><span data-stu-id="ada23-174">When the Index view is rendered to the browser, the desired title appears in the browser title bar:</span></span>


<span data-ttu-id="ada23-175">[![Záhlaví prohlížeče](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="ada23-175">[![Browser title bar](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)</span></span>


<span data-ttu-id="ada23-176">Neexistuje jeden důležité požadavek, který v pořadí pro atribut title fungovat, musí vyhovovat zobrazení stránky předlohy.</span><span class="sxs-lookup"><span data-stu-id="ada23-176">There is one important requirement that a master view page must satisfy in order for the title attribute to work.</span></span> <span data-ttu-id="ada23-177">Musí obsahovat zobrazení stránky předlohy `<head runat="server">` značky místo normální `<head>` značky pro jeho záhlaví.</span><span class="sxs-lookup"><span data-stu-id="ada23-177">The view master page must contain a `<head runat="server">` tag instead of a normal `<head>` tag for its header.</span></span> <span data-ttu-id="ada23-178">Pokud `<head>` značky nezahrnuje runat = "server" atribut pak název nezobrazí.</span><span class="sxs-lookup"><span data-stu-id="ada23-178">If the `<head>` tag does not include the runat="server" attribute then the title won't appear.</span></span> <span data-ttu-id="ada23-179">Výchozí zobrazení stránky předlohy zahrnuje požadované `<head runat="server">` značky.</span><span class="sxs-lookup"><span data-stu-id="ada23-179">The default view master page includes the required `<head runat="server">` tag.</span></span>

<span data-ttu-id="ada23-180">Alternativní způsob úpravy obsahu stránky předlohy ze stránky obsahu jednotlivých zobrazení je zabalit oblast, kterou chcete upravit v `<asp:ContentPlaceHolder>` značky.</span><span class="sxs-lookup"><span data-stu-id="ada23-180">An alternative approach to modifying master page content from an individual view content page is to wrap the region that you want to modify in a `<asp:ContentPlaceHolder>` tag.</span></span> <span data-ttu-id="ada23-181">Představte si například, že chcete změnit pouze název, ale také značky meta pro vykreslení zobrazení stránky předlohy.</span><span class="sxs-lookup"><span data-stu-id="ada23-181">For example, imagine that you want to change not only the title, but also the meta tags, rendered by a master view page.</span></span> <span data-ttu-id="ada23-182">Tato stránka předlohy výpis 4 obsahuje `<asp:ContentPlaceHolder>` označit jeho `<head>` značky.</span><span class="sxs-lookup"><span data-stu-id="ada23-182">The master view page in Listing 4 contains a `<asp:ContentPlaceHolder>` tag within its `<head>` tag.</span></span>

<span data-ttu-id="ada23-183">**Výpis 4 –`Views\Shared\Site2.master`**</span><span class="sxs-lookup"><span data-stu-id="ada23-183">**Listing 4 – `Views\Shared\Site2.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample5.aspx)]

<span data-ttu-id="ada23-184">Všimněte si, že `<asp:ContentPlaceHolder>` značku výpis 4 obsahuje výchozí obsah: výchozí název a výchozí značky meta.</span><span class="sxs-lookup"><span data-stu-id="ada23-184">Notice that the `<asp:ContentPlaceHolder>` tag in Listing 4 includes default content: a default title and default meta tags.</span></span> <span data-ttu-id="ada23-185">Pokud není toto přepsat `<asp:ContentPlaceHolder>` označení jednotlivých zobrazení obsahu stránce, pak se zobrazí výchozí obsah.</span><span class="sxs-lookup"><span data-stu-id="ada23-185">If you don't override this `<asp:ContentPlaceHolder>` tag in an individual view content page, then the default content will be displayed.</span></span>

<span data-ttu-id="ada23-186">Stránka zobrazení obsahu v výpis 5 přepíše `<asp:ContentPlaceHolder>` značky, aby bylo možné zobrazit vlastní název a vlastní značky meta.</span><span class="sxs-lookup"><span data-stu-id="ada23-186">The content view page in Listing 5 overrides the `<asp:ContentPlaceHolder>` tag in order to display a custom title and custom meta tags.</span></span>

<span data-ttu-id="ada23-187">**Výpis 5 –`Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="ada23-187">**Listing 5 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample6.aspx)]

### <a name="summary"></a><span data-ttu-id="ada23-188">Souhrn</span><span class="sxs-lookup"><span data-stu-id="ada23-188">Summary</span></span>

<span data-ttu-id="ada23-189">V tomto kurzu poskytl základní informace o zobrazit stránky předlohy a stránky obsahu.</span><span class="sxs-lookup"><span data-stu-id="ada23-189">This tutorial provided you with a basic introduction to view master pages and view content pages.</span></span> <span data-ttu-id="ada23-190">Jste zjistili, jak vytvořit nové zobrazení hlavní stránky a vytvářet zobrazení obsahu stránky na jejich základě.</span><span class="sxs-lookup"><span data-stu-id="ada23-190">You learned how to create new view master pages and create view content pages based on them.</span></span> <span data-ttu-id="ada23-191">Rovněž zkoumány, jak je možné upravit obsah zobrazení stránky předlohy z konkrétní zobrazení obsahu stránky.</span><span class="sxs-lookup"><span data-stu-id="ada23-191">We also examined how you can modify the content of a view master page from a particular view content page.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="ada23-192">[Předchozí](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
[další](passing-data-to-view-master-pages-vb.md)</span><span class="sxs-lookup"><span data-stu-id="ada23-192">[Previous](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
[Next](passing-data-to-view-master-pages-vb.md)</span></span>