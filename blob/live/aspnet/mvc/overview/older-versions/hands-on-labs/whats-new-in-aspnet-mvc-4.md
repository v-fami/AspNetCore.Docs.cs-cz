---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: "Co je nového v architektuře ASP.NET MVC 4 | Microsoft Docs"
author: rick-anderson
description: "ASP.NET MVC 4 je rozhraní pro vytváření škálovatelných standardy webových aplikací pomocí vzory zavedené návrhu a výkonu technologie ASP.NET a..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 3de952224e23eed29f90ed0e8c662e4ee3f531ce
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/10/2017
---
<a name="whats-new-in-aspnet-mvc-4"></a><span data-ttu-id="0bf25-103">Co je nového v architektuře ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="0bf25-103">What's New in ASP.NET MVC 4</span></span>
====================
<span data-ttu-id="0bf25-104">podle [webové táborech Team](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="0bf25-104">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="0bf25-105">Stažení webové táborech cvičení Kit</span><span class="sxs-lookup"><span data-stu-id="0bf25-105">Download Web Camps Training Kit</span></span>](http://www.microsoft.com/en-us/download/29843)

> <span data-ttu-id="0bf25-106">ASP.NET MVC 4 je rozhraní pro vytváření škálovatelných standardy webových aplikací pomocí vzory zavedené návrhu a výkonu technologie ASP.NET a rozhraní .NET framework.</span><span class="sxs-lookup"><span data-stu-id="0bf25-106">ASP.NET MVC 4 is a framework for building scalable, standards-based web applications using well-established design patterns and the power of the ASP.NET and the .NET framework.</span></span> <span data-ttu-id="0bf25-107">Tento nový, čtvrté verzi rozhraní framework se zaměřuje na snadněji vývoj mobilních webových aplikací.</span><span class="sxs-lookup"><span data-stu-id="0bf25-107">This new, fourth version of the framework focuses on making mobile web application development easier.</span></span>
> 
> <span data-ttu-id="0bf25-108">Pokud vytvoříte nový projekt ASP.NET MVC 4 je nyní šablona projektu mobilních aplikací, které můžete použít k vytvoření samostatné aplikace speciálně pro mobilní zařízení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-108">To begin with, when you create a new ASP.NET MVC 4 project there is now a mobile application project template you can use to build a standalone app specifically for mobile devices.</span></span> <span data-ttu-id="0bf25-109">Kromě toho ASP.NET MVC 4 se integruje s jQuery Mobile prostřednictvím balíčku NuGet jQuery.Mobile.MVC.</span><span class="sxs-lookup"><span data-stu-id="0bf25-109">Additionally, ASP.NET MVC 4 integrates with jQuery Mobile through a jQuery.Mobile.MVC NuGet package.</span></span> <span data-ttu-id="0bf25-110">jQuery Mobile je základě HTML5 rozhraní pro vývoj webových aplikací, které jsou kompatibilní s všechny platformy oblíbených mobilních zařízení, včetně Windows Phone, iPhone, Android a tak dále.</span><span class="sxs-lookup"><span data-stu-id="0bf25-110">jQuery Mobile is an HTML5-based framework for developing web apps that are compatible with all popular mobile device platforms, including Windows Phone, iPhone, Android and so on.</span></span> <span data-ttu-id="0bf25-111">Ale pokud budete potřebovat specializace, ASP.NET MVC 4 také umožňuje obsluhovat různá zobrazení pro různá zařízení a poskytovat optimalizace pro konkrétní zařízení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-111">However, if you need specialization, ASP.NET MVC 4 also enables you to serve different views for different devices and provide device-specific optimizations.</span></span>
> 
> <span data-ttu-id="0bf25-112">V tomto testovacím prostředí praktických se spustí s ASP.NET MVC 4 &quot;Internetové aplikace&quot; šablona projektu pro vytvoření aplikace Fotogalerie.</span><span class="sxs-lookup"><span data-stu-id="0bf25-112">In this hands-on lab, you will start with the ASP.NET MVC 4 &quot;Internet Application&quot; project template to create a Photo Gallery application.</span></span> <span data-ttu-id="0bf25-113">Progresivně se zlepšila aplikace pomocí jQuery Mobile a nové funkce ASP.NET MVC 4, aby byl kompatibilní s různých mobilních zařízení a klientů webových prohlížečů.</span><span class="sxs-lookup"><span data-stu-id="0bf25-113">You will progressively enhance the app using jQuery Mobile and ASP.NET MVC 4's new features to make it compatible with different mobile devices and desktop web browsers.</span></span> <span data-ttu-id="0bf25-114">Naučíte se také o nový kód recepty pro generování kódu a jak ASP.NET MVC 4 usnadňuje psaní metody asynchronní akce díky podpoře úloh&lt;ActionResult&gt; návratové typy.</span><span class="sxs-lookup"><span data-stu-id="0bf25-114">You will also learn about new code recipes for code generation and how ASP.NET MVC 4 makes it easier for you to write asynchronous action methods by supporting Task&lt;ActionResult&gt; return types.</span></span>
> 
> <span data-ttu-id="0bf25-115">Všechny ukázky kódu a fragmenty kódu jsou součástí webové táborech školení sady, k dispozici na [https://www.microsoft.com/en-us/download/29843](https://www.microsoft.com/en-us/download/29843).</span><span class="sxs-lookup"><span data-stu-id="0bf25-115">All sample code and snippets are included in the Web Camps Training Kit, available at [https://www.microsoft.com/en-us/download/29843](https://www.microsoft.com/en-us/download/29843).</span></span>


<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="0bf25-116">Cíle</span><span class="sxs-lookup"><span data-stu-id="0bf25-116">Objectives</span></span>

<span data-ttu-id="0bf25-117">V tomto testovacím prostředí praktických se dozvíte, jak:</span><span class="sxs-lookup"><span data-stu-id="0bf25-117">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="0bf25-118">Využívat výhod rozšíření, která chcete šablony včetně projektu ASP.NET MVC šabloně nový projekt mobilních aplikací</span><span class="sxs-lookup"><span data-stu-id="0bf25-118">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="0bf25-119">Pomocí zobrazení atributů jazyka HTML5 a dotazy na média šablon stylů CSS ke zlepšení zobrazení na mobilních zařízeních</span><span class="sxs-lookup"><span data-stu-id="0bf25-119">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="0bf25-120">Pro progresivní vylepšení a vytváření dotykovým webového uživatelského rozhraní použijte jQuery Mobile</span><span class="sxs-lookup"><span data-stu-id="0bf25-120">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="0bf25-121">Vytvoření mobilní konkrétní zobrazení</span><span class="sxs-lookup"><span data-stu-id="0bf25-121">Create mobile-specific views</span></span>
- <span data-ttu-id="0bf25-122">Používání komponent přepínači zobrazení lze přepínat mezi mobilních a desktopových zobrazení v aplikaci</span><span class="sxs-lookup"><span data-stu-id="0bf25-122">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="0bf25-123">Vytvořte asynchronní řadičů pomocí úloh podpory</span><span class="sxs-lookup"><span data-stu-id="0bf25-123">Create asynchronous controllers using task support</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="0bf25-124">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0bf25-124">Prerequisites</span></span>

<span data-ttu-id="0bf25-125">Musíte mít následující položky k dokončení tohoto testovacího prostředí:</span><span class="sxs-lookup"><span data-stu-id="0bf25-125">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="0bf25-126">[Microsoft Visual Studio Express 2012 pro Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) nebo i vyšší (čtení [příloha B](#AppendixB) pokyny o tom, jak ji nainstalovat).</span><span class="sxs-lookup"><span data-stu-id="0bf25-126">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix B](#AppendixB) for instructions on how to install it).</span></span>
- <span data-ttu-id="0bf25-127">[ASP.NET MVC 4](../../../mvc4.md) (zahrnutá v instalaci sady Microsoft Visual Studio 2012)</span><span class="sxs-lookup"><span data-stu-id="0bf25-127">[ASP.NET MVC 4](../../../mvc4.md) (included in the Microsoft Visual Studio 2012 installation)</span></span>
- <span data-ttu-id="0bf25-128">Emulátor Windows Phone (součástí [Windows Phone 7.1.1 SDK](https://www.microsoft.com/en-us/download/details.aspx?id=29233))</span><span class="sxs-lookup"><span data-stu-id="0bf25-128">Windows Phone Emulator (included in the [Windows Phone 7.1.1 SDK](https://www.microsoft.com/en-us/download/details.aspx?id=29233))</span></span>
- <span data-ttu-id="0bf25-129">Volitelné - [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) s **Electric Plum iPhone simulátoru** rozšíření (pouze pro cvičení 3 umožňuje procházet webové aplikace s simulátor pro zařízení iPhone)</span><span class="sxs-lookup"><span data-stu-id="0bf25-129">Optional - [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) with **Electric Plum iPhone Simulator** extension (only for Exercise 3 used to browse the web application with an iPhone simulator)</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="0bf25-130">Instalace</span><span class="sxs-lookup"><span data-stu-id="0bf25-130">Setup</span></span>

<span data-ttu-id="0bf25-131">V dokumentu testovacího prostředí budete vyzváni k vložení bloky kódu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-131">Throughout the lab document, you will be instructed to insert code blocks.</span></span> <span data-ttu-id="0bf25-132">Pro usnadnění vaší práce většina tento kód je k dispozici jako Visual Studio fragmenty kódu, který můžete použít z Visual Studia abyste nemuseli přidat ručně.</span><span class="sxs-lookup"><span data-stu-id="0bf25-132">For your convenience, most of that code is provided as Visual Studio Code Snippets, which you can use from within Visual Studio to avoid having to add it manually.</span></span>

<span data-ttu-id="0bf25-133">Chcete-li nainstalovat fragmenty kódu:</span><span class="sxs-lookup"><span data-stu-id="0bf25-133">To install the code snippets:</span></span>

1. <span data-ttu-id="0bf25-134">Otevřete okno Průzkumníka Windows a přejděte do tohoto prostředí **Source\Setup** složky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-134">Open a Windows Explorer window and browse to the lab's **Source\Setup** folder.</span></span>
2. <span data-ttu-id="0bf25-135">Dvakrát klikněte **Setup.cmd** soubor v této složce pro instalaci fragmenty kódu sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0bf25-135">Double-click the **Setup.cmd** file in this folder to install the Visual Studio code snippets.</span></span>

<span data-ttu-id="0bf25-136">Pokud si nejste obeznámeni s fragmenty kódu Visual Studio a chcete se dozvíte, jak používat, můžete odkazovat na příloze z tohoto dokumentu &quot; [fragmenty kódu pomocí příloha A:](#AppendixA)&quot;.</span><span class="sxs-lookup"><span data-stu-id="0bf25-136">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix A: Using Code Snippets](#AppendixA)&quot;.</span></span>

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="0bf25-137">Cvičení</span><span class="sxs-lookup"><span data-stu-id="0bf25-137">Exercises</span></span>

<span data-ttu-id="0bf25-138">Toto praktické cvičení zahrnuje následující cvičení:</span><span class="sxs-lookup"><span data-stu-id="0bf25-138">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="0bf25-139">Nové šablony projektu ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="0bf25-139">New ASP.NET MVC 4 Project Templates</span></span>](#Exercise1)
2. [<span data-ttu-id="0bf25-140">Vytváření webové aplikace Fotogalerie</span><span class="sxs-lookup"><span data-stu-id="0bf25-140">Creating the Photo Gallery Web Application</span></span>](#Exercise2)
3. [<span data-ttu-id="0bf25-141">Přidání podpory pro mobilní zařízení</span><span class="sxs-lookup"><span data-stu-id="0bf25-141">Adding Support for Mobile Devices</span></span>](#Exercise3)
4. [<span data-ttu-id="0bf25-142">Použití asynchronní řadičů</span><span class="sxs-lookup"><span data-stu-id="0bf25-142">Using Asynchronous Controllers</span></span>](#Exercise4)

> [!NOTE]
> <span data-ttu-id="0bf25-143">Každý úkol je přiložena **End** složku obsahující výsledné řešení by si měly opatřit po dokončení cvičeních.</span><span class="sxs-lookup"><span data-stu-id="0bf25-143">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="0bf25-144">Toto řešení můžete použít jako vodítko, pokud potřebujete další pomoc při procházení cvičeních.</span><span class="sxs-lookup"><span data-stu-id="0bf25-144">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="0bf25-145">Odhadovaný čas dokončení tohoto testovacího prostředí: **60 minut**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-145">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a><span data-ttu-id="0bf25-146">Cvičení 1: Nové šablony projektu ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="0bf25-146">Exercise 1: New ASP.NET MVC 4 Project Templates</span></span>

<span data-ttu-id="0bf25-147">V tomto cvičení zaměříte vylepšení v šablonách projektu ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="0bf25-147">In this exercise, you will explore the enhancements in the ASP.NET MVC 4 Project templates.</span></span> <span data-ttu-id="0bf25-148">Kromě šabloně Internetové aplikace již existuje v MVC 3, tato verze nyní obsahuje samostatné šablonu pro mobilní aplikace.</span><span class="sxs-lookup"><span data-stu-id="0bf25-148">In addition to the Internet Application template, already present in MVC 3, this version now includes a separate template for Mobile applications.</span></span> <span data-ttu-id="0bf25-149">Nejprve bude vypadat v některé důležité funkce každé ze šablony.</span><span class="sxs-lookup"><span data-stu-id="0bf25-149">First, you will look at some relevant features of each of the templates.</span></span> <span data-ttu-id="0bf25-150">Pak bude fungovat na vykreslování stránku správně na různých platformách pomocí správný přístup.</span><span class="sxs-lookup"><span data-stu-id="0bf25-150">Then, you will work on rendering your page properly on the different platforms by using the right approach.</span></span>

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a><span data-ttu-id="0bf25-151">Úloha 1 – prohlížení Internetu šablona aplikací</span><span class="sxs-lookup"><span data-stu-id="0bf25-151">Task 1 - Exploring the Internet Application Template</span></span>

1. <span data-ttu-id="0bf25-152">Otevřete **sady Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-152">Open **Visual Studio**.</span></span>
2. <span data-ttu-id="0bf25-153">Vyberte **souboru | Nové | Projekt** příkazu nabídky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-153">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="0bf25-154">V **nový projekt** dialogovém okně, vyberte **Visual C# | Webové** šablony v levém podokně stromu a vyberte **webové aplikace ASP.NET MVC 4.**</span><span class="sxs-lookup"><span data-stu-id="0bf25-154">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="0bf25-155">Název projektu **Fotogalerie**, vyberte umístění (nebo ponechte výchozí nastavení) a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-155">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0bf25-156">Bude později upravit Fotogalerie ASP.NET MVC 4 řešení, které teď vytváříte.</span><span class="sxs-lookup"><span data-stu-id="0bf25-156">You will later customize the PhotoGallery ASP.NET MVC 4 solution you are now creating.</span></span>

    <span data-ttu-id="0bf25-157">![Vytvoření nového projektu](whats-new-in-aspnet-mvc-4/_static/image1.png "vytvoření nového projektu")</span><span class="sxs-lookup"><span data-stu-id="0bf25-157">![Creating a new project](whats-new-in-aspnet-mvc-4/_static/image1.png "Creating a new project")</span></span>

    <span data-ttu-id="0bf25-158">*Vytvoření nového projektu*</span><span class="sxs-lookup"><span data-stu-id="0bf25-158">*Creating a new project*</span></span>
3. <span data-ttu-id="0bf25-159">V **nový ASP.NET MVC 4 projekt** dialogovém okně, vyberte **Internetové aplikace** šablona projektu a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-159">In the **New ASP.NET MVC 4 Project** dialog, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="0bf25-160">Ujistěte se, že vyberete jako zobrazovací modul Razor.</span><span class="sxs-lookup"><span data-stu-id="0bf25-160">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="0bf25-161">![Vytvoření nové aplikace ASP.NET MVC 4 Internet](whats-new-in-aspnet-mvc-4/_static/image2.png "vytvoření nové aplikace ASP.NET MVC 4 Internetu")</span><span class="sxs-lookup"><span data-stu-id="0bf25-161">![Creating a new ASP.NET MVC 4 Internet Application](whats-new-in-aspnet-mvc-4/_static/image2.png "Creating a new ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="0bf25-162">*Vytvoření nové aplikace ASP.NET MVC 4 Internetu*</span><span class="sxs-lookup"><span data-stu-id="0bf25-162">*Creating a new ASP.NET MVC 4 Internet Application*</span></span>

    > [!NOTE]
    > <span data-ttu-id="0bf25-163">Syntaxe Razor byla zavedena v architektuře ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="0bf25-163">Razor syntax has been introduced in ASP.NET MVC 3.</span></span> <span data-ttu-id="0bf25-164">Jeho cílem je minimalizovat počet znaků a stisknutí kláves požadované v souboru, povolení fast a kapaliny kódování pracovního postupu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-164">Its goal is to minimize the number of characters and keystrokes required in a file, enabling a fast and fluid coding workflow.</span></span> <span data-ttu-id="0bf25-165">Syntaxe Razor využívá existující C# / VB (nebo jiných) znalosti jazyka a doručí syntaxi značek šablony, která umožňuje pracovním postupu vytváření Super HTML.</span><span class="sxs-lookup"><span data-stu-id="0bf25-165">Razor leverages existing C# / VB (or other) language skills and delivers a template markup syntax that enables an awesome HTML construction workflow.</span></span>
4. <span data-ttu-id="0bf25-166">Stiskněte klávesu **F5** a spuštění řešení obnoveného šablony.</span><span class="sxs-lookup"><span data-stu-id="0bf25-166">Press **F5** to run the solution and see the renewed templates.</span></span> <span data-ttu-id="0bf25-167">Můžete zkontrolovat na následující funkce:</span><span class="sxs-lookup"><span data-stu-id="0bf25-167">You can check out the following features:</span></span>

    <span data-ttu-id="0bf25-168">**Styl moderních šablony**</span><span class="sxs-lookup"><span data-stu-id="0bf25-168">**Modern-style templates**</span></span>

    <span data-ttu-id="0bf25-169">Byla obnovena šablony, poskytuje další styly moderních vyhledávání.</span><span class="sxs-lookup"><span data-stu-id="0bf25-169">The templates have been renewed, providing more modern-looking styles.</span></span>

    <span data-ttu-id="0bf25-170">![Šablony MVC ASP.NET 4 přepracován tak](whats-new-in-aspnet-mvc-4/_static/image3.png "přepracován tak šablony MVC 4")</span><span class="sxs-lookup"><span data-stu-id="0bf25-170">![ASP.NET MVC 4 restyled templates](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 restyled templates")</span></span>

    <span data-ttu-id="0bf25-171">*ASP.NET MVC 4 přepracován tak šablony*</span><span class="sxs-lookup"><span data-stu-id="0bf25-171">*ASP.NET MVC 4 restyled templates*</span></span>

    <span data-ttu-id="0bf25-172">![Nová stránka kontaktujte](whats-new-in-aspnet-mvc-4/_static/image4.png "nového kontaktu stránky")</span><span class="sxs-lookup"><span data-stu-id="0bf25-172">![New Contact page](whats-new-in-aspnet-mvc-4/_static/image4.png "New Contact page")</span></span>

    <span data-ttu-id="0bf25-173">*Nová stránka kontakt*</span><span class="sxs-lookup"><span data-stu-id="0bf25-173">*New Contact page*</span></span>

    <span data-ttu-id="0bf25-174">**Adaptivního vykreslování**</span><span class="sxs-lookup"><span data-stu-id="0bf25-174">**Adaptive Rendering**</span></span>

    <span data-ttu-id="0bf25-175">Podívejte se na změnu velikosti okna prohlížeče a Všimněte si, jak rozložení stránky dynamicky přizpůsobení novou velikost okna.</span><span class="sxs-lookup"><span data-stu-id="0bf25-175">Check out resizing the browser window and notice how the page layout dynamically adapts to the new window size.</span></span> <span data-ttu-id="0bf25-176">Tyto šablony pomocí technik adaptivního vykreslování stolní počítače a mobilní platformy bez nutnosti přizpůsobení řádně vykreslit.</span><span class="sxs-lookup"><span data-stu-id="0bf25-176">These templates use the adaptive rendering technique to render properly in both desktop and mobile platforms without any customization.</span></span>

    <span data-ttu-id="0bf25-177">![Šablona projektu ASP.NET MVC 4 v jiném prohlížeči velikosti](whats-new-in-aspnet-mvc-4/_static/image5.png "šablona projektu ASP.NET MVC 4 v jiném prohlížeči velikosti")</span><span class="sxs-lookup"><span data-stu-id="0bf25-177">![ASP.NET MVC 4 project template in different browser sizes](whats-new-in-aspnet-mvc-4/_static/image5.png "ASP.NET MVC 4 project template in different browser sizes")</span></span>

    <span data-ttu-id="0bf25-178">*Šablona projektu ASP.NET MVC 4 v jiném prohlížeči velikosti*</span><span class="sxs-lookup"><span data-stu-id="0bf25-178">*ASP.NET MVC 4 project template in different browser sizes*</span></span>

    <span data-ttu-id="0bf25-179">**Širší uživatelského rozhraní v jazyce JavaScript**</span><span class="sxs-lookup"><span data-stu-id="0bf25-179">**Richer UI with JavaScript**</span></span>

    <span data-ttu-id="0bf25-180">Další vylepšení výchozích šablon projektu je použití JavaScript zajistit více interaktivní JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0bf25-180">Another enhancement to default project templates is the use of JavaScript to provide a more interactive JavaScript.</span></span> <span data-ttu-id="0bf25-181">Přihlášení a registrace odkazy, které jsou použité v šabloně exemplify použití jQuery ověření k ověření vstupních polí z klienta.</span><span class="sxs-lookup"><span data-stu-id="0bf25-181">The Login and Register links used in the template exemplify how to use the jQuery Validations to validate the input fields from client-side.</span></span>

    ![jQuery ověření](whats-new-in-aspnet-mvc-4/_static/image6.png)

    <span data-ttu-id="0bf25-183">*jQuery ověření*</span><span class="sxs-lookup"><span data-stu-id="0bf25-183">*jQuery Validation*</span></span>

    > [!NOTE]
    > <span data-ttu-id="0bf25-184">Všimněte si, že dva protokolu v části v první části se můžou přihlásit pomocí účtu zaregistrovaný z webu a v druhé části můžete altenativelly přihlásit pomocí jiné služby ověřování, jako je google (zakázané ve výchozím nastavení).</span><span class="sxs-lookup"><span data-stu-id="0bf25-184">Notice the two log in sections, in the first section you can log in using a registerd account from the site and in the second section you can altenativelly log in using another authentication service like google (disabled by default).</span></span>
5. <span data-ttu-id="0bf25-185">Zavřete prohlížeč zastavení ladicího programu a vrátíte se k sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0bf25-185">Close the browser to stop the debugger and return to Visual Studio.</span></span>
6. <span data-ttu-id="0bf25-186">Otevřete soubor **AuthConfig.cs** umístěná **aplikace\_spustit** složky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-186">Open the file **AuthConfig.cs** located under the **App\_Start** folder.</span></span>
7. <span data-ttu-id="0bf25-187">Odebrat z posledního řádku registrace klienta Google pro komentář *OAuth* ověřování.</span><span class="sxs-lookup"><span data-stu-id="0bf25-187">Remove the comment from the last line to register Google client for *OAuth* authentication.</span></span>


    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

    > [!NOTE]
    > <span data-ttu-id="0bf25-188">Všimněte si, že můžete snadno povolit ověřování pomocí služby všechny OpenID nebo OAuth, jako je Facebook, Twitter, Microsoft atd.</span><span class="sxs-lookup"><span data-stu-id="0bf25-188">Notice you can easily enable authentication using any OpenID or OAuth service like Facebook, Twitter, Microsoft, etc.</span></span>
8. <span data-ttu-id="0bf25-189">Stiskněte klávesu **F5** spustíte řešení v a přejít na stránku přihlášení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-189">Press **F5** to run the solution and navigate to the login page.</span></span>
9. <span data-ttu-id="0bf25-190">Vyberte **Google** službu pro přihlášení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-190">Select **Google** service to log in.</span></span>

    ![Vyberte protokol ve službě](whats-new-in-aspnet-mvc-4/_static/image7.png)

    <span data-ttu-id="0bf25-192">*Vyberte protokol ve službě*</span><span class="sxs-lookup"><span data-stu-id="0bf25-192">*Selecting the log in service*</span></span>
10. <span data-ttu-id="0bf25-193">Přihlaste se pomocí účtu Google.</span><span class="sxs-lookup"><span data-stu-id="0bf25-193">Log in using your Google account.</span></span>
11. <span data-ttu-id="0bf25-194">Povolit web (localhost) za účelem načtení informací z účtu Google.</span><span class="sxs-lookup"><span data-stu-id="0bf25-194">Allow the site (localhost) to retrieve information from Google account.</span></span>
12. <span data-ttu-id="0bf25-195">Nakonec budete muset zaregistrovat v lokalitě za účelem přidružení účtu Google.</span><span class="sxs-lookup"><span data-stu-id="0bf25-195">Finally, you will have to register in the site to associate the Google account.</span></span>

    ![Přidružení účtu Google](whats-new-in-aspnet-mvc-4/_static/image8.png)

    <span data-ttu-id="0bf25-197">*Přidružení účtu Google*</span><span class="sxs-lookup"><span data-stu-id="0bf25-197">*Associating your Google account*</span></span>
13. <span data-ttu-id="0bf25-198">Zavřete prohlížeč zastavení ladicího programu a vrátíte se k sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0bf25-198">Close the browser to stop the debugger and return to Visual Studio.</span></span>
14. <span data-ttu-id="0bf25-199">Nyní prozkoumejte řešení podívejte se na některé další nové funkce, zavedená v šabloně projektu ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="0bf25-199">Now explore the solution to check out some other new features introduced by ASP.NET MVC 4 in the project template.</span></span>

    <span data-ttu-id="0bf25-200">![Šablona projektu ASP.NET MVC 4 Internet aplikace](whats-new-in-aspnet-mvc-4/_static/image9.png "šablona projektu ASP.NET MVC 4 Internetové aplikace")</span><span class="sxs-lookup"><span data-stu-id="0bf25-200">![The ASP.NET MVC 4 Internet Application Project Template](whats-new-in-aspnet-mvc-4/_static/image9.png "The ASP.NET MVC 4 Internet Application Project Template")</span></span>

    <span data-ttu-id="0bf25-201">*Šablona projektu ASP.NET MVC 4 Internetové aplikace*</span><span class="sxs-lookup"><span data-stu-id="0bf25-201">*The ASP.NET MVC 4 Internet Application Project Template*</span></span>

    - <span data-ttu-id="0bf25-202">**HTML 5 značek**</span><span class="sxs-lookup"><span data-stu-id="0bf25-202">**HTML 5 Markup**</span></span>

        <span data-ttu-id="0bf25-203">Procházejte šablony zobrazení a zjistěte, kód nový motiv.</span><span class="sxs-lookup"><span data-stu-id="0bf25-203">Browse template views to find out the new theme markup.</span></span>

        <span data-ttu-id="0bf25-204">![Nové šablony, pomocí syntaxe Razor a HTML5 značek About.cshtml. ] (whats-new-in-aspnet-mvc-4/_static/image10.png "Novou šablonu, pomocí syntaxe Razor a HTML5 značek About.cshtml.")</span><span class="sxs-lookup"><span data-stu-id="0bf25-204">![New template, using Razor and HTML5 markup About.cshtml.](whats-new-in-aspnet-mvc-4/_static/image10.png "New template, using Razor and HTML5 markup About.cshtml.")</span></span>

        <span data-ttu-id="0bf25-205">*Nové šablony, pomocí syntaxe Razor a HTML5 značek (About.cshtml).*</span><span class="sxs-lookup"><span data-stu-id="0bf25-205">*New template, using Razor and HTML5 markup (About.cshtml).*</span></span>
    - <span data-ttu-id="0bf25-206">**Aktualizované knihoven jazyka JavaScript**</span><span class="sxs-lookup"><span data-stu-id="0bf25-206">**Updated JavaScript libraries**</span></span>

        <span data-ttu-id="0bf25-207">Výchozí šablony ASP.NET MVC 4 nyní zahrnuje kódem KnockoutJS, rozhraní MVVM JavaScript rozhraní, které umožňuje vytvářet a vysoce přizpůsobivém webových aplikací pomocí jazyka JavaScript a HTML.</span><span class="sxs-lookup"><span data-stu-id="0bf25-207">The ASP.NET MVC 4 default template now includes KnockoutJS, a JavaScript MVVM framework that lets you create rich and highly responsive web applications using JavaScript and HTML.</span></span> <span data-ttu-id="0bf25-208">Jako v MVC3, jQuery a knihovny uživatelského rozhraní jQuery jsou také zahrnuté v architektuře ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="0bf25-208">Like in MVC3, jQuery and jQuery UI libraries are also included in ASP.NET MVC 4.</span></span>

        > [!NOTE]
        > <span data-ttu-id="0bf25-209">Můžete získat další informace o knihovně kódem KnockOutJS v tento odkaz: [ [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="0bf25-209">You can get more information about KnockOutJS library in this link: [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/).</span></span> <span data-ttu-id="0bf25-210">Kromě toho se dozvíte jQuery a kalendáře jQuery UI v [ [http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span><span class="sxs-lookup"><span data-stu-id="0bf25-210">Additionally, you can learn about jQuery and jQuery UI in [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).</span></span>

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a><span data-ttu-id="0bf25-211">Úloha 2 – prohlížení šablona mobilních aplikací</span><span class="sxs-lookup"><span data-stu-id="0bf25-211">Task 2 - Exploring the Mobile Application Template</span></span>

<span data-ttu-id="0bf25-212">ASP.NET MVC 4 usnadňuje vývoj webů pro mobilní a tablet prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="0bf25-212">ASP.NET MVC 4 facilitates the development of websites for mobile and tablet browsers.</span></span> <span data-ttu-id="0bf25-213">Tato šablona má stejnou strukturu aplikací jako šablonu internetovou aplikaci (Všimněte si, že kódu kontroleru je prakticky shodný), ale jeho styl byla změněna k vykreslení správně v mobilních zařízeních, na základě touch.</span><span class="sxs-lookup"><span data-stu-id="0bf25-213">This template has the same application structure as the Internet Application template (notice that the controller code is practically identical), but its style was modified to render properly in touch-based mobile devices.</span></span>

1. <span data-ttu-id="0bf25-214">Vyberte **souboru | Nové | Projekt** příkazu nabídky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-214">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="0bf25-215">V **nový projekt** dialogovém okně, vyberte **Visual C# | Webové** šablony v levém podokně stromu a vyberte **webové aplikace ASP.NET MVC 4.**</span><span class="sxs-lookup"><span data-stu-id="0bf25-215">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose the **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="0bf25-216">Název projektu **PhotoGallery.Mobile**, vyberte umístění (nebo ponechte výchozí nastavení), vyberte &quot;přidat do řešení&quot; a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-216">Name the project **PhotoGallery.Mobile**, select a location (or leave the default), select &quot;Add to solution&quot; and click **OK**.</span></span>
2. <span data-ttu-id="0bf25-217">V **nový ASP.NET MVC 4 projekt** dialogovém okně, vyberte **mobilní aplikace** šablona projektu a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-217">In the **New ASP.NET MVC 4 Project** dialog, select the **Mobile Application** project template and click **OK**.</span></span> <span data-ttu-id="0bf25-218">Ujistěte se, že vyberete jako zobrazovací modul Razor.</span><span class="sxs-lookup"><span data-stu-id="0bf25-218">Make sure you have selected Razor as the view engine.</span></span>

    <span data-ttu-id="0bf25-219">![Vytvoření nové aplikace ASP.NET MVC 4 Mobile](whats-new-in-aspnet-mvc-4/_static/image11.png "vytvoření nové aplikace ASP.NET MVC 4 Mobile")</span><span class="sxs-lookup"><span data-stu-id="0bf25-219">![Creating a new ASP.NET MVC 4 Mobile Application](whats-new-in-aspnet-mvc-4/_static/image11.png "Creating a new ASP.NET MVC 4 Mobile Application")</span></span>

    <span data-ttu-id="0bf25-220">*Vytvoření nové aplikace ASP.NET MVC 4 Mobile*</span><span class="sxs-lookup"><span data-stu-id="0bf25-220">*Creating a new ASP.NET MVC 4 Mobile Application*</span></span>
3. <span data-ttu-id="0bf25-221">Nyní budete moci zkoumat řešení a podívejte se na některé z nových funkcí zaváděné řešení šablony ASP.NET MVC 4 pro mobile:</span><span class="sxs-lookup"><span data-stu-id="0bf25-221">Now you are able to explore the solution and check out some of the new features introduced by the ASP.NET MVC 4 solution template for mobile:</span></span>

    - <span data-ttu-id="0bf25-222">**jQuery Mobile knihovny**</span><span class="sxs-lookup"><span data-stu-id="0bf25-222">**jQuery Mobile Library**</span></span>

        <span data-ttu-id="0bf25-223">Šablona projektu mobilní aplikace obsahuje mobilní knihovny jQuery, která je s otevřeným zdrojem knihovna pro kompatibilitu prohlížeč pro mobilní zařízení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-223">The Mobile Application project template includes the jQuery Mobile library, which is an open source library for mobile browser compatibility.</span></span> <span data-ttu-id="0bf25-224">jQuery Mobile platí postupném rozšiřování do mobilních prohlížečů, které podporují šablon stylů CSS a JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0bf25-224">jQuery Mobile applies progressive enhancement to mobile browsers that support CSS and JavaScript.</span></span> <span data-ttu-id="0bf25-225">Progresivní vylepšení umožňuje všechny prohlížeče zobrazíte základní obsah na webové stránce, zatímco umožňuje nejúčinnějších prohlížeče zobrazíte bohaté obsah.</span><span class="sxs-lookup"><span data-stu-id="0bf25-225">Progressive enhancement enables all browsers to display the basic content of a web page, while it only enables the most powerful browsers to display the rich content.</span></span> <span data-ttu-id="0bf25-226">Souborů JavaScript a CSS součástí jQuery mobilní styl, pomůže mobilní prohlížeče a přizpůsobit obsah na obrazovce bez provedení jakékoli změny v kódu stránky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-226">The JavaScript and CSS files, included in the jQuery Mobile style, help mobile browsers to fit the content in the screen without making any change in the page markup.</span></span>

        ![jQuery-mobile-library-included-in-the-template](whats-new-in-aspnet-mvc-4/_static/image12.png)

        <span data-ttu-id="0bf25-228">*mobilní knihovny jQuery zahrnuté v šabloně*</span><span class="sxs-lookup"><span data-stu-id="0bf25-228">*jQuery mobile library included in the template*</span></span>
    - <span data-ttu-id="0bf25-229">**HTML5 na základě značek**</span><span class="sxs-lookup"><span data-stu-id="0bf25-229">**HTML5 based markup**</span></span>

        ![Mobile-application-template-using-HTML5-markup](whats-new-in-aspnet-mvc-4/_static/image13.png)

        <span data-ttu-id="0bf25-231">*Šablona mobilních aplikací pomocí značek HTML5, (Login.cshtml a index.cshtml)*</span><span class="sxs-lookup"><span data-stu-id="0bf25-231">*Mobile application template using HTML5 markup, (Login.cshtml and index.cshtml)*</span></span>
4. <span data-ttu-id="0bf25-232">Stiskněte klávesu **F5** ke spuštění řešení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-232">Press **F5** to run the solution.</span></span>
5. <span data-ttu-id="0bf25-233">Otevřete **Windows Phone 7 emulátoru**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-233">Open the **Windows Phone 7 Emulator**.</span></span>
6. <span data-ttu-id="0bf25-234">Na obrazovce start phone otevřete Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="0bf25-234">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="0bf25-235">Podívejte se na adresu URL, kde plochy aplikaci spustit a přejděte na tuto adresu URL z telefonu (například `http://localhost:[PortNumber]/`).</span><span class="sxs-lookup"><span data-stu-id="0bf25-235">Check out the URL where the desktop application started and browse to that URL from the phone (e.g. `http://localhost:[PortNumber]/`).</span></span>
7. <span data-ttu-id="0bf25-236">Nyní budete moci zadat přihlašovací stránku nebo podívejte se na o stránce.</span><span class="sxs-lookup"><span data-stu-id="0bf25-236">Now you are able to enter the login page or check out the about page.</span></span> <span data-ttu-id="0bf25-237">Všimněte si, že styl webové stránky je založen na novou aplikaci Metro Mobile.</span><span class="sxs-lookup"><span data-stu-id="0bf25-237">Notice that the style of the website is based on the new Metro app for mobile.</span></span> <span data-ttu-id="0bf25-238">Šablona projektu ASP.NET MVC 4 je správně zobrazen na mobilních zařízeních, ujistěte se, že všechny prvky stránky jsou viditelné a povolené.</span><span class="sxs-lookup"><span data-stu-id="0bf25-238">The ASP.NET MVC 4 project template is correctly displayed on mobile devices, making sure all the elements of the page are visible and enabled.</span></span> <span data-ttu-id="0bf25-239">Všimněte si, že jsou odkazy na v hlavičce dost klikli nebo stisknuté.</span><span class="sxs-lookup"><span data-stu-id="0bf25-239">Notice that the links on the header are big enough to be clicked or tapped.</span></span>

    <span data-ttu-id="0bf25-240">![Projektu šablony stránky v mobilním zařízení](whats-new-in-aspnet-mvc-4/_static/image14.png "projektu šablony stránky v mobilních zařízení")</span><span class="sxs-lookup"><span data-stu-id="0bf25-240">![Project template pages in a mobile device](whats-new-in-aspnet-mvc-4/_static/image14.png "Project template pages in a mobile device")</span></span>

    <span data-ttu-id="0bf25-241">*Projekt šablony stránky v mobilních zařízení*</span><span class="sxs-lookup"><span data-stu-id="0bf25-241">*Project template pages in a mobile device*</span></span>
8. <span data-ttu-id="0bf25-242">Nová šablona používá také **zobrazení metaznačku**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-242">The new template also uses the **Viewport meta tag**.</span></span> <span data-ttu-id="0bf25-243">Většina mobilních prohlížečů definovat šířku pro okno virtuální prohlížeče nebo &quot;zobrazení&quot;, která je větší než skutečná šířka mobilního zařízení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-243">Most mobile browsers define a width for a virtual browser window or &quot;viewport&quot;, which is larger than the actual width of the mobile device.</span></span> <span data-ttu-id="0bf25-244">To umožňuje mobilní prohlížeče zobrazíte celou webovou stránku uvnitř virtuální zobrazení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-244">This enables mobile browsers to display the entire web page inside the virtual display.</span></span> <span data-ttu-id="0bf25-245">**Zobrazení metaznačku** umožňuje vývojářům webů nastavení šířky, výšky a škále oblasti prohlížeče na mobilních zařízeních **.**</span><span class="sxs-lookup"><span data-stu-id="0bf25-245">The **Viewport meta tag** allows web developers to set the width, height and scale of the browser area on mobile devices **.**</span></span> <span data-ttu-id="0bf25-246">Šablony ASP.NET MVC 4 pro mobilní aplikace nastaví zobrazení na šířku zařízení (&quot;šířka = šířkou zařízení&quot;) v šabloně rozložení (*Views\Shared\_Layout.cshtml*) tak, aby všechny stránky budou mít jejich zobrazení nastavena na šířku obrazovky zařízení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-246">The ASP.NET MVC 4 template for Mobile Applications sets the viewport to the device width (&quot;width=device-width&quot;) in the layout template (*Views\Shared\_Layout.cshtml*), so that all the pages will have their viewport set to the device screen width.</span></span> <span data-ttu-id="0bf25-247">Všimněte si, že zobrazení metaznačku nedojde ke změně zobrazení výchozí prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="0bf25-247">Notice that the Viewport meta tag will not change the default browser view.</span></span>
9. <span data-ttu-id="0bf25-248">Otevřete  **\_Layout.cshtml**, který je umístěn v **zobrazení | Sdílené** složky a komentář metaznačku zobrazení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-248">Open **\_Layout.cshtml**, located in the **Views | Shared** folder, and comment the Viewport meta tag.</span></span> <span data-ttu-id="0bf25-249">Spuštění aplikace, není-li již otevřít a podívejte se na rozdíly.</span><span class="sxs-lookup"><span data-stu-id="0bf25-249">Run the application, if not already opened, and check out the differences.</span></span>


    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

    <span data-ttu-id="0bf25-250">![Lokality po komentářů metaznačku zobrazení](whats-new-in-aspnet-mvc-4/_static/image15.png "lokality po komentářů metaznačku zobrazení")</span><span class="sxs-lookup"><span data-stu-id="0bf25-250">![The site after commenting the viewport meta tag](whats-new-in-aspnet-mvc-4/_static/image15.png "The site after commenting the viewport meta tag")</span></span>

    <span data-ttu-id="0bf25-251">*Lokality po komentářů metaznačku zobrazení*</span><span class="sxs-lookup"><span data-stu-id="0bf25-251">*The site after commenting the viewport meta tag*</span></span>
10. <span data-ttu-id="0bf25-252">V sadě Visual Studio, stiskněte klávesu **SHIFT** + **F5** Zastavit ladění aplikace.</span><span class="sxs-lookup"><span data-stu-id="0bf25-252">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
11. <span data-ttu-id="0bf25-253">Zrušením komentáře u metaznačku zobrazení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-253">Uncomment the viewport meta tag.</span></span>


    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a><span data-ttu-id="0bf25-254">Úloha 3 – pomocí adaptivního vykreslování</span><span class="sxs-lookup"><span data-stu-id="0bf25-254">Task 3 - Using Adaptive Rendering</span></span>

<span data-ttu-id="0bf25-255">V této úloze se dozvíte další metodou pro vykreslení stránky správně na mobilních zařízeních a webových prohlížečů ve stejnou dobu bez nutnosti přizpůsobení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-255">In this task, you will learn another method to render a Web page correctly on mobile devices and Web browsers at the same time without any customization.</span></span> <span data-ttu-id="0bf25-256">Už jste použili zobrazení metaznačku s podobným účelem.</span><span class="sxs-lookup"><span data-stu-id="0bf25-256">You have already used Viewport meta tag with a similar purpose.</span></span> <span data-ttu-id="0bf25-257">Nyní bude vyhovovat jinou efektivní metodu: *adaptivního vykreslování*.</span><span class="sxs-lookup"><span data-stu-id="0bf25-257">Now you will meet another powerful method: *adaptive rendering*.</span></span>

<span data-ttu-id="0bf25-258">Adaptivního vykreslování je technika, který používá **dotazy na média CSS3** Chcete-li přizpůsobit styl použitý na stránku.</span><span class="sxs-lookup"><span data-stu-id="0bf25-258">Adaptive rendering is a technique that uses **CSS3 media queries** to customize the style applied to a page.</span></span> <span data-ttu-id="0bf25-259">Dotazy na média zadejte podmínky uvnitř šablony stylů CSS styly za určité podmínky seskupení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-259">Media queries define conditions inside a style sheet, grouping CSS styles under a certain condition.</span></span> <span data-ttu-id="0bf25-260">Jenom v případě, že je podmínka pravdivá, styl se použije na deklarované objekty.</span><span class="sxs-lookup"><span data-stu-id="0bf25-260">Only when the condition is true, the style is applied to the declared objects.</span></span>

<span data-ttu-id="0bf25-261">Flexibilita poskytované adaptivního vykreslování technika umožňuje všechny vlastní nastavení pro zobrazení webu na různých zařízeních.</span><span class="sxs-lookup"><span data-stu-id="0bf25-261">The flexibility provided by the adaptive rendering technique enables any customization for displaying the site on different devices.</span></span> <span data-ttu-id="0bf25-262">Můžete definovat libovolný počet styly tak, jak chcete na jedinou šablonu stylů bez nutnosti psaní kódu logiku zvolit styl.</span><span class="sxs-lookup"><span data-stu-id="0bf25-262">You can define as many styles as you want on a single style sheet without writing logic code to choose the style.</span></span> <span data-ttu-id="0bf25-263">Proto je velmi úhledné způsob přizpůsobení stylů stránky, protože snižuje množství duplicitní kód a logiku pro vykreslování účely.</span><span class="sxs-lookup"><span data-stu-id="0bf25-263">Therefore, it is a very neat way of adapting page styles, as it reduces the amount of duplicated code and logic for rendering purposes.</span></span> <span data-ttu-id="0bf25-264">Na druhé straně byste zvýšit spotřeba šířky pásma, jak může málo zvětšit velikost souborů šablon stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="0bf25-264">On the other hand, bandwidth consumption would increase, as the size of your CSS files could grow marginally.</span></span>

<span data-ttu-id="0bf25-265">Pomocí adaptivního vykreslování techniku, bude web **zobrazí správně, bez ohledu na to, v prohlížeči.**</span><span class="sxs-lookup"><span data-stu-id="0bf25-265">By using the adaptive rendering technique, your site will be **displayed properly, regardless of the browser.**</span></span> <span data-ttu-id="0bf25-266">Ale byste měli zvážit, není vážný, pokud načíst navíc šířky pásma.</span><span class="sxs-lookup"><span data-stu-id="0bf25-266">However, you should consider if the bandwidth extra load is a concern.</span></span>

> [!NOTE]
> <span data-ttu-id="0bf25-267">Je základní formát media dotaz: @media \[oboru: všechny | kapesních | tisku | projekce | obrazovky\] ([vlastnost: hodnota] a... [vlastnost: hodnota])</span><span class="sxs-lookup"><span data-stu-id="0bf25-267">The basic format of a media query is: @media \[Scope: all | handheld | print | projection | screen\] ([property:value] and ... [property:value])</span></span>


<span data-ttu-id="0bf25-268">Příklady dotazů média: &gt;  **@media všechny a (max-width: 1000px) a (min-width: 700px) {}:** pro všechny rozlišení mezi 700px a 1000px.</span><span class="sxs-lookup"><span data-stu-id="0bf25-268">Examples of media queries: &gt;**@media all and (max-width: 1000px) and (min-width: 700px) {}:** For all the resolutions between 700px and 1000px.</span></span>

> <span data-ttu-id="0bf25-269">**@mediaobrazovky a (min-width: 400 px) a (max-width: 700px) {...}:** pouze pro obrazovky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-269">**@media screen and (min-width: 400px) and (max-width: 700px) { ... }:** Only for screens.</span></span> <span data-ttu-id="0bf25-270">Řešení musí být v rozsahu od 400 do 700px.</span><span class="sxs-lookup"><span data-stu-id="0bf25-270">The resolution must be between 400 and 700px.</span></span>
> 
> <span data-ttu-id="0bf25-271">**@mediakapesních a (min-width: 20em), obrazovky a (min-width: 20em) {...}:** kapesní zařízení (mobile a zařízení) a obrazovky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-271">**@media handheld and (min-width: 20em), screen and (min-width: 20em) { ... }:** For handhelds(mobile and devices) and screens.</span></span> <span data-ttu-id="0bf25-272">Minimální šířka musí být větší než 20em.</span><span class="sxs-lookup"><span data-stu-id="0bf25-272">The minimum width must be greater than 20em.</span></span>
> 
> <span data-ttu-id="0bf25-273">Další informace o tom najdete na [W3C lokality](http://www.w3.org/TR/css3-mediaqueries/).</span><span class="sxs-lookup"><span data-stu-id="0bf25-273">You can find more information about this on the [W3C site](http://www.w3.org/TR/css3-mediaqueries/).</span></span>


<span data-ttu-id="0bf25-274">Bude nyní prozkoumat, jak funguje adaptivního vykreslování, zlepšení čitelnosti ASP.NET MVC 4 výchozí šablony webové stránky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-274">You will now explore how the adaptive rendering works, improving the readability of the ASP.NET MVC 4 default website template.</span></span>

1. <span data-ttu-id="0bf25-275">Otevřete **PhotoGallery.sln** řešení, které jste vytvořili v úloze 1 a vyberte **Fotogalerie** projektu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-275">Open the **PhotoGallery.sln** solution you have created at Task 1 and select the **PhotoGallery** project.</span></span> <span data-ttu-id="0bf25-276">Stiskněte klávesu **F5** ke spuštění řešení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-276">Press **F5** to run the solution.</span></span>
2. <span data-ttu-id="0bf25-277">Změnit šířku prohlížeče, nastavení windows polovina nebo méně než čtvrtletí původní velikosti.</span><span class="sxs-lookup"><span data-stu-id="0bf25-277">Resize the browser's width, setting the windows to half or to less than a quarter of its original size.</span></span> <span data-ttu-id="0bf25-278">Všimněte si, co se stane s položkami v hlavičce: některé prvky se nezobrazí v oblasti viditelné hlavičky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-278">Notice what happens with the items in the header: Some elements will not appear in the visible area of the header.</span></span>
3. <span data-ttu-id="0bf25-279">Otevřete **Site.css** soubor v Průzkumníku řešení Visual Studio, umístěný v **obsahu** složce projektu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-279">Open **Site.css** file from the Visual Studio Solution explorer, located in **Content** project folder.</span></span> <span data-ttu-id="0bf25-280">Stiskněte klávesu **kombinaci kláves CTRL + F** otevřete Visual Studio integrované hledání a zapisovat  **@media**  najít **šablon stylů CSS media dotaz**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-280">Press **CTRL + F** to open Visual Studio integrated search, and write **@media** to locate the **CSS media query**.</span></span>

    <span data-ttu-id="0bf25-281">Tímto způsobem lze použít média dotazu podmínka, která je definována v této šabloně: když je velikost okna prohlížeče pod **850 px**, použita pravidla stylu CSS jsou ty, které jsou definované v tomto bloku média.</span><span class="sxs-lookup"><span data-stu-id="0bf25-281">The media query condition defined in this template works in this way: When the browser's window size is below **850 px**, the CSS rules applied are the ones defined inside this media block.</span></span>

    <span data-ttu-id="0bf25-282">![Vyhledání media dotaz](whats-new-in-aspnet-mvc-4/_static/image16.png "vyhledání media dotaz")</span><span class="sxs-lookup"><span data-stu-id="0bf25-282">![Locating the media query](whats-new-in-aspnet-mvc-4/_static/image16.png "Locating the media query")</span></span>

    <span data-ttu-id="0bf25-283">*Vyhledání media dotaz*</span><span class="sxs-lookup"><span data-stu-id="0bf25-283">*Locating the media query*</span></span>
4. <span data-ttu-id="0bf25-284">Nahraďte hodnotu atributu maximální šířka nastavenou v 850 px s **10px**, aby bylo možné zakázat adaptivního vykreslování a stiskněte klávesu **kombinaci kláves CTRL + S** a uložte změny.</span><span class="sxs-lookup"><span data-stu-id="0bf25-284">Replace the max-width attribute value set in 850 px with **10px**, in order to disable the adaptive rendering, and press **CTRL + S** to save the changes.</span></span> <span data-ttu-id="0bf25-285">Vraťte do prohlížeče a stiskněte klávesu **kombinaci kláves CTRL + F5** obnovíte stránku s provedené změny.</span><span class="sxs-lookup"><span data-stu-id="0bf25-285">Return to the browser and press **CTRL + F5** to refresh the page with the changes you have made.</span></span> <span data-ttu-id="0bf25-286">Všimněte si rozdíly v obou stránek, při úpravě šířky okna.</span><span class="sxs-lookup"><span data-stu-id="0bf25-286">Notice the differences in both pages when adjusting the width of the window.</span></span>

    <span data-ttu-id="0bf25-287">![Na levé straně stránky aplikuje @media styl, v pravém styl je vynechán](whats-new-in-aspnet-mvc-4/_static/image17.png "na levé straně stránky použití @media styl, v pravém styl je vynechán.")</span><span class="sxs-lookup"><span data-stu-id="0bf25-287">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image17.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="0bf25-288">*Na levé straně stránky aplikuje @media styl, v pravém styl je vynechán.*</span><span class="sxs-lookup"><span data-stu-id="0bf25-288">*In the left, the page is applying the @media style, in the right, the style is omitted*</span></span>

    <span data-ttu-id="0bf25-289">Nyní Pojďme podívejte se na co se stane, že na mobilních zařízeních:</span><span class="sxs-lookup"><span data-stu-id="0bf25-289">Now, let's check out what happens on mobile devices:</span></span>

    <span data-ttu-id="0bf25-290">![Na levé straně stránky aplikuje @media styl, v pravém styl je vynechán](whats-new-in-aspnet-mvc-4/_static/image18.png "na levé straně stránky použití @media styl, v pravém styl je vynechán.")</span><span class="sxs-lookup"><span data-stu-id="0bf25-290">![In the left, the page is applying the @media style, in the right, the style is omitted](whats-new-in-aspnet-mvc-4/_static/image18.png "In the left, the page is applying the @media style, in the right, the style is omitted")</span></span>

    <span data-ttu-id="0bf25-291">*Na levé straně stránky aplikuje @media styl, v pravém styl je vynechán.*</span><span class="sxs-lookup"><span data-stu-id="0bf25-291">*In the left, the page is applying the @media style, in the right, the style is omitted*</span></span>

    <span data-ttu-id="0bf25-292">I když si všimnete, že změny při vykreslení stránky ve webovém prohlížeči nejsou velmi důležité, pokud používáte mobilní zařízení stane zřejmější rozdíly.</span><span class="sxs-lookup"><span data-stu-id="0bf25-292">Although you will notice that the changes when the page is rendered in a Web browser are not very significant, when using a mobile device the differences become more obvious.</span></span> <span data-ttu-id="0bf25-293">Na levé straně bitové kopie můžete vidíte, že vlastní styl lepší čitelnost.</span><span class="sxs-lookup"><span data-stu-id="0bf25-293">On the left side of the image, we can see that the custom style improved the readability.</span></span>

    <span data-ttu-id="0bf25-294">Adaptivního vykreslování lze použít v mnoha scénářích další, což usnadňuje použít podmíněného styly na web a řešení běžných problémů styl s úhledné přístup.</span><span class="sxs-lookup"><span data-stu-id="0bf25-294">Adaptive rendering can be used in many more scenarios, making it easier to apply conditional styling to a Web site and solving common style issues with a neat approach.</span></span>

    <span data-ttu-id="0bf25-295">Zobrazení metaznačku a dotazy na média šablon stylů CSS nejsou specifické pro ASP.NET MVC 4, takže můžete využít výhod těchto funkcí v jakékoli webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="0bf25-295">The Viewport meta tag and CSS media queries are not specific to ASP.NET MVC 4, so you can take advantage of these features in any web application.</span></span>
5. <span data-ttu-id="0bf25-296">V sadě Visual Studio, stiskněte klávesu **SHIFT** + **F5** Zastavit ladění aplikace.</span><span class="sxs-lookup"><span data-stu-id="0bf25-296">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a><span data-ttu-id="0bf25-297">Cvičení 2: Vytvoření webové aplikace Fotogalerie</span><span class="sxs-lookup"><span data-stu-id="0bf25-297">Exercise 2: Creating the Photo Gallery Web Application</span></span>

<span data-ttu-id="0bf25-298">V tomto cvičení budete pracovat na aplikaci Fotogalerie zobrazíte fotografie.</span><span class="sxs-lookup"><span data-stu-id="0bf25-298">In this exercise, you will work on a Photo Gallery application to display photos.</span></span> <span data-ttu-id="0bf25-299">Bude spuštěn v šabloně projektu ASP.NET MVC 4, a pak přidáte funkci načtení fotografií ze služby a je zobrazit na domovské stránce.</span><span class="sxs-lookup"><span data-stu-id="0bf25-299">You will start with the ASP.NET MVC 4 project template, and then you will add a feature to retrieve photos from a service and display them in the home page.</span></span>

<span data-ttu-id="0bf25-300">V následujícím cvičení aktualizujte toto řešení pro zlepšení způsob, jakým se zobrazí na mobilních zařízeních.</span><span class="sxs-lookup"><span data-stu-id="0bf25-300">In the following exercise, you will update this solution to enhance the way it is displayed on mobile devices.</span></span>

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a><span data-ttu-id="0bf25-301">Úloha 1 – vytvoření služby Imitované fotografie</span><span class="sxs-lookup"><span data-stu-id="0bf25-301">Task 1 - Creating a Mock Photo Service</span></span>

<span data-ttu-id="0bf25-302">V této úloze se vytvoří model služby fotografii k získání obsahu, který se zobrazí v galerii.</span><span class="sxs-lookup"><span data-stu-id="0bf25-302">In this task, you will create a mock of the photo service to retrieve the content that will be displayed in the gallery.</span></span> <span data-ttu-id="0bf25-303">K tomuto účelu přidáte nový řadič, jednoduše vrátí soubor JSON s daty každé fotografie.</span><span class="sxs-lookup"><span data-stu-id="0bf25-303">To do this, you will add a new controller that will simply return a JSON file with the data of each photo.</span></span>

1. <span data-ttu-id="0bf25-304">Otevřete **Visual Studio** Pokud ještě není otevřené.</span><span class="sxs-lookup"><span data-stu-id="0bf25-304">Open **Visual Studio** if not already opened.</span></span>
2. <span data-ttu-id="0bf25-305">Vyberte **souboru | Nové | Projekt** příkazu nabídky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-305">Select the **File | New | Project** menu command.</span></span> <span data-ttu-id="0bf25-306">V **nový projekt** dialogovém okně, vyberte **Visual C# | Webové** šablony v levém podokně stromu a vyberte **webové aplikace ASP.NET MVC 4.**</span><span class="sxs-lookup"><span data-stu-id="0bf25-306">In the **New Project** dialog, select the **Visual C# | Web** template on the left pane tree, and choose **ASP.NET MVC 4 Web Application.**</span></span> <span data-ttu-id="0bf25-307">Název projektu **Fotogalerie**, vyberte umístění (nebo ponechte výchozí nastavení) a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-307">Name the project **PhotoGallery**, select a location (or leave the default) and click **OK**.</span></span> <span data-ttu-id="0bf25-308">Alternativně můžete pokračovat v práci z existující ASP.NET MVC 4 **Internetové aplikace** řešení z **cvičení 1** a přejděte na další krok.</span><span class="sxs-lookup"><span data-stu-id="0bf25-308">Alternatively, you can continue working from your existing ASP.NET MVC 4 **Internet Application** solution from **Exercise 1** and skip the next step.</span></span>
3. <span data-ttu-id="0bf25-309">V **nový ASP.NET MVC 4 projekt** dialogové okno, vyberte **Internetové aplikace** šablona projektu a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-309">In the **New ASP.NET MVC 4 Project** dialog box, select the **Internet Application** project template and click **OK**.</span></span> <span data-ttu-id="0bf25-310">Ujistěte se, že jste vybrali jako zobrazovací modul Razor.</span><span class="sxs-lookup"><span data-stu-id="0bf25-310">Make sure you have Razor selected as the View Engine.</span></span>
4. <span data-ttu-id="0bf25-311">V **Průzkumníku řešení**, klikněte pravým tlačítkem myši **aplikace\_Data** složku projekt a vyberte **přidat | Existující položka**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-311">In the **Solution Explorer**, right-click the **App\_Data** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="0bf25-312">Vyhledejte **Source\Assets\App\_Data** složky tohoto testovacího prostředí a přidejte **Photos.json** souboru.</span><span class="sxs-lookup"><span data-stu-id="0bf25-312">Browse to the **Source\Assets\App\_Data** folder of this lab and add the **Photos.json** file.</span></span>
5. <span data-ttu-id="0bf25-313">Vytvořte nový řadič s názvem **PhotoController**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-313">Create a new controller with the name **PhotoController**.</span></span> <span data-ttu-id="0bf25-314">Chcete-li to provést, klikněte pravým tlačítkem na **řadiče** složku, přejděte na **přidat** a vyberte **řadiče.**</span><span class="sxs-lookup"><span data-stu-id="0bf25-314">To do this, right-click on the **Controllers** folder, go to **Add** and select **Controller.**</span></span> <span data-ttu-id="0bf25-315">Dokončení názvu kontroleru, ponechte **kontroler MVC prázdný** šablonu a klikněte na tlačítko **přidat**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-315">Complete the controller name, leave the **Empty MVC controller** template and click **Add**.</span></span>

    <span data-ttu-id="0bf25-316">![Přidávání PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "přidání PhotoController")</span><span class="sxs-lookup"><span data-stu-id="0bf25-316">![Adding the PhotoController](whats-new-in-aspnet-mvc-4/_static/image19.png "Adding the PhotoController")</span></span>

    <span data-ttu-id="0bf25-317">*Přidávání PhotoController*</span><span class="sxs-lookup"><span data-stu-id="0bf25-317">*Adding the PhotoController*</span></span>
6. <span data-ttu-id="0bf25-318">Nahraďte **Index** metoda s následující **Galerie** akce a vrátí obsah ze souboru JSON jste nedávno přidali do projektu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-318">Replace the **Index** method with the following **Gallery** action, and return the content from the JSON file you have recently added to the project.</span></span>

    <span data-ttu-id="0bf25-319">(Code fragment kódu - *architektury ASP.NET MVC 4 laboratoř - Ex02 - Galerie akce*)</span><span class="sxs-lookup"><span data-stu-id="0bf25-319">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Gallery Action*)</span></span>


    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
7. <span data-ttu-id="0bf25-320">Stiskněte klávesu **F5** pro spuštění řešení a pak přejděte na následující adresu URL k testování služby mocked fotografií: `http://localhost:[port]/photo/gallery` (hodnoty [port] závisí na aktuální portu, kde byla aplikace spuštěná).</span><span class="sxs-lookup"><span data-stu-id="0bf25-320">Press **F5** to run the solution, and then browse to the following URL in order to test the mocked photo service: `http://localhost:[port]/photo/gallery` (the [port] value depends on the current port where the application was launched).</span></span> <span data-ttu-id="0bf25-321">Požadavek na tuto adresu URL by měla načíst obsah **Photos.json** souboru.</span><span class="sxs-lookup"><span data-stu-id="0bf25-321">The request to this URL should retrieve the content of the **Photos.json** file.</span></span>

    <span data-ttu-id="0bf25-322">![Testování službu mocked fotografií](whats-new-in-aspnet-mvc-4/_static/image20.png "testování mocked fotografií služby")</span><span class="sxs-lookup"><span data-stu-id="0bf25-322">![Testing the mocked photo service](whats-new-in-aspnet-mvc-4/_static/image20.png "Testing the mocked photo service")</span></span>

    <span data-ttu-id="0bf25-323">*Testování mocked fotografií služby*</span><span class="sxs-lookup"><span data-stu-id="0bf25-323">*Testing the mocked photo service*</span></span>

<span data-ttu-id="0bf25-324">V implementaci skutečné můžete použít [rozhraní ASP.NET Web API](../../../../web-api/index.md) k implementaci služby Fotogalerie.</span><span class="sxs-lookup"><span data-stu-id="0bf25-324">In a real implementation you could use [ASP.NET Web API](../../../../web-api/index.md) to implement the Photo Gallery service.</span></span> <span data-ttu-id="0bf25-325">Rozhraní ASP.NET Web API je rozhraní, které usnadňuje sestavování služeb HTTP, které využity širokou škálou klientů včetně prohlížečů a mobilních zařízení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-325">ASP.NET Web API is a framework that makes it easy to build HTTP services that reach a broad range of clients, including browsers and mobile devices.</span></span> <span data-ttu-id="0bf25-326">Rozhraní ASP.NET Web API je ideální platformu pro sestavování aplikací RESTful v rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="0bf25-326">ASP.NET Web API is an ideal platform for building RESTful applications on the .NET Framework.</span></span>

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a><span data-ttu-id="0bf25-327">Úloha 2 – zobrazení galerie fotografií</span><span class="sxs-lookup"><span data-stu-id="0bf25-327">Task 2 - Displaying the Photo Gallery</span></span>

<span data-ttu-id="0bf25-328">V této úloze aktualizujte domovské stránce k zobrazení galerie fotografií pomocí mocked službu, kterou jste vytvořili v první úloze tohoto cvičení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-328">In this task, you will update the Home page to show the photo gallery by using the mocked service you created in the first task of this exercise.</span></span> <span data-ttu-id="0bf25-329">Přidáte soubory modelu a aktualizovat zobrazení galerie.</span><span class="sxs-lookup"><span data-stu-id="0bf25-329">You will add model files and update the gallery views.</span></span>

1. <span data-ttu-id="0bf25-330">V sadě Visual Studio, stiskněte klávesu **SHIFT** + **F5** Zastavit ladění aplikace.</span><span class="sxs-lookup"><span data-stu-id="0bf25-330">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="0bf25-331">Vytvořte **fotografií** třídy v **modely** složky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-331">Create the **Photo** class in the **Models** folder.</span></span> <span data-ttu-id="0bf25-332">Chcete-li to provést, klikněte pravým tlačítkem na **modely** složky, vyberte **přidat** a klikněte na tlačítko **třída**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-332">To do this, right-click on the **Models** folder, select **Add** and click **Class**.</span></span> <span data-ttu-id="0bf25-333">Potom nastavte název na **Photo.cs** a klikněte na tlačítko **přidat**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-333">Then, set the name to **Photo.cs** and click **Add**.</span></span>
3. <span data-ttu-id="0bf25-334">Přidejte následující členy **fotografií** třídy.</span><span class="sxs-lookup"><span data-stu-id="0bf25-334">Add the following members to the **Photo** class.</span></span>

    <span data-ttu-id="0bf25-335">(Code fragment kódu - *modelu ASP.NET MVC 4 laboratoř - Ex02 - fotografie*)</span><span class="sxs-lookup"><span data-stu-id="0bf25-335">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo model*)</span></span>


    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
4. <span data-ttu-id="0bf25-336">Otevřete **HomeController.cs** souboru z **řadiče** složky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-336">Open the **HomeController.cs** file from the **Controllers** folder.</span></span>
5. <span data-ttu-id="0bf25-337">Přidejte následující příkazy using.</span><span class="sxs-lookup"><span data-stu-id="0bf25-337">Add the following using statements.</span></span>

    <span data-ttu-id="0bf25-338">(Code fragment kódu - *architektury ASP.NET MVC 4 laboratoř - Ex02 - HomeController direktiv Using*)</span><span class="sxs-lookup"><span data-stu-id="0bf25-338">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - HomeController Usings*)</span></span>


    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
6. <span data-ttu-id="0bf25-339">Aktualizace **Index** akci použít **HttpClient** k načtení dat Galerie a potom pomocí **JavaScriptSerializer** k deserializaci do modelu zobrazení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-339">Update the **Index** action to use **HttpClient** to retrieve the gallery data, and then use the **JavaScriptSerializer** to deserialize it to the view model.</span></span>

    <span data-ttu-id="0bf25-340">(Code fragment kódu - *architektury ASP.NET MVC 4 laboratoř - Ex02 - indexu akce*)</span><span class="sxs-lookup"><span data-stu-id="0bf25-340">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Index Action*)</span></span>


    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
7. <span data-ttu-id="0bf25-341">Otevřete **Index.cshtml** soubor umístěný v části **Views\Home** složky a nahradit veškerý obsah následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="0bf25-341">Open the **Index.cshtml** file located under the **Views\Home** folder and replace all the content with the following code.</span></span>

    <span data-ttu-id="0bf25-342">Tento kód projde všech fotografií získaný ze služby a zobrazí je do neuspořádaný seznam.</span><span class="sxs-lookup"><span data-stu-id="0bf25-342">This code loops through all the photos retrieved from the service and displays them into an unordered list.</span></span>

    <span data-ttu-id="0bf25-343">(Code fragment kódu - *architektury ASP.NET MVC 4 laboratoř - Ex02 - fotografií seznamu*)</span><span class="sxs-lookup"><span data-stu-id="0bf25-343">(Code Snippet - *ASP.NET MVC 4 Lab - Ex02 - Photo List*)</span></span>


    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
8. <span data-ttu-id="0bf25-344">V **Průzkumníku řešení**, klikněte pravým tlačítkem myši **obsahu** složku projekt a vyberte **přidat | Existující položka**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-344">In the **Solution Explorer**, right-click the **Content** folder of your project, and select **Add | Existing Item**.</span></span> <span data-ttu-id="0bf25-345">Vyhledejte **Source\Assets\Content** složky tohoto testovacího prostředí a přidejte **Site.css** souboru.</span><span class="sxs-lookup"><span data-stu-id="0bf25-345">Browse to the **Source\Assets\Content** folder of this lab and add the **Site.css** file.</span></span> <span data-ttu-id="0bf25-346">Budete muset potvrdit jeho nahrazení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-346">You will have to confirm its replacement.</span></span> <span data-ttu-id="0bf25-347">Pokud máte **Site.css** soubor otevřít, budete muset potvrďte také znovu načíst soubor.</span><span class="sxs-lookup"><span data-stu-id="0bf25-347">If you have the **Site.css** file open, you will have to confirm to reload the file also.</span></span>
9. <span data-ttu-id="0bf25-348">Otevřete Průzkumníka souborů a zkopírujte celou **fotografie** složka umístěná **Source\Assets** složky tohoto testovacího prostředí do kořenové složky vašeho projektu v Průzkumníku řešení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-348">Open File Explorer and copy the entire **Photos** folder located under the **Source\Assets** folder of this lab to the root folder of your project in Solution Explorer.</span></span>
10. <span data-ttu-id="0bf25-349">Spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="0bf25-349">Run the application.</span></span> <span data-ttu-id="0bf25-350">Měli byste nyní vidět na domovskou stránku zobrazení fotografií v galerii.</span><span class="sxs-lookup"><span data-stu-id="0bf25-350">You should now see the home page displaying the photos in the gallery.</span></span>

    <span data-ttu-id="0bf25-351">![Galerie fotografií](whats-new-in-aspnet-mvc-4/_static/image21.png "Fotogalerie")</span><span class="sxs-lookup"><span data-stu-id="0bf25-351">![Photo Gallery](whats-new-in-aspnet-mvc-4/_static/image21.png "Photo Gallery")</span></span>

    <span data-ttu-id="0bf25-352">*Galerie fotografií*</span><span class="sxs-lookup"><span data-stu-id="0bf25-352">*Photo Gallery*</span></span>
11. <span data-ttu-id="0bf25-353">V sadě Visual Studio, stiskněte klávesu **SHIFT** + **F5** Zastavit ladění aplikace.</span><span class="sxs-lookup"><span data-stu-id="0bf25-353">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a><span data-ttu-id="0bf25-354">Cvičení 3: Přidání podpory pro mobilní zařízení</span><span class="sxs-lookup"><span data-stu-id="0bf25-354">Exercise 3: Adding support for mobile devices</span></span>

<span data-ttu-id="0bf25-355">Jednou z klíčových aktualizací v architektuře ASP.NET MVC 4 je podpora pro vývoj mobilních řešení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-355">One of the key updates in ASP.NET MVC 4 is the support for mobile development.</span></span> <span data-ttu-id="0bf25-356">V tomto cvičení zaměříte ASP.NET MVC 4 nové funkce pro mobilní aplikace tím, že rozšíří Fotogalerie řešení, které jste vytvořili v předchozím cvičení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-356">In this exercise, you will explore ASP.NET MVC 4 new features for mobile applications by extending the PhotoGallery solution you have created in the previous exercise.</span></span>

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a><span data-ttu-id="0bf25-357">Úloha 1 - instalaci jQuery Mobile v aplikaci ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="0bf25-357">Task 1 - Installing jQuery Mobile in an ASP.NET MVC 4 Application</span></span>

1. <span data-ttu-id="0bf25-358">Otevřete **začít** řešení nacházející se v **zdroj/EX3.-MobileSupport/počáteční/** složky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-358">Open the **Begin** solution located at **Source/Ex3-MobileSupport/Begin/** folder.</span></span> <span data-ttu-id="0bf25-359">Jinak, může pokračovat, pomocí **End** řešení získat provedením předchozím cvičení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-359">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="0bf25-360">Pokud jste otevřeli poskytnutého **začít** řešení, budete muset stáhnout některé chybějící balíčky NuGet než budete pokračovat.</span><span class="sxs-lookup"><span data-stu-id="0bf25-360">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="0bf25-361">Chcete-li to provést, klikněte na tlačítko **projektu** nabídku a vyberte **spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-361">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="0bf25-362">V **spravovat balíčky NuGet** dialogové okno, klikněte na tlačítko **obnovení** Chcete-li stáhnout chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-362">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="0bf25-363">Nakonec sestavte řešení kliknutím **sestavení** | **sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-363">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0bf25-364">Jednou z výhod použití NuGet je, že nemáte pro odeslání všech knihoven v projektu, zmenšení velikosti projektu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-364">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="0bf25-365">Napájení nástroje NuGet zadáním verze balíčku v souboru Packages.config, nebudete moct stáhnout všechny požadované knihovny při prvním spuštění projektu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-365">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="0bf25-366">Z tohoto důvodu je nutné provést tyto kroky po otevření existujícího řešení z tohoto testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="0bf25-366">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="0bf25-367">Otevřete **Konzola správce balíčků** kliknutím **nástroje** &gt; **Správce balíčků knihoven** &gt; **Správce balíčků Konzole** možnost nabídky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-367">Open the **Package Manager Console** by clicking the **Tools** &gt; **Library Package Manager** &gt; **Package Manager Console** menu option.</span></span>

    <span data-ttu-id="0bf25-368">![Otevření konzole Správce balíčků NuGet](whats-new-in-aspnet-mvc-4/_static/image22.png "otevření konzole Správce balíčků NuGet")</span><span class="sxs-lookup"><span data-stu-id="0bf25-368">![Opening the NuGet Package Manager Console](whats-new-in-aspnet-mvc-4/_static/image22.png "Opening the NuGet Package Manager Console")</span></span>

    <span data-ttu-id="0bf25-369">*Otevření konzoly Správce balíčků NuGet*</span><span class="sxs-lookup"><span data-stu-id="0bf25-369">*Opening the NuGet Package Manager Console*</span></span>
3. <span data-ttu-id="0bf25-370">V konzole Správce balíčků spusťte následující příkaz k instalaci **jQuery.Mobile.MVC** balíčku.</span><span class="sxs-lookup"><span data-stu-id="0bf25-370">In the Package Manager Console run the following command to install the **jQuery.Mobile.MVC** package.</span></span>

    <span data-ttu-id="0bf25-371">jQuery Mobile je knihovna s otevřeným zdrojem pro vytváření dotykovým webového uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="0bf25-371">jQuery Mobile is an open source library for building touch-optimized web UI.</span></span> <span data-ttu-id="0bf25-372">Balíček NuGet jQuery.Mobile.MVC zahrnuje pomocné rutiny pro použití jQuery Mobile pomocí aplikace ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="0bf25-372">The jQuery.Mobile.MVC NuGet package includes helpers to use jQuery Mobile with an ASP.NET MVC 4 application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0bf25-373">Spuštěním následujícího příkazu můžete bude stahování knihovně jQuery.Mobile.MVC z Nuget.</span><span class="sxs-lookup"><span data-stu-id="0bf25-373">By running the following command, you will be downloading the jQuery.Mobile.MVC library from Nuget.</span></span>

    <span data-ttu-id="0bf25-374">PM</span><span class="sxs-lookup"><span data-stu-id="0bf25-374">PM</span></span>

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    <span data-ttu-id="0bf25-375">Tento příkaz nainstaluje jQuery Mobile a některé pomocné soubory, včetně následujících:</span><span class="sxs-lookup"><span data-stu-id="0bf25-375">This command installs jQuery Mobile and some helper files, including the following:</span></span>

    - <span data-ttu-id="0bf25-376">**Zobrazení a sdílených nebo\_Layout.Mobile.cshtml**: je optimalizovaná pro menší obrazovky systémem Mobile rozložení jQuery.</span><span class="sxs-lookup"><span data-stu-id="0bf25-376">**Views/Shared/\_Layout.Mobile.cshtml**: is a jQuery Mobile-based layout optimized for a smaller screen.</span></span> <span data-ttu-id="0bf25-377">Když web obdrží žádost od prohlížeč pro mobilní zařízení, nahradí původní rozložení (\_Layout.cshtml) tímto tématem.</span><span class="sxs-lookup"><span data-stu-id="0bf25-377">When the website receives a request from a mobile browser, it will replace the original layout (\_Layout.cshtml) with this one.</span></span>
    - <span data-ttu-id="0bf25-378">Součást přepínači zobrazení: se skládá z **zobrazení a sdílených nebo\_ViewSwitcher.cshtml** částečné zobrazení a **ViewSwitcherController.cs** řadiče.</span><span class="sxs-lookup"><span data-stu-id="0bf25-378">A view-switcher component: consists of the **Views/Shared/\_ViewSwitcher.cshtml** partial view and the **ViewSwitcherController.cs** controller.</span></span> <span data-ttu-id="0bf25-379">Tato součást se zobrazí odkaz na mobilní prohlížeče, aby mohli uživatelé přepnout na verzi pro stolní počítače stránky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-379">This component will show a link on mobile browsers to enable users to switch to the desktop version of the page.</span></span>  
        <span data-ttu-id="0bf25-380">![Galerie fotografií projektu s podporou mobilních](whats-new-in-aspnet-mvc-4/_static/image23.png "Fotogalerie projektu s podporou mobilních")</span><span class="sxs-lookup"><span data-stu-id="0bf25-380">![Photo Gallery project with mobile support](whats-new-in-aspnet-mvc-4/_static/image23.png "Photo Gallery project with mobile support")</span></span>

        <span data-ttu-id="0bf25-381">*Galerie fotografií projektu s podporou mobilních*</span><span class="sxs-lookup"><span data-stu-id="0bf25-381">*Photo Gallery project with mobile support*</span></span>
4. <span data-ttu-id="0bf25-382">Zaregistrujte mobilní sady.</span><span class="sxs-lookup"><span data-stu-id="0bf25-382">Register the Mobile bundles.</span></span> <span data-ttu-id="0bf25-383">Chcete-li to provést, otevřete **Global.asax.cs** souboru a přidejte následující řádek.</span><span class="sxs-lookup"><span data-stu-id="0bf25-383">To do this, open the **Global.asax.cs** file and add the following line.</span></span>

    <span data-ttu-id="0bf25-384">(Code fragment kódu - *architektury ASP.NET MVC 4 laboratoř - Ex03 - zaregistrovat mobilní sady*)</span><span class="sxs-lookup"><span data-stu-id="0bf25-384">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - Register Mobile Bundles*)</span></span>


    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
5. <span data-ttu-id="0bf25-385">Spusťte aplikaci pomocí plochy webového prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="0bf25-385">Run the application using a desktop web browser.</span></span>
6. <span data-ttu-id="0bf25-386">Otevřete **Windows Phone 7 emulátoru,** umístěný v **nabídce Start | Všechny programy | Windows Phone SDK 7.1 | Emulátor Windows Phone.**</span><span class="sxs-lookup"><span data-stu-id="0bf25-386">Open the **Windows Phone 7 Emulator,** located in **Start Menu | All Programs | Windows Phone SDK 7.1 | Windows Phone Emulator.**</span></span>
7. <span data-ttu-id="0bf25-387">Na obrazovce start phone otevřete Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="0bf25-387">In the phone start screen, open Internet Explorer.</span></span> <span data-ttu-id="0bf25-388">Podívejte se na adresu URL, kde je aplikace spuštěna a přejděte na tuto adresu URL pomocí prohlížeče telefonu (například `http://localhost:[PortNumber]/`).</span><span class="sxs-lookup"><span data-stu-id="0bf25-388">Check out the URL where the application started and browse to that URL with the phone browser (e.g. `http://localhost:[PortNumber]/`).</span></span>

    <span data-ttu-id="0bf25-389">Si všimnete, že aplikace bude vypadat různých v emulátoru Windows Phone, jako jQuery.Mobile.MVC vytvořil nové prostředky ve vašem projektu, který zobrazí zobrazení optimalizované pro mobilní zařízení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-389">You will notice that your application will look different in the Windows Phone emulator, as the jQuery.Mobile.MVC has created new assets in your project that show views optimized for mobile devices.</span></span>

    <span data-ttu-id="0bf25-390">Všimněte si zpráv v horní části telefonu, zobrazuje odkaz, který se přepne do zobrazení plochy.</span><span class="sxs-lookup"><span data-stu-id="0bf25-390">Notice the message at the top of the phone, showing the link that switches to the Desktop view.</span></span> <span data-ttu-id="0bf25-391">Kromě toho  **\_Layout.Mobile.cshtml** rozložení, který byl vytvořen jste nainstalovali balíček je včetně rozložení v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="0bf25-391">Additionally, the **\_Layout.Mobile.cshtml** layout that was created by the package you have installed is including a different layout in the application.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0bf25-392">Zatím není žádný odkaz na mobilní zobrazení nelze vrátit zpět.</span><span class="sxs-lookup"><span data-stu-id="0bf25-392">So far, there is no link to get back to mobile view.</span></span> <span data-ttu-id="0bf25-393">Mají být zahrnuty v novějších verzích.</span><span class="sxs-lookup"><span data-stu-id="0bf25-393">It will be included in later versions.</span></span>

    <span data-ttu-id="0bf25-394">![Mobilní zobrazení fotografií Galerie domovské stránky](whats-new-in-aspnet-mvc-4/_static/image24.png "mobilní zobrazení fotografií Galerie domovské stránky")</span><span class="sxs-lookup"><span data-stu-id="0bf25-394">![Mobile view of the Photo Gallery Home page](whats-new-in-aspnet-mvc-4/_static/image24.png "Mobile view of the Photo Gallery Home page")</span></span>

    <span data-ttu-id="0bf25-395">*Mobilní zobrazení fotografií Galerie domovské stránky*</span><span class="sxs-lookup"><span data-stu-id="0bf25-395">*Mobile view of the Photo Gallery Home page*</span></span>
8. <span data-ttu-id="0bf25-396">V sadě Visual Studio, stiskněte klávesu **SHIFT** + **F5** Zastavit ladění aplikace.</span><span class="sxs-lookup"><span data-stu-id="0bf25-396">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a><span data-ttu-id="0bf25-397">Úloha 2 – Vytvoření mobilní zobrazení</span><span class="sxs-lookup"><span data-stu-id="0bf25-397">Task 2 - Creating Mobile Views</span></span>

<span data-ttu-id="0bf25-398">V této úloze vytvoříte mobilní verzi zobrazení pro index s obsah přizpůsobit pro lepší appareance v mobilních zařízeních.</span><span class="sxs-lookup"><span data-stu-id="0bf25-398">In this task, you will create a mobile version of the index view with content adapted for better appareance in mobile devices.</span></span>

1. <span data-ttu-id="0bf25-399">Kopírování **Views\Home\Index.cshtml** zobrazení a vložte ji k vytvoření kopie, přejmenujte nového souboru **Index.Mobile.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-399">Copy the **Views\Home\Index.cshtml** view and paste it to create a copy, rename the new file to **Index.Mobile.cshtml**.</span></span>
2. <span data-ttu-id="0bf25-400">Otevřete nový vytvořit **Index.Mobile.cshtml** zobrazení a nahradit existující &lt;ul&gt; značky s tímto kódem.</span><span class="sxs-lookup"><span data-stu-id="0bf25-400">Open the new created **Index.Mobile.cshtml** view and replace the existing &lt;ul&gt; tag with this code.</span></span> <span data-ttu-id="0bf25-401">Díky tomu bude aktualizace &lt;ul&gt; značky s anotacemi mobilních dat jQuery pomocí mobilních motivů z jQuery.</span><span class="sxs-lookup"><span data-stu-id="0bf25-401">By doing this, you will be updating the &lt;ul&gt; tag with jQuery Mobile data annotations to use the mobile themes from jQuery.</span></span>


    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

    > [!NOTE] 
    > 
    > <span data-ttu-id="0bf25-402">Všimněte si, že:</span><span class="sxs-lookup"><span data-stu-id="0bf25-402">Notice that:</span></span>
    > 
    > - <span data-ttu-id="0bf25-403">**Data-role** atribut nastaven na **listview** vykreslí seznamu pomocí listview stylů.</span><span class="sxs-lookup"><span data-stu-id="0bf25-403">The **data-role** attribute set to **listview** will render the list using the listview styles.</span></span>
    > 
    > - <span data-ttu-id="0bf25-404">**Data inset** atribut nastaven na hodnotu true se zobrazí v seznamu s zaokrouhlené okraj a okraj.</span><span class="sxs-lookup"><span data-stu-id="0bf25-404">The **data-inset** attribute set to true will show the list with rounded border and margin.</span></span>
    > 
    > - <span data-ttu-id="0bf25-405">**Filtr dat** atribut nastaven na **true** vygeneruje vyhledávací pole.</span><span class="sxs-lookup"><span data-stu-id="0bf25-405">The **data-filter** attribute set to **true** will generate a search box.</span></span>
    > 
    > <span data-ttu-id="0bf25-406">Další informace o mobilních konvence jQuery v dokumentaci k projektu: [ [http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)</span><span class="sxs-lookup"><span data-stu-id="0bf25-406">You can learn more about jQuery Mobile conventions in the project documentation: [[http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)</span></span>
3. <span data-ttu-id="0bf25-407">Stiskněte klávesu **kombinaci kláves CTRL + S** a uložte změny.</span><span class="sxs-lookup"><span data-stu-id="0bf25-407">Press **CTRL + S** to save the changes.</span></span>
4. <span data-ttu-id="0bf25-408">Přepnout **emulátoru Windows Phone** a aktualizovat lokalitu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-408">Switch to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="0bf25-409">Všimněte si nového vzhledu a chování seznamu galerie, jakož i nové vyhledávacího pole umístěné v horní části.</span><span class="sxs-lookup"><span data-stu-id="0bf25-409">Notice the new look and feel of the gallery list, as well as the new search box located on the top.</span></span> <span data-ttu-id="0bf25-410">Poté do vyhledávacího pole zadejte slovo (například **Tulipány**) Chcete-li hledat v galerii fotografií.</span><span class="sxs-lookup"><span data-stu-id="0bf25-410">Then, type a word in the search box (for instance, **Tulips**) to start a search in the photo gallery.</span></span>

    <span data-ttu-id="0bf25-411">![Pomocí filtrování listview styl galerie](whats-new-in-aspnet-mvc-4/_static/image25.png "Galerie pomocí filtrování styl listview")</span><span class="sxs-lookup"><span data-stu-id="0bf25-411">![Gallery using listview style with filtering](whats-new-in-aspnet-mvc-4/_static/image25.png "Gallery using listview style with filtering")</span></span>

    <span data-ttu-id="0bf25-412">*Galerie pomocí filtrování styl listview*</span><span class="sxs-lookup"><span data-stu-id="0bf25-412">*Gallery using listview style with filtering*</span></span>

    <span data-ttu-id="0bf25-413">To Shrneme, jste použili recepturách zobrazení Mobilizer Pokud chcete vytvořit kopii zobrazení Index se &quot;mobilní&quot; příponu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-413">To summarize, you have used the View Mobilizer recipe to create a copy of the Index view with the &quot;mobile&quot; suffix.</span></span> <span data-ttu-id="0bf25-414">Tato přípona ASP.NET MVC 4 označuje, že každou žádost vygeneruje z mobilního zařízení bude používat tuto kopii index.</span><span class="sxs-lookup"><span data-stu-id="0bf25-414">This suffix indicates to ASP.NET MVC 4 that every request generated from a mobile device will use this copy of the index.</span></span> <span data-ttu-id="0bf25-415">Kromě toho jste aktualizovali mobilní verzi Index zobrazení pro použití jQuery Mobile rozšíření lokality vzhledu a chování v mobilních zařízeních.</span><span class="sxs-lookup"><span data-stu-id="0bf25-415">Additionally, you have updated the mobile version of the Index view to use jQuery Mobile for enhancing the site look and feel in mobile devices.</span></span>
5. <span data-ttu-id="0bf25-416">Přejděte zpět na Visual Studio a otevřete **Site.Mobile.css** umístěná **obsahu** složky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-416">Go back to Visual Studio and open **Site.Mobile.css** located under the **Content** folder.</span></span>
6. <span data-ttu-id="0bf25-417">Opravte umístění titulek fotografie, chcete-li zobrazit na pravé straně bitové kopie.</span><span class="sxs-lookup"><span data-stu-id="0bf25-417">Fix the positioning of the photo title to make it show at the right side of the image.</span></span> <span data-ttu-id="0bf25-418">K tomu, přidejte následující kód, který **Site.Mobile.css** souboru.</span><span class="sxs-lookup"><span data-stu-id="0bf25-418">To do this, add the following code to the **Site.Mobile.css** file.</span></span>

    <span data-ttu-id="0bf25-419">CSS</span><span class="sxs-lookup"><span data-stu-id="0bf25-419">CSS</span></span>

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. <span data-ttu-id="0bf25-420">Stiskněte klávesu **kombinaci kláves CTRL + S** a uložte změny.</span><span class="sxs-lookup"><span data-stu-id="0bf25-420">Press **CTRL + S** to save the changes.</span></span>
8. <span data-ttu-id="0bf25-421">Přepnout zpět **emulátoru Windows Phone** a aktualizovat lokalitu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-421">Switch back to the **Windows Phone Emulator** and refresh the site.</span></span> <span data-ttu-id="0bf25-422">Všimněte si, že název fotografií je správně nastavený teď.</span><span class="sxs-lookup"><span data-stu-id="0bf25-422">Notice the photo title is properly positioned now.</span></span>

    <span data-ttu-id="0bf25-423">![Název umístěný na pravé straně bitové kopie](whats-new-in-aspnet-mvc-4/_static/image26.png "Title umístěný na pravé straně bitové kopie")</span><span class="sxs-lookup"><span data-stu-id="0bf25-423">![Title positioned on the right side of the image](whats-new-in-aspnet-mvc-4/_static/image26.png "Title positioned on the right side of the image")</span></span>

    <span data-ttu-id="0bf25-424">*Název umístěný na pravé straně bitové kopie*</span><span class="sxs-lookup"><span data-stu-id="0bf25-424">*Title positioned on the right side of the image*</span></span>

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a><span data-ttu-id="0bf25-425">Úloha 3 – motivy jQuery Mobile</span><span class="sxs-lookup"><span data-stu-id="0bf25-425">Task 3 - jQuery Mobile Themes</span></span>

<span data-ttu-id="0bf25-426">Každé rozložení a widget jQuery Mobile je uspořádaná kolem nové objektově orientované šablon stylů CSS rozhraní, které vám umožní použít dokončení jednotná visual návrhu motiv k webům a aplikacím.</span><span class="sxs-lookup"><span data-stu-id="0bf25-426">Every layout and widget in jQuery Mobile is designed around a new object-oriented CSS framework that makes it possible to apply a complete unified visual design theme to sites and applications.</span></span>

<span data-ttu-id="0bf25-427">jQuery Mobile výchozí motiv zahrnuje 5 vzorník, které jsou uvedeny písmena (a, b, c, d e) pro rychlou referenci.</span><span class="sxs-lookup"><span data-stu-id="0bf25-427">jQuery Mobile's default Theme includes 5 swatches that are given letters (a, b, c, d, e) for quick reference.</span></span>

<span data-ttu-id="0bf25-428">V této úloze aktualizujte mobilní rozložení používat jiný než výchozí motiv.</span><span class="sxs-lookup"><span data-stu-id="0bf25-428">In this task, you will update the mobile layout to use a different theme than the default.</span></span>

1. <span data-ttu-id="0bf25-429">Přepněte zpátky na Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0bf25-429">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="0bf25-430">Otevřete  **\_Layout.Mobile.cshtml** soubor umístěný ve **Views\Shared**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-430">Open the **\_Layout.Mobile.cshtml** file located in **Views\Shared**.</span></span>
3. <span data-ttu-id="0bf25-431">Najít div element k roli dat nastavena na &quot;stránky&quot; a aktualizovat **data-theme** k &quot; **e**&quot;.</span><span class="sxs-lookup"><span data-stu-id="0bf25-431">Find the div element with the data-role set to &quot;page&quot; and update the **data-theme** to &quot;**e**&quot;.</span></span>


    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
4. <span data-ttu-id="0bf25-432">Stiskněte klávesu **kombinaci kláves CTRL + S** a uložte změny.</span><span class="sxs-lookup"><span data-stu-id="0bf25-432">Press **CTRL + S** to save the changes.</span></span>
5. <span data-ttu-id="0bf25-433">Aktualizujte lokality v **emulátoru Windows Phone** a Všimněte si nové schéma barev.</span><span class="sxs-lookup"><span data-stu-id="0bf25-433">Refresh the site in the **Windows Phone Emulator** and notice the new colors scheme.</span></span>

    <span data-ttu-id="0bf25-434">![Mobilní rozložení s jiné barevné schéma](whats-new-in-aspnet-mvc-4/_static/image27.png "mobilní rozložení s jiné barevné schéma")</span><span class="sxs-lookup"><span data-stu-id="0bf25-434">![Mobile layout with a different color scheme](whats-new-in-aspnet-mvc-4/_static/image27.png "Mobile layout with a different color scheme")</span></span>

    <span data-ttu-id="0bf25-435">*Mobilní rozložení s jiné barevné schéma*</span><span class="sxs-lookup"><span data-stu-id="0bf25-435">*Mobile layout with a different color scheme*</span></span>

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a><span data-ttu-id="0bf25-436">Úloha 4 – pomocí komponentu přepínači zobrazení a prohlížeče přepisování funkcí</span><span class="sxs-lookup"><span data-stu-id="0bf25-436">Task 4 - Using the View-Switcher Component and the Browser Overriding Features</span></span>

<span data-ttu-id="0bf25-437">Konvence pro optimalizované mobilní webové stránky je přidat odkaz, jejíž text je něco jako zobrazení plochy nebo režim plnou verzi webu, který umožňuje uživatelům přepnout na ploše verzi stránky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-437">A convention for mobile-optimized web pages is to add a link whose text is something like Desktop view or Full site mode that lets users switch to a desktop version of the page.</span></span> <span data-ttu-id="0bf25-438">Balíček jQuery.Mobile.MVC obsahuje ukázkový **přepínači zobrazení** součásti pro tento účel použít v  **\_Layout.Mobile.cshtml** zobrazení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-438">The jQuery.Mobile.MVC package includes a sample **view-switcher** component for this purpose used in the **\_Layout.Mobile.cshtml** view.</span></span>

<span data-ttu-id="0bf25-439">![Odkaz na přepnout na zobrazení plochy](whats-new-in-aspnet-mvc-4/_static/image28.png "odkaz na přepnout na zobrazení plochy")</span><span class="sxs-lookup"><span data-stu-id="0bf25-439">![Link to switch to Desktop View](whats-new-in-aspnet-mvc-4/_static/image28.png "Link to switch to Desktop View")</span></span>

<span data-ttu-id="0bf25-440">*Propojit přepnout do zobrazení plochy*</span><span class="sxs-lookup"><span data-stu-id="0bf25-440">*Link to switch to Desktop View*</span></span>

<span data-ttu-id="0bf25-441">K přepínači zobrazení používá novou funkci s názvem **přepsání prohlížeče**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-441">The view switcher uses a new feature called **Browser Overriding**.</span></span> <span data-ttu-id="0bf25-442">Tato funkce umožňuje aplikaci zacházet se žádostmi, jako kdyby kdyby přicházely z jiného prohlížeče (uživatelského agenta) než je ta, kterou ve skutečnosti přicházejí z.</span><span class="sxs-lookup"><span data-stu-id="0bf25-442">This feature lets your application treat requests as if they were coming from a different browser (user agent) than the one they are actually coming from.</span></span>

<span data-ttu-id="0bf25-443">V této úloze bude prozkoumat ukázkové implementace přepínači zobrazení přidal jQuery.Mobile.MVC a nový prohlížeč přepisování funkce v rozhraní ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="0bf25-443">In this task, you will explore the sample implementation of a view-switcher added by jQuery.Mobile.MVC and the new browser overriding features in ASP.NET MVC 4.</span></span>

1. <span data-ttu-id="0bf25-444">Přepněte zpátky na Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0bf25-444">Switch back to Visual Studio.</span></span>
2. <span data-ttu-id="0bf25-445">Otevřete  **\_Layout.Mobile.cshtml** zobrazení umístěná **Views\Shared** složky a Všimněte si komponentu přepínači zobrazení, který je odkazováno jako částečné zobrazení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-445">Open the **\_Layout.Mobile.cshtml** view located under the **Views\Shared** folder and notice the view-switcher component being referenced as a partial view.</span></span>

    <span data-ttu-id="0bf25-446">![Mobilní rozložení pomocí součásti přepínači zobrazení](whats-new-in-aspnet-mvc-4/_static/image29.png "mobilní rozložení pomocí součásti přepínači zobrazení")</span><span class="sxs-lookup"><span data-stu-id="0bf25-446">![Mobile layout using View-Switcher component](whats-new-in-aspnet-mvc-4/_static/image29.png "Mobile layout using View-Switcher component")</span></span>

    <span data-ttu-id="0bf25-447">*Mobilní rozložení pomocí součásti přepínači zobrazení*</span><span class="sxs-lookup"><span data-stu-id="0bf25-447">*Mobile layout using View-Switcher component*</span></span>
3. <span data-ttu-id="0bf25-448">Otevřete  **\_ViewSwitcher.cshtml** částečné zobrazení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-448">Open the **\_ViewSwitcher.cshtml** partial view.</span></span>

    <span data-ttu-id="0bf25-449">Částečné zobrazení používá nová metoda **ViewContext.HttpContext.GetOverriddenBrowser()** zobrazit na odpovídající odkaz přepnout buď zobrazení Desktop nebo Mobile a určení původu webového požadavku.</span><span class="sxs-lookup"><span data-stu-id="0bf25-449">The partial view uses the new method **ViewContext.HttpContext.GetOverriddenBrowser()** to determine the origin of the web request and show the corresponding link to switch either to the Desktop or Mobile views.</span></span>

    <span data-ttu-id="0bf25-450">**GetOverridenBrowser** metoda vrátí **HttpBrowserCapabilitiesBase** instance, která odpovídá uživatelský agent nastaveno pro požadavek (skutečné nebo přepsané).</span><span class="sxs-lookup"><span data-stu-id="0bf25-450">The **GetOverridenBrowser** method returns an **HttpBrowserCapabilitiesBase** instance that corresponds to the user agent currently set for the request (actual or overridden).</span></span> <span data-ttu-id="0bf25-451">Tuto hodnotu můžete získat vlastnosti, jako **IsMobileDevice**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-451">You can use this value to get properties such as **IsMobileDevice**.</span></span>

    <span data-ttu-id="0bf25-452">![Částečné zobrazení ViewSwitcher](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher částečné zobrazení")</span><span class="sxs-lookup"><span data-stu-id="0bf25-452">![ViewSwitcher partial view](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher partial view")</span></span>

    <span data-ttu-id="0bf25-453">*ViewSwitcher částečné zobrazení*</span><span class="sxs-lookup"><span data-stu-id="0bf25-453">*ViewSwitcher partial view*</span></span>
4. <span data-ttu-id="0bf25-454">Otevřete **ViewSwitcherController.cs** třída umístěný v **řadiče** složky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-454">Open the **ViewSwitcherController.cs** class located in the **Controllers** folder.</span></span> <span data-ttu-id="0bf25-455">Podívejte se na této funkci SwitchView akce je volána metodou odkaz v komponentě ViewSwitcher a Všimněte si nových metod položka HttpContext.</span><span class="sxs-lookup"><span data-stu-id="0bf25-455">Check out that SwitchView action is called by the link in the ViewSwitcher component, and notice the new HttpContext methods.</span></span>

    - <span data-ttu-id="0bf25-456">**HttpContext.ClearOverridenBrowser()** metoda odebere každého přepsaného uživatelského agenta pro aktuální požadavek.</span><span class="sxs-lookup"><span data-stu-id="0bf25-456">The **HttpContext.ClearOverridenBrowser()** method removes any overridden user agent for the current request.</span></span>
    - <span data-ttu-id="0bf25-457">**HttpContext.SetOverridenBrowser()** metoda přepíše hodnotu skutečného uživatelského agenta žádosti pomocí zadaného uživatelského agenta.</span><span class="sxs-lookup"><span data-stu-id="0bf25-457">The **HttpContext.SetOverridenBrowser()** method overrides the request's actual user agent value using the specified user agent.</span></span>  
        <span data-ttu-id="0bf25-458">![Řadič ViewSwitcher](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher řadiče")</span><span class="sxs-lookup"><span data-stu-id="0bf25-458">![ViewSwitcher Controller](whats-new-in-aspnet-mvc-4/_static/image31.png "ViewSwitcher Controller")</span></span>  
<span data-ttu-id="0bf25-459">*ViewSwitcher řadiče*</span><span class="sxs-lookup"><span data-stu-id="0bf25-459">*ViewSwitcher Controller*</span></span>

        <span data-ttu-id="0bf25-460">Přepíše prohlížeče je základní funkce ASP.NET MVC 4, což je také k dispozici i v případě, že nenainstalujete jQuery.Mobile.MVC balíčku.</span><span class="sxs-lookup"><span data-stu-id="0bf25-460">Browser Overriding is a core feature of ASP.NET MVC 4, which is also available even if you do not install the jQuery.Mobile.MVC package.</span></span> <span data-ttu-id="0bf25-461">Ale tato funkce ovlivňuje pouze zobrazení, rozložení a částečného zobrazení a neovlivní žádné funkce, které jsou závislé na Request.Browser objektu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-461">However, this feature affects only view, layout, and partial-view, and it does not affect any of the features that depend on the Request.Browser object.</span></span>

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a><span data-ttu-id="0bf25-462">Úloha 5 – Přidání k přepínači zobrazení v zobrazení plochy</span><span class="sxs-lookup"><span data-stu-id="0bf25-462">Task 5 - Adding the View-Switcher in the Desktop View</span></span>

<span data-ttu-id="0bf25-463">V této úloze aktualizujte plochy rozložení zahrnout k přepínači zobrazení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-463">In this task, you will update the desktop layout to include the view-switcher.</span></span> <span data-ttu-id="0bf25-464">To vám umožní mobilním uživatelům přejděte zpět na mobilní zobrazení při procházení zobrazení plochy.</span><span class="sxs-lookup"><span data-stu-id="0bf25-464">This will allow mobile users to go back to the mobile view when browsing the desktop view.</span></span>

1. <span data-ttu-id="0bf25-465">Aktualizujte lokality v **emulátoru Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-465">Refresh the site in the **Windows Phone Emulator**.</span></span>
2. <span data-ttu-id="0bf25-466">Klikněte na **zobrazení plochy** odkaz v horní části galerie.</span><span class="sxs-lookup"><span data-stu-id="0bf25-466">Click on the **Desktop view** link at the top of the gallery.</span></span> <span data-ttu-id="0bf25-467">Všimněte si, že v zobrazení plochy tak, aby umožnily že vrátíte na mobilní zobrazení žádné přepínači zobrazení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-467">Notice there is no view-switcher in the desktop view to allow you return to the mobile view.</span></span>
3. <span data-ttu-id="0bf25-468">Přejděte zpět na Visual Studio a otevřete  **\_Layout.cshtml** zobrazení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-468">Go back to Visual Studio and open the **\_Layout.cshtml** view.</span></span>
4. <span data-ttu-id="0bf25-469">Najít oddíl přihlášení a vložení volání k vykreslení  **\_ViewSwitcher** částečné zobrazení níže  **\_LogOnPartial** částečné zobrazení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-469">Find the login section and insert a call to render the **\_ViewSwitcher** partial view below the **\_LogOnPartial** partial view.</span></span> <span data-ttu-id="0bf25-470">Potom stiskněte klávesu **kombinaci kláves CTRL + S** a uložte změny.</span><span class="sxs-lookup"><span data-stu-id="0bf25-470">Then, press **CTRL + S** to save the changes.</span></span>


    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
5. <span data-ttu-id="0bf25-471">Stiskněte klávesu **kombinaci kláves CTRL + S** a uložte změny.</span><span class="sxs-lookup"><span data-stu-id="0bf25-471">Press **CTRL + S** to save the changes.</span></span>
6. <span data-ttu-id="0bf25-472">Aktualizujte stránku v emulátoru Windows Phone a dvakrát klikněte na obrazovce a přiblížení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-472">Refresh the page in the Windows Phone Emulator and double-click the screen to zoom in.</span></span> <span data-ttu-id="0bf25-473">Všimněte si, že nyní zobrazuje domovské stránce **mobilní zobrazení** odkaz, který přepíná z mobilních na zobrazení plochy.</span><span class="sxs-lookup"><span data-stu-id="0bf25-473">Notice that the home page now shows the **Mobile view** link that switches from mobile to desktop view.</span></span>

    <span data-ttu-id="0bf25-474">![Zobrazit v zobrazení plochy přepínači](whats-new-in-aspnet-mvc-4/_static/image32.png "přepínači zobrazení se zobrazují v zobrazení plochy")</span><span class="sxs-lookup"><span data-stu-id="0bf25-474">![View Switcher rendered in desktop view](whats-new-in-aspnet-mvc-4/_static/image32.png "View Switcher rendered in desktop view")</span></span>

    <span data-ttu-id="0bf25-475">*Přepínači zobrazení se zobrazují v zobrazení plochy*</span><span class="sxs-lookup"><span data-stu-id="0bf25-475">*View Switcher rendered in desktop view*</span></span>
7. <span data-ttu-id="0bf25-476">Přepněte do pohledu mobilní znovu a přejděte do **o** stránky (http://localhost [port] / Home/o).</span><span class="sxs-lookup"><span data-stu-id="0bf25-476">Switch to the Mobile view again and browse to **About** page (http://localhost[port]/Home/About).</span></span> <span data-ttu-id="0bf25-477">Všimněte si, že i v případě, že jste nevytvořili zobrazení About.Mobile.cshtml, o stránka se zobrazí pomocí mobilních rozložení (\_Layout.Mobile.cshtml).</span><span class="sxs-lookup"><span data-stu-id="0bf25-477">Notice that, even if you haven't created an About.Mobile.cshtml view, the About page is displayed using the mobile layout (\_Layout.Mobile.cshtml).</span></span>

    <span data-ttu-id="0bf25-478">![O stránku](whats-new-in-aspnet-mvc-4/_static/image33.png "o stránce")</span><span class="sxs-lookup"><span data-stu-id="0bf25-478">![About page](whats-new-in-aspnet-mvc-4/_static/image33.png "About page")</span></span>

    <span data-ttu-id="0bf25-479">*O stránku*</span><span class="sxs-lookup"><span data-stu-id="0bf25-479">*About page*</span></span>
8. <span data-ttu-id="0bf25-480">Nakonec otevřete web ve webovém prohlížeči klientů.</span><span class="sxs-lookup"><span data-stu-id="0bf25-480">Finally, open the site in a desktop Web browser.</span></span> <span data-ttu-id="0bf25-481">Všimněte si, že žádnou z předchozích aktualizací ovlivnil zobrazení plochy.</span><span class="sxs-lookup"><span data-stu-id="0bf25-481">Notice that none of the previous updates has affected the desktop view.</span></span>

    <span data-ttu-id="0bf25-482">![Zobrazení plochy Fotogalerie](whats-new-in-aspnet-mvc-4/_static/image34.png "Fotogalerie zobrazení plochy")</span><span class="sxs-lookup"><span data-stu-id="0bf25-482">![PhotoGallery desktop view](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery desktop view")</span></span>

    <span data-ttu-id="0bf25-483">*Zobrazení plochy Fotogalerie*</span><span class="sxs-lookup"><span data-stu-id="0bf25-483">*PhotoGallery desktop view*</span></span>

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a><span data-ttu-id="0bf25-484">Úloha 6 – Vytvoření nové režimy zobrazení</span><span class="sxs-lookup"><span data-stu-id="0bf25-484">Task 6 - Creating New Display Modes</span></span>

<span data-ttu-id="0bf25-485">Nová funkce režimy zobrazení umožňuje aplikaci, vyberte zobrazení v závislosti na prohlížeči, který vytváří žádosti.</span><span class="sxs-lookup"><span data-stu-id="0bf25-485">The new display modes feature lets an application select views depending on the browser that is generating the request.</span></span> <span data-ttu-id="0bf25-486">Například pokud prohlížeč pro stolní počítač požadavky na domovskou stránku, aplikace se vrátit **Views\Home\Index.cshtml** šablony.</span><span class="sxs-lookup"><span data-stu-id="0bf25-486">For example, if a desktop browser requests the Home page, the application will return the **Views\Home\Index.cshtml** template.</span></span> <span data-ttu-id="0bf25-487">Pokud prohlížeč pro mobilní zařízení požadavky na domovskou stránku, aplikace se vrátíte **Views\Home\Index.mobile.cshtml** šablony.</span><span class="sxs-lookup"><span data-stu-id="0bf25-487">Then, if a mobile browser requests the Home page, the application will return the **Views\Home\Index.mobile.cshtml** template.</span></span>

<span data-ttu-id="0bf25-488">V této úloze se vytvoří vlastní rozložení pro zařízení iPhone a bude mít k simulaci požadavky ze zařízení iPhone.</span><span class="sxs-lookup"><span data-stu-id="0bf25-488">In this task, you will create a customized layout for iPhone devices, and you will have to simulate requests from iPhone devices.</span></span> <span data-ttu-id="0bf25-489">K tomuto účelu můžete použít buď emulátoru nebo simulátor pro zařízení iPhone (jako je [Electric Mobile simulátoru](http://www.electricplum.com/)) nebo prohlížeči s doplňků, které upravit uživatelský agent.</span><span class="sxs-lookup"><span data-stu-id="0bf25-489">To do this, you can use either an iPhone emulator/simulator (like [Electric Mobile Simulator](http://www.electricplum.com/)) or a browser with add-ons that modify the user agent.</span></span> <span data-ttu-id="0bf25-490">Pokyny k nastavení řetězec uživatelského agenta v prohlížeči Safari emulovat zařízení typu iPhone najdete v tématu [jak umožníte Safari předstírají, že je aplikace Internet Explorer](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) v blogu David Alison.</span><span class="sxs-lookup"><span data-stu-id="0bf25-490">For instructions on how to set the user agent string in an Safari browser to emulate an iPhone, see [How to let Safari pretend it's IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) in David Alison's blog.</span></span>

<span data-ttu-id="0bf25-491">**Všimněte si, že tato úloha je volitelný a může pokračovat v testovacím prostředí bez její provedení.**</span><span class="sxs-lookup"><span data-stu-id="0bf25-491">**Notice that this task is optional and you can continue throughout the lab without executing it.**</span></span>

1. <span data-ttu-id="0bf25-492">V sadě Visual Studio, stiskněte klávesu **SHIFT** + **F5** Zastavit ladění aplikace.</span><span class="sxs-lookup"><span data-stu-id="0bf25-492">In Visual Studio, press **SHIFT** + **F5** to stop debugging the application.</span></span>
2. <span data-ttu-id="0bf25-493">Otevřete **Global.asax.cs** a přidejte následující příkaz using.</span><span class="sxs-lookup"><span data-stu-id="0bf25-493">Open **Global.asax.cs** and add the following using statement.</span></span>


    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
3. <span data-ttu-id="0bf25-494">Přidejte následující zvýrazněný kód do aplikace\_Start – metoda.</span><span class="sxs-lookup"><span data-stu-id="0bf25-494">Add the following highlighted code into the Application\_Start method.</span></span>

    <span data-ttu-id="0bf25-495">(Code fragment kódu - *ASP.NET MVC 4 laboratoř - Ex03 - iPhone DisplayMode*)</span><span class="sxs-lookup"><span data-stu-id="0bf25-495">(Code Snippet - *ASP.NET MVC 4 Lab - Ex03 - iPhone DisplayMode*)</span></span>


    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

    <span data-ttu-id="0bf25-496">Jste si zaregistrovali nový **DefaultDisplayMode s názvem &quot;iPhone&quot;**, v rámci statických **DisplayModeProvider.Instance.Modes** statický seznam, který bude porovnání každého příchozího požadavku.</span><span class="sxs-lookup"><span data-stu-id="0bf25-496">You have registered a new **DefaultDisplayMode named &quot;iPhone&quot;**, within the static **DisplayModeProvider.Instance.Modes** static list, that will be matched against each incoming request.</span></span> <span data-ttu-id="0bf25-497">Pokud příchozí požadavek obsahuje řetězec &quot;iPhone&quot;, ASP.NET MVC najdete zobrazení, jehož název obsahovat &quot;iPhone&quot; příponu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-497">If the incoming request contains the string &quot;iPhone&quot;, ASP.NET MVC will find the views whose name contain the &quot;iPhone&quot; suffix.</span></span> <span data-ttu-id="0bf25-498">Parametr 0 označuje, jak konkrétní je nový režim; Toto zobrazení je pro instanci podrobnější než Obecné &quot;.mobile&quot; pravidlo, které odpovídá požadavky z mobilních zařízení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-498">The 0 parameter indicates how specific is the new mode; for instance, this view is more specific than the general &quot;.mobile&quot; rule that matches requests from mobile devices.</span></span>

    <span data-ttu-id="0bf25-499">Po spuštění tohoto kódu, pokud iPhone prohlížeči vygeneruje žádost, vaše aplikace bude používat **Views\Shared\\_Layout.iPhone.cshtml** rozložení vytvoříte v dalších krocích.</span><span class="sxs-lookup"><span data-stu-id="0bf25-499">After this code runs, when an iPhone browser generates a request, your application will use the **Views\Shared\\_Layout.iPhone.cshtml** layout you will create in the next steps.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0bf25-500">Tímto způsobem testování požadavku pro iPhone je jednodušší pro účely ukázky a nemusí fungovat podle očekávání pro každý řetězec uživatelského agenta iPhone (pro testovací příklad je malá a velká písmena).</span><span class="sxs-lookup"><span data-stu-id="0bf25-500">This way of testing the request for iPhone has been simplified for demo purposes and might not work as expected for every iPhone user agent string (for example test is case sensitive).</span></span>
4. <span data-ttu-id="0bf25-501">Vytvořit kopii  **\_Layout.Mobile.cshtml** v soubor **Views\Shared** složku a přejmenujte kopírovat do &quot;  **\_Layout.iPhone.csthml** &quot;.</span><span class="sxs-lookup"><span data-stu-id="0bf25-501">Create a copy of the **\_Layout.Mobile.cshtml** file in the **Views\Shared** folder and rename the copy to &quot;**\_Layout.iPhone.csthml**&quot;.</span></span>
5. <span data-ttu-id="0bf25-502">Otevřete  **\_Layout.iPhone.csthml** jste vytvořili v předchozím kroku.</span><span class="sxs-lookup"><span data-stu-id="0bf25-502">Open **\_Layout.iPhone.csthml** you created in the previous step.</span></span>
6. <span data-ttu-id="0bf25-503">Najít div element s atribut data-role nastaven na **stránky** a změňte **data-theme** atribut &quot; **a**&quot;.</span><span class="sxs-lookup"><span data-stu-id="0bf25-503">Find the div element with the data-role attribute set to **page** and change the **data-theme** attribute to &quot;**a**&quot;.</span></span>


    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

    <span data-ttu-id="0bf25-504">Nyní máte 3 rozložení v aplikaci ASP.NET MVC 4:</span><span class="sxs-lookup"><span data-stu-id="0bf25-504">Now you have 3 layouts in your ASP.NET MVC 4 application:</span></span>

    1. <span data-ttu-id="0bf25-505">**\_Layout.cshtml**: výchozí rozložení použít u stolních počítačů.</span><span class="sxs-lookup"><span data-stu-id="0bf25-505">**\_Layout.cshtml**: default layout used for desktop browsers.</span></span>
    2. <span data-ttu-id="0bf25-506">**\_Layout.Mobile.cshtml**: výchozí rozložení se používá pro mobilní zařízení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-506">**\_Layout.mobile.cshtml**: default layout used for mobile devices.</span></span>
    3. <span data-ttu-id="0bf25-507">**\_Layout.iPhone.cshtml**: konkrétní rozložení pro zařízení iPhone, pomocí jiné barevné schéma k odlišení od \_Layout.mobile.cshtml.</span><span class="sxs-lookup"><span data-stu-id="0bf25-507">**\_Layout.iPhone.cshtml**: specific layout for iPhone devices, using a different color scheme to differentiate from \_Layout.mobile.cshtml.</span></span>
7. <span data-ttu-id="0bf25-508">Stiskněte klávesu **F5** ke spuštění aplikace a přejděte do lokality v **emulátoru Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-508">Press **F5** to run the application and browse the site in the **Windows Phone Emulator**.</span></span>
8. <span data-ttu-id="0bf25-509">Otevřete **iPhone simulátoru** (najdete v části [příloha C](#AppendixC) pokyny o tom, jak nainstalovat a nakonfigurovat simulátor pro zařízení iPhone) a přejděte na web příliš.</span><span class="sxs-lookup"><span data-stu-id="0bf25-509">Open an **iPhone simulator** (see [Appendix C](#AppendixC) for instructions on how to install and configure an iPhone simulator), and browse to the site too.</span></span> <span data-ttu-id="0bf25-510">Všimněte si, že každý phone používá konkrétní šablonu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-510">Notice that each phone is using the specific template.</span></span>

    ![Using-different-views-for-each-Mobile-device2](whats-new-in-aspnet-mvc-4/_static/image35.png)

    <span data-ttu-id="0bf25-512">*Použití různých zobrazení pro každý mobilní zařízení*</span><span class="sxs-lookup"><span data-stu-id="0bf25-512">*Using different views for each mobile device*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a><span data-ttu-id="0bf25-513">Cvičení 4: Použití asynchronní řadičů</span><span class="sxs-lookup"><span data-stu-id="0bf25-513">Exercise 4: Using Asynchronous Controllers</span></span>

<span data-ttu-id="0bf25-514">Rozhraní Microsoft .NET Framework 4.5 zavádí nové jazykové funkce v C# a Visual Basic zajistit nové platformu pro asynchrony v .NET – programování.</span><span class="sxs-lookup"><span data-stu-id="0bf25-514">Microsoft .NET Framework 4.5 introduces new language features in C# and Visual Basic to provide a new foundation for asynchrony in .NET programming.</span></span> <span data-ttu-id="0bf25-515">Tento nový foundation umožňuje asynchronní programování podobná - a o stejně jednoduché jako - synchronní programování.</span><span class="sxs-lookup"><span data-stu-id="0bf25-515">This new foundation makes asynchronous programming similar to - and about as straightforward as - synchronous programming.</span></span> <span data-ttu-id="0bf25-516">Je nyní možné zapisovat pomocí metody asynchronní akce v architektuře ASP.NET MVC 4 **AsyncController** třídy.</span><span class="sxs-lookup"><span data-stu-id="0bf25-516">You are now able to write asynchronous action methods in ASP.NET MVC 4 by using the **AsyncController** class.</span></span> <span data-ttu-id="0bf25-517">Můžete použít asynchronní akce metody pro dlouhodobé, bez procesoru vázaný požadavky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-517">You can use asynchronous action methods for long-running, non-CPU bound requests.</span></span> <span data-ttu-id="0bf25-518">Tím je zabráněno blokování webový server z provede práci během zpracování požadavku.</span><span class="sxs-lookup"><span data-stu-id="0bf25-518">This avoids blocking the Web server from performing work while the request is being processed.</span></span> <span data-ttu-id="0bf25-519">Třída AsyncController se obvykle používá pro dlouhodobé volání webové služby.</span><span class="sxs-lookup"><span data-stu-id="0bf25-519">The AsyncController class is typically used for long-running Web service calls.</span></span>

<span data-ttu-id="0bf25-520">Tento postup vysvětluje základy asynchronní operace v rozhraní ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="0bf25-520">This exercise explains the basics of asynchronous operation in ASP.NET MVC 4.</span></span> <span data-ttu-id="0bf25-521">Pokud chcete o podrobnější prohlídku, můžete najdete v následujícím článku: [ [https://msdn.microsoft.com/en-us/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/en-us/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/en-us/library/ee728598%28v=vs.100%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="0bf25-521">If you want a deeper dive, you can check out the following article: [[https://msdn.microsoft.com/en-us/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/en-us/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/en-us/library/ee728598%28v=vs.100%29.aspx)</span></span>

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a><span data-ttu-id="0bf25-522">Úloha 1 – implementace asynchronní kontroler</span><span class="sxs-lookup"><span data-stu-id="0bf25-522">Task 1 - Implementing an Asynchronous Controller</span></span>

1. <span data-ttu-id="0bf25-523">Otevřete **začít** řešení nacházející se v **zdroj/Ex4-asynchronní/počáteční/** složky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-523">Open the **Begin** solution located at **Source/Ex4-Async/Begin/** folder.</span></span> <span data-ttu-id="0bf25-524">Jinak, může pokračovat, pomocí **End** řešení získat provedením předchozím cvičení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-524">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

    1. <span data-ttu-id="0bf25-525">Pokud jste otevřeli poskytnutého **začít** řešení, budete muset stáhnout některé chybějící balíčky NuGet než budete pokračovat.</span><span class="sxs-lookup"><span data-stu-id="0bf25-525">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="0bf25-526">Chcete-li to provést, klikněte na tlačítko **projektu** nabídku a vyberte **spravovat balíčky NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-526">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="0bf25-527">V **spravovat balíčky NuGet** dialogové okno, klikněte na tlačítko **obnovení** Chcete-li stáhnout chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-527">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
    3. <span data-ttu-id="0bf25-528">Nakonec sestavte řešení kliknutím **sestavení** | **sestavit řešení**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-528">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0bf25-529">Jednou z výhod použití NuGet je, že nemáte pro odeslání všech knihoven v projektu, zmenšení velikosti projektu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-529">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="0bf25-530">Napájení nástroje NuGet zadáním verze balíčku v souboru Packages.config, nebudete moct stáhnout všechny požadované knihovny při prvním spuštění projektu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-530">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="0bf25-531">Z tohoto důvodu je nutné provést tyto kroky po otevření existujícího řešení z tohoto testovacího prostředí.</span><span class="sxs-lookup"><span data-stu-id="0bf25-531">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="0bf25-532">Otevřete **HomeController.cs** třídy z **řadiče** složky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-532">Open the **HomeController.cs** class from the **Controllers** folder.</span></span>
3. <span data-ttu-id="0bf25-533">Přidejte následující příkaz using.</span><span class="sxs-lookup"><span data-stu-id="0bf25-533">Add the following using statement.</span></span>


    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
4. <span data-ttu-id="0bf25-534">Aktualizace **HomeController** třídy dědí **AsyncController**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-534">Update the **HomeController** class to inherit from **AsyncController**.</span></span> <span data-ttu-id="0bf25-535">Řadiče, které jsou odvozeny od AsyncController povolit technologii ASP.NET pro zpracování asynchronní požadavky a mohou stále metody synchronní akce služby.</span><span class="sxs-lookup"><span data-stu-id="0bf25-535">Controllers that derive from AsyncController enable ASP.NET to process asynchronous requests, and they can still service synchronous action methods.</span></span>


    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
5. <span data-ttu-id="0bf25-536">Přidat **asynchronní** – klíčové slovo k **Index** metoda a nastavit jej vrátí typ **úloh&lt;ActionResult&gt;**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-536">Add the **async** keyword to the **Index** method and make it return the type **Task&lt;ActionResult&gt;**.</span></span>


    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

    > [!NOTE]
    > <span data-ttu-id="0bf25-537">**Asynchronní** – klíčové slovo je jednou z nových klíčových slov rozhraní .NET Framework 4.5 poskytuje; říká kompilátoru, že tato metoda obsahuje asynchronní kód.</span><span class="sxs-lookup"><span data-stu-id="0bf25-537">The **async** keyword is one of the new keywords the .NET Framework 4.5 provides; it tells the compiler that this method contains asynchronous code.</span></span> <span data-ttu-id="0bf25-538">A **úloh** objekt představuje asynchronní operaci, kterou může dokončit v určitém okamžiku v budoucnu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-538">A **Task** object represents an asynchronous operation that may complete at some point in the future.</span></span>
6. <span data-ttu-id="0bf25-539">Nahraďte **klienta. GetAsync()** volání s použitím verze úplné asynchronní – klíčové slovo await, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="0bf25-539">Replace the **client.GetAsync()** call with the full async version using await keyword as shown below.</span></span>

    <span data-ttu-id="0bf25-540">(Code fragment kódu - *architektury ASP.NET MVC 4 laboratoř - Ex04 - GetAsync*)</span><span class="sxs-lookup"><span data-stu-id="0bf25-540">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - GetAsync*)</span></span>


    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

    > [!NOTE]
    > <span data-ttu-id="0bf25-541">V předchozí verzi, jste používali **výsledek** vlastnost z **úloh** objekt, který chcete blokovat vlákno, dokud vrácením výsledku (verzi služby sync).</span><span class="sxs-lookup"><span data-stu-id="0bf25-541">In the previous version, you were using the **Result** property from the **Task** object to block the thread until the result is returned (sync version).</span></span>
    > 
    > <span data-ttu-id="0bf25-542">Přidávání **await** – klíčové slovo říká kompilátoru asynchronně čekání úlohy vrácená z volání metody.</span><span class="sxs-lookup"><span data-stu-id="0bf25-542">Adding the **await** keyword tells the compiler to asynchronously wait for the task returned from the method call.</span></span> <span data-ttu-id="0bf25-543">To znamená, že zbytek kód bude proveden jako zpětné volání pouze po dokončení awaited metoda.</span><span class="sxs-lookup"><span data-stu-id="0bf25-543">This means that the rest of the code will be executed as a callback only after the awaited method completes.</span></span> <span data-ttu-id="0bf25-544">Jiné si všimněte je, že není potřeba změnit vaše bloku try-catch – aby bylo možné tento pracovní: výjimky, které dojít pozadí nebo v popředí stále vzniká, bez další zátěže pomocí poskytované rozhraní framework obslužnou rutinu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-544">Another thing to notice is that you do not need to change your try-catch block in order to make this work: the exceptions that happen in background or in foreground will still be caught without any extra work using a handler provided by the framework.</span></span>
7. <span data-ttu-id="0bf25-545">Změnit kód pokračujte s asynchronní implementace nahrazením řádky s novým kódem, jak je uvedeno níže</span><span class="sxs-lookup"><span data-stu-id="0bf25-545">Change the code to continue with the asynchronous implementation by replacing the lines with the new code as shown below</span></span>

    <span data-ttu-id="0bf25-546">(Code fragment kódu - *architektury ASP.NET MVC 4 laboratoř - Ex04 - ReadAsStringAsync*)</span><span class="sxs-lookup"><span data-stu-id="0bf25-546">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - ReadAsStringAsync*)</span></span>


    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
8. <span data-ttu-id="0bf25-547">Spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="0bf25-547">Run the application.</span></span> <span data-ttu-id="0bf25-548">Všimnete si žádné větší změny, ale váš kód nebude blokování vlákna z fondu podprocesů Příprava lepší využití serverových prostředků a zlepšení výkonu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-548">You will notice no major changes, but your code will not block a thread from the thread pool making a better usage of the server resources and improving performance.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0bf25-549">Další informace o nových funkcích asynchronního programování v testovacím prostředí &quot; **asynchronní programování v rozhraní .NET 4.5 s C# a Visual Basic** &quot; zahrnuté v sadě Visual Studio školení Kit.</span><span class="sxs-lookup"><span data-stu-id="0bf25-549">You can learn more about the new asynchronous programming features in the lab &quot;**Asynchronous Programming in .NET 4.5 with C# and Visual Basic**&quot; included in the Visual Studio Training Kit.</span></span>

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a><span data-ttu-id="0bf25-550">Úloha 2 – zpracování vypršení časových limitů s zrušení tokenů</span><span class="sxs-lookup"><span data-stu-id="0bf25-550">Task 2 - Handling Time-Outs with Cancellation Tokens</span></span>

<span data-ttu-id="0bf25-551">Asynchronní akce metody, které vracejí instance úloh může také podporovat vypršení časových limitů.</span><span class="sxs-lookup"><span data-stu-id="0bf25-551">Asynchronous action methods that return Task instances can also support time-outs.</span></span> <span data-ttu-id="0bf25-552">V této úloze aktualizujte kód metoda Index pro zpracování časový limit scénář používající token zrušení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-552">In this task, you will update the Index method code to handle a time-out scenario using a cancellation token.</span></span>

1. <span data-ttu-id="0bf25-553">Přejděte zpět na Visual Studio a stiskněte klávesu **SHIFT + F5** Zastavit ladění.</span><span class="sxs-lookup"><span data-stu-id="0bf25-553">Go back to Visual Studio and press **SHIFT + F5** to stop debugging.</span></span>
2. <span data-ttu-id="0bf25-554">Přidejte následující příkaz k použití **HomeController.cs** souboru.</span><span class="sxs-lookup"><span data-stu-id="0bf25-554">Add the following using statement to the **HomeController.cs** file.</span></span>


    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
3. <span data-ttu-id="0bf25-555">Akce indexu přijímat aktualizace **CancellationToken** argument.</span><span class="sxs-lookup"><span data-stu-id="0bf25-555">Update the Index action to receive a **CancellationToken** argument.</span></span>


    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
4. <span data-ttu-id="0bf25-556">Aktualizace **GetAsync** volání předat token zrušení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-556">Update the **GetAsync** call to pass the cancellation token.</span></span>

    <span data-ttu-id="0bf25-557">(Code fragment kódu - *SendAsync laboratoř - Ex04 - architektury ASP.NET MVC 4 s CancellationToken*)</span><span class="sxs-lookup"><span data-stu-id="0bf25-557">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - SendAsync with CancellationToken*)</span></span>


    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
5. <span data-ttu-id="0bf25-558">Uspořádání *Index* metoda s **hodnota vlastnosti AsyncTimeout** atributu nastavena na 500 milisekund a **HandleError** atributu nakonfigurovaného pro zpracování  **TaskCanceledException** přesměrováním na **TimedOut** zobrazení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-558">Decorate the *Index* method with an **AsyncTimeout** attribute set to 500 milliseconds and a **HandleError** attribute configured to handle **TaskCanceledException** by redirecting to a **TimedOut** view.</span></span>

    <span data-ttu-id="0bf25-559">(Code fragment kódu - *atributy architektury ASP.NET MVC 4 laboratoř - Ex04 -*)</span><span class="sxs-lookup"><span data-stu-id="0bf25-559">(Code Snippet - *ASP.NET MVC 4 Lab - Ex04 - Attributes*)</span></span>


    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
6. <span data-ttu-id="0bf25-560">Otevřete **PhotoController** třídy a aktualizace **Galerie** metoda zpoždění spuštění 1000 miliseconds (1 sekunda) simulovat dlouhotrvající úlohy.</span><span class="sxs-lookup"><span data-stu-id="0bf25-560">Open the **PhotoController** class and update the **Gallery** method to delay the execution 1000 miliseconds (1 second) to simulate a long running task.</span></span>


    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
7. <span data-ttu-id="0bf25-561">Otevřete **Web.config** souboru a povolit vlastní chyby přidáním následující element.</span><span class="sxs-lookup"><span data-stu-id="0bf25-561">Open the **Web.config** file and enable custom errors by adding the following element.</span></span>


    [!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
8. <span data-ttu-id="0bf25-562">Vytvořit nové zobrazení v **Views\Shared** s názvem **TimedOut** a použít výchozí rozložení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-562">Create a new view in **Views\Shared** named **TimedOut** and use the default layout.</span></span> <span data-ttu-id="0bf25-563">V Průzkumníku řešení klikněte pravým tlačítkem myši **Views\Shared** složky a vyberte **přidat | Zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-563">In the Solution Explorer, right-click the **Views\Shared** folder and select **Add | View**.</span></span>

    <span data-ttu-id="0bf25-564">![Pro každé mobilních zařízení pomocí různých zobrazení](whats-new-in-aspnet-mvc-4/_static/image36.png "použití různých zobrazení pro každý mobilní zařízení")</span><span class="sxs-lookup"><span data-stu-id="0bf25-564">![Using different views for each mobile device](whats-new-in-aspnet-mvc-4/_static/image36.png "Using different views for each mobile device")</span></span>

    <span data-ttu-id="0bf25-565">*Použití různých zobrazení pro každý mobilní zařízení*</span><span class="sxs-lookup"><span data-stu-id="0bf25-565">*Using different views for each mobile device*</span></span>
9. <span data-ttu-id="0bf25-566">Aktualizace **TimedOut** zobrazit obsah, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="0bf25-566">Update the **TimedOut** view content as shown below.</span></span>


    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
10. <span data-ttu-id="0bf25-567">Spusťte aplikaci a přejděte do adresy URL kořenového adresáře.</span><span class="sxs-lookup"><span data-stu-id="0bf25-567">Run the application and navigate to the root URL.</span></span> <span data-ttu-id="0bf25-568">Jak jste přidali **Thread.Sleep** na 1000 milisekund, budete mít k vypršení časového limitu, generovaných **hodnota vlastnosti AsyncTimeout** atribut a catch podle **HandleError** atribut.</span><span class="sxs-lookup"><span data-stu-id="0bf25-568">As you have added a **Thread.Sleep** of 1000 milliseconds, you will get a time-out error, generated by the **AsyncTimeout** attribute and catch by the **HandleError** attribute.</span></span>

    <span data-ttu-id="0bf25-569">![Časový limit výjimka zpracovává](whats-new-in-aspnet-mvc-4/_static/image37.png "zpracovává výjimka časového limitu")</span><span class="sxs-lookup"><span data-stu-id="0bf25-569">![Time-out exception handled](whats-new-in-aspnet-mvc-4/_static/image37.png "Time-out exception handled")</span></span>

    <span data-ttu-id="0bf25-570">*Časový limit výjimka zpracovává*</span><span class="sxs-lookup"><span data-stu-id="0bf25-570">*Time-out exception handled*</span></span>

> [!NOTE]
> <span data-ttu-id="0bf25-571">Kromě toho můžete nasadit tuto aplikaci do následující weby systému Windows Azure [Dodatek D: publikování aplikace ASP.NET MVC 4 pomocí nástroje nasazení webu](#AppendixD).</span><span class="sxs-lookup"><span data-stu-id="0bf25-571">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixD).</span></span>


<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="0bf25-572">Souhrn</span><span class="sxs-lookup"><span data-stu-id="0bf25-572">Summary</span></span>

<span data-ttu-id="0bf25-573">V tomto hands-na-testovacím prostředí můžete jsme zaznamenali, některé z nových funkcí v architektuře ASP.NET MVC 4 trvalé.</span><span class="sxs-lookup"><span data-stu-id="0bf25-573">In this hands-on-lab, you've observed some of the new features resident in ASP.NET MVC 4.</span></span> <span data-ttu-id="0bf25-574">Projednat následující koncepty:</span><span class="sxs-lookup"><span data-stu-id="0bf25-574">The following concepts have been discussed:</span></span>

- <span data-ttu-id="0bf25-575">Využívat výhod rozšíření, která chcete šablony včetně projektu ASP.NET MVC šabloně nový projekt mobilních aplikací</span><span class="sxs-lookup"><span data-stu-id="0bf25-575">Take advantage of the enhancements to the ASP.NET MVC project templates-including the new mobile application project template</span></span>
- <span data-ttu-id="0bf25-576">Pomocí zobrazení atributů jazyka HTML5 a dotazy na média šablon stylů CSS ke zlepšení zobrazení na mobilních zařízeních</span><span class="sxs-lookup"><span data-stu-id="0bf25-576">Use the HTML5 viewport attribute and CSS media queries to improve the display on mobile devices</span></span>
- <span data-ttu-id="0bf25-577">Pro progresivní vylepšení a vytváření dotykovým webového uživatelského rozhraní použijte jQuery Mobile</span><span class="sxs-lookup"><span data-stu-id="0bf25-577">Use jQuery Mobile for progressive enhancements and for building touch-optimized web UI</span></span>
- <span data-ttu-id="0bf25-578">Vytvoření mobilní konkrétní zobrazení</span><span class="sxs-lookup"><span data-stu-id="0bf25-578">Create mobile-specific views</span></span>
- <span data-ttu-id="0bf25-579">Používání komponent přepínači zobrazení lze přepínat mezi mobilních a desktopových zobrazení v aplikaci</span><span class="sxs-lookup"><span data-stu-id="0bf25-579">Use the view-switcher component to toggle between mobile and desktop views in the application</span></span>
- <span data-ttu-id="0bf25-580">Vytvořte asynchronní řadičů pomocí úloh podpory</span><span class="sxs-lookup"><span data-stu-id="0bf25-580">Create asynchronous controllers using task support</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a><span data-ttu-id="0bf25-581">Příloha A: používání fragmentů kódu</span><span class="sxs-lookup"><span data-stu-id="0bf25-581">Appendix A: Using Code Snippets</span></span>

<span data-ttu-id="0bf25-582">S fragmenty kódu máte všechny kód, který je nutné na dosah ruky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-582">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="0bf25-583">Dokument testovacího prostředí vás bude informovat přesně Pokud můžete, jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="0bf25-583">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="0bf25-584">![Používání fragmentů kódu v sadě Visual Studio pro vložení kódu do projektu](whats-new-in-aspnet-mvc-4/_static/image38.png "fragmenty kódu pomocí sady Visual Studio pro vložení kódu do projektu")</span><span class="sxs-lookup"><span data-stu-id="0bf25-584">![Using Visual Studio code snippets to insert code into your project](whats-new-in-aspnet-mvc-4/_static/image38.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="0bf25-585">*Používání fragmentů kódu v sadě Visual Studio pro vložení kódu do projektu*</span><span class="sxs-lookup"><span data-stu-id="0bf25-585">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="0bf25-586">***Chcete-li přidat fragment kódu pomocí klávesnice (C# pouze)***</span><span class="sxs-lookup"><span data-stu-id="0bf25-586">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="0bf25-587">Umístěte kurzor, kam chcete vložit kód.</span><span class="sxs-lookup"><span data-stu-id="0bf25-587">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="0bf25-588">Začněte psát název fragmentu kódu (bez mezery nebo spojovníky).</span><span class="sxs-lookup"><span data-stu-id="0bf25-588">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="0bf25-589">Podívejte se na jako IntelliSense zobrazí odpovídající fragmenty názvy.</span><span class="sxs-lookup"><span data-stu-id="0bf25-589">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="0bf25-590">Vyberte správný fragment kódu (nebo ponechte zadáním dokud je vybraný název celý fragmentu).</span><span class="sxs-lookup"><span data-stu-id="0bf25-590">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="0bf25-591">Stisknutím klávesy Tab dvakrát můžete vložit fragment v umístění kurzoru.</span><span class="sxs-lookup"><span data-stu-id="0bf25-591">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="0bf25-592">![Začněte psát název fragmentu](whats-new-in-aspnet-mvc-4/_static/image39.png "začněte psát název fragmentu kódu")</span><span class="sxs-lookup"><span data-stu-id="0bf25-592">![Start typing the snippet name](whats-new-in-aspnet-mvc-4/_static/image39.png "Start typing the snippet name")</span></span>

<span data-ttu-id="0bf25-593">*Začněte psát název fragmentu kódu*</span><span class="sxs-lookup"><span data-stu-id="0bf25-593">*Start typing the snippet name*</span></span>

<span data-ttu-id="0bf25-594">![Stisknutím klávesy Tab vyberte fragmentu zvýrazněná](whats-new-in-aspnet-mvc-4/_static/image40.png "stisknutím klávesy Tab vyberte zvýrazněný fragmentu kódu")</span><span class="sxs-lookup"><span data-stu-id="0bf25-594">![Press Tab to select the highlighted snippet](whats-new-in-aspnet-mvc-4/_static/image40.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="0bf25-595">*Stisknutím klávesy Tab vyberte zvýrazněný fragmentu kódu*</span><span class="sxs-lookup"><span data-stu-id="0bf25-595">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="0bf25-596">![Stisknutím klávesy Tab znovu a fragmentu rozšíří](whats-new-in-aspnet-mvc-4/_static/image41.png "stisknutím klávesy Tab znovu a fragmentu bude rozšiřovat.")</span><span class="sxs-lookup"><span data-stu-id="0bf25-596">![Press Tab again and the snippet will expand](whats-new-in-aspnet-mvc-4/_static/image41.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="0bf25-597">*Stisknutím klávesy Tab znovu a fragmentu bude rozšiřovat.*</span><span class="sxs-lookup"><span data-stu-id="0bf25-597">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="0bf25-598">***Chcete-li přidat fragment kódu pomocí myši (C#, Visual Basic a XML)***</span><span class="sxs-lookup"><span data-stu-id="0bf25-598">***To add a code snippet using the mouse (C#, Visual Basic and XML)***</span></span>

1. <span data-ttu-id="0bf25-599">Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-599">Right-click where you want to insert the code snippet.</span></span>
2. <span data-ttu-id="0bf25-600">Vyberte **Vložit fragment** následuje **Moje fragmenty kódu**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-600">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
3. <span data-ttu-id="0bf25-601">Vyberte relevantní fragment kódu ze seznamu, kliknutím na.</span><span class="sxs-lookup"><span data-stu-id="0bf25-601">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="0bf25-602">![Klikněte pravým tlačítkem, kam chcete vložit fragment kódu a vyberte Vložit fragment](whats-new-in-aspnet-mvc-4/_static/image42.png "klikněte pravým tlačítkem, kam chcete vložit fragment kódu a vyberte Vložit fragment")</span><span class="sxs-lookup"><span data-stu-id="0bf25-602">![Right-click where you want to insert the code snippet and select Insert Snippet](whats-new-in-aspnet-mvc-4/_static/image42.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="0bf25-603">*Klikněte pravým tlačítkem myši, kam chcete vložit fragment kódu a vyberte Vložit fragment*</span><span class="sxs-lookup"><span data-stu-id="0bf25-603">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="0bf25-604">![Vyberte relevantní fragment kódu ze seznamu, kliknutím na](whats-new-in-aspnet-mvc-4/_static/image43.png "vyberte relevantní fragment kódu ze seznamu, kliknutím na")</span><span class="sxs-lookup"><span data-stu-id="0bf25-604">![Pick the relevant snippet from the list, by clicking on it](whats-new-in-aspnet-mvc-4/_static/image43.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="0bf25-605">*Vyberte relevantní fragment kódu ze seznamu, kliknutím na*</span><span class="sxs-lookup"><span data-stu-id="0bf25-605">*Pick the relevant snippet from the list, by clicking on it*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="0bf25-606">Příloha B: instalaci sady Visual Studio Express 2012 pro Web</span><span class="sxs-lookup"><span data-stu-id="0bf25-606">Appendix B: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="0bf25-607">Můžete nainstalovat **Microsoft Visual Studio Express 2012 pro Web** nebo jiný &quot;Express&quot; pomocí verze  **[instalačního programu webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** .</span><span class="sxs-lookup"><span data-stu-id="0bf25-607">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="0bf25-608">Následující pokyny vás provede kroky potřebné k instalaci *Visual studio Express 2012 pro Web* pomocí *instalačního programu webové platformy Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="0bf25-608">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="0bf25-609">Přejděte na [ [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="0bf25-609">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="0bf25-610">Případně, pokud jste již nainstalovali instalačního programu webové platformy, můžete otevřít a vyhledejte produktu &quot; *Visual Studio Express 2012 pro Web se sadou Windows Azure SDK*&quot;.</span><span class="sxs-lookup"><span data-stu-id="0bf25-610">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*Visual Studio Express 2012 for Web with Windows Azure SDK*&quot;.</span></span>
2. <span data-ttu-id="0bf25-611">Klikněte na **nyní nainstalovat**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-611">Click on **Install Now**.</span></span> <span data-ttu-id="0bf25-612">Pokud nemáte **instalačního programu webové platformy** budete přesměrováni na stáhněte a nainstalujte ji jako první.</span><span class="sxs-lookup"><span data-stu-id="0bf25-612">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="0bf25-613">Jednou **instalačního programu webové platformy** je otevřený, klikněte na tlačítko **nainstalovat** zahájíte instalaci.</span><span class="sxs-lookup"><span data-stu-id="0bf25-613">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="0bf25-614">![Nainstalovat Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "nainstalovat Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="0bf25-614">![Install Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="0bf25-615">*Nainstalovat Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="0bf25-615">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="0bf25-616">Číst všechny produkty se licence a podmínky a klikněte na tlačítko **souhlasím** pokračujte.</span><span class="sxs-lookup"><span data-stu-id="0bf25-616">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![Vyjádření souhlasu s podmínkami licence](whats-new-in-aspnet-mvc-4/_static/image45.png)

    <span data-ttu-id="0bf25-618">*Vyjádření souhlasu s podmínkami licence*</span><span class="sxs-lookup"><span data-stu-id="0bf25-618">*Accepting the license terms*</span></span>
5. <span data-ttu-id="0bf25-619">Počkejte na dokončení procesu stahování a instalaci.</span><span class="sxs-lookup"><span data-stu-id="0bf25-619">Wait until the downloading and installation process completes.</span></span>

    ![Průběh instalace](whats-new-in-aspnet-mvc-4/_static/image46.png)

    <span data-ttu-id="0bf25-621">*Průběh instalace*</span><span class="sxs-lookup"><span data-stu-id="0bf25-621">*Installation progress*</span></span>
6. <span data-ttu-id="0bf25-622">Po dokončení instalace, klikněte na tlačítko **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-622">When the installation completes, click **Finish**.</span></span>

    ![Instalace byla dokončena.](whats-new-in-aspnet-mvc-4/_static/image47.png)

    <span data-ttu-id="0bf25-624">*Instalace byla dokončena.*</span><span class="sxs-lookup"><span data-stu-id="0bf25-624">*Installation completed*</span></span>
7. <span data-ttu-id="0bf25-625">Klikněte na tlačítko **ukončení** ukončíte instalační program webové platformy.</span><span class="sxs-lookup"><span data-stu-id="0bf25-625">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="0bf25-626">Chcete-li spustit nástroj Visual Studio Express pro Web, přejděte na **spustit** obrazovky a začít psát &quot; **VS Express**&quot;, klikněte na **VS Express pro Web** dlaždice.</span><span class="sxs-lookup"><span data-stu-id="0bf25-626">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express pro Web dlaždice](whats-new-in-aspnet-mvc-4/_static/image48.png)

    <span data-ttu-id="0bf25-628">*VS Express pro Web dlaždice*</span><span class="sxs-lookup"><span data-stu-id="0bf25-628">*VS Express for Web tile*</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a><span data-ttu-id="0bf25-629">Příloha C: instalace služby WebMatrix 2 a iPhone simulátoru</span><span class="sxs-lookup"><span data-stu-id="0bf25-629">Appendix C: Installing WebMatrix 2 and iPhone Simulator</span></span>

<span data-ttu-id="0bf25-630">Spusťte svůj web ve iPhone simulované zařízení můžete rozšíření prostředí WebMatrix &quot;Electric simulátoru Mobile pro iPhone&quot;.</span><span class="sxs-lookup"><span data-stu-id="0bf25-630">To run your site in a simulated iPhone device you can use the WebMatrix extension &quot;Electric Mobile Simulator for the iPhone&quot;.</span></span> <span data-ttu-id="0bf25-631">Také můžete nakonfigurovat stejné rozšiřující spouštět simulátoru ze sady Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="0bf25-631">Also, you can configure the same extension to run the simulator from Visual Studio 2012.</span></span>

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a><span data-ttu-id="0bf25-632">Úloha 1 – instalace služby WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="0bf25-632">Task 1 - Installing WebMatrix 2</span></span>

1. <span data-ttu-id="0bf25-633">Přejděte na [ [https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169).</span><span class="sxs-lookup"><span data-stu-id="0bf25-633">Go to [[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="0bf25-634">Případně, pokud jste již nainstalovali instalačního programu webové platformy, můžete otevřít a vyhledejte produktu &quot; *WebMatrix 2*&quot;.</span><span class="sxs-lookup"><span data-stu-id="0bf25-634">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;*WebMatrix 2*&quot;.</span></span>
2. <span data-ttu-id="0bf25-635">Klikněte na **nyní nainstalovat**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-635">Click on **Install Now**.</span></span> <span data-ttu-id="0bf25-636">Pokud nemáte **instalačního programu webové platformy** budete přesměrováni na stáhněte a nainstalujte ji jako první.</span><span class="sxs-lookup"><span data-stu-id="0bf25-636">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="0bf25-637">Jednou **instalačního programu webové platformy** je otevřený, klikněte na tlačítko **nainstalovat** zahájíte instalaci.</span><span class="sxs-lookup"><span data-stu-id="0bf25-637">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="0bf25-638">![Instalace služby WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "instalace služby WebMatrix 2")</span><span class="sxs-lookup"><span data-stu-id="0bf25-638">![Install WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "Install WebMatrix 2")</span></span>

    <span data-ttu-id="0bf25-639">*Instalace služby WebMatrix 2*</span><span class="sxs-lookup"><span data-stu-id="0bf25-639">*Install WebMatrix 2*</span></span>
4. <span data-ttu-id="0bf25-640">Číst všechny produkty se licence a podmínky a klikněte na tlačítko **souhlasím** pokračujte.</span><span class="sxs-lookup"><span data-stu-id="0bf25-640">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    <span data-ttu-id="0bf25-641">![Vyjádření souhlasu s podmínkami licence](whats-new-in-aspnet-mvc-4/_static/image50.png "vyjádření souhlasu s podmínkami licence")</span><span class="sxs-lookup"><span data-stu-id="0bf25-641">![Accepting the license terms](whats-new-in-aspnet-mvc-4/_static/image50.png "Accepting the license terms")</span></span>

    <span data-ttu-id="0bf25-642">*Vyjádření souhlasu s podmínkami licence*</span><span class="sxs-lookup"><span data-stu-id="0bf25-642">*Accepting the license terms*</span></span>
5. <span data-ttu-id="0bf25-643">Počkejte na dokončení procesu stahování a instalaci.</span><span class="sxs-lookup"><span data-stu-id="0bf25-643">Wait until the downloading and installation process completes.</span></span>

    <span data-ttu-id="0bf25-644">![Průběh instalace](whats-new-in-aspnet-mvc-4/_static/image51.png "průběh instalace")</span><span class="sxs-lookup"><span data-stu-id="0bf25-644">![Installation progress](whats-new-in-aspnet-mvc-4/_static/image51.png "Installation progress")</span></span>

    <span data-ttu-id="0bf25-645">*Průběh instalace*</span><span class="sxs-lookup"><span data-stu-id="0bf25-645">*Installation progress*</span></span>
6. <span data-ttu-id="0bf25-646">Po dokončení instalace, klikněte na tlačítko **Dokončit**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-646">When the installation completes, click **Finish**.</span></span>

    <span data-ttu-id="0bf25-647">![Instalace byla dokončena](whats-new-in-aspnet-mvc-4/_static/image52.png "instalace byla dokončena.")</span><span class="sxs-lookup"><span data-stu-id="0bf25-647">![Installation completed](whats-new-in-aspnet-mvc-4/_static/image52.png "Installation completed")</span></span>

    <span data-ttu-id="0bf25-648">*Instalace byla dokončena.*</span><span class="sxs-lookup"><span data-stu-id="0bf25-648">*Installation completed*</span></span>
7. <span data-ttu-id="0bf25-649">Klikněte na tlačítko **ukončení** ukončíte instalační program webové platformy.</span><span class="sxs-lookup"><span data-stu-id="0bf25-649">Click **Exit** to close Web Platform Installer.</span></span>

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a><span data-ttu-id="0bf25-650">Úloha 2 – instalace iPhone simulátoru rozšíření</span><span class="sxs-lookup"><span data-stu-id="0bf25-650">Task 2 - Installing the iPhone Simulator Extension</span></span>

1. <span data-ttu-id="0bf25-651">Spustit **WebMatrix** a otevřete všechny existující webovou stránku nebo vytvořte novou.</span><span class="sxs-lookup"><span data-stu-id="0bf25-651">Run **WebMatrix** and open any existing Web site or create a new one.</span></span>
2. <span data-ttu-id="0bf25-652">Klikněte **spustit** tlačítko z **Domů** pásu karet a vyberte **přidat nový**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-652">Click the **Run** button from the **Home** ribbon and select **Add new**.</span></span>

    <span data-ttu-id="0bf25-653">![Přidání nové rozšíření prostředí WebMatrix](whats-new-in-aspnet-mvc-4/_static/image53.png "přidání nové rozšíření prostředí WebMatrix")</span><span class="sxs-lookup"><span data-stu-id="0bf25-653">![Adding new WebMatrix extension](whats-new-in-aspnet-mvc-4/_static/image53.png "Adding new WebMatrix extension")</span></span>

    <span data-ttu-id="0bf25-654">*Přidání nové rozšíření prostředí WebMatrix*</span><span class="sxs-lookup"><span data-stu-id="0bf25-654">*Adding new WebMatrix extension*</span></span>
3. <span data-ttu-id="0bf25-655">Vyberte **iPhone simulátoru** a klikněte na tlačítko **nainstalovat**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-655">Select **iPhone Simulator** and click **Install**.</span></span>

    <span data-ttu-id="0bf25-656">![Procházení rozšíření prostředí WebMatrix](whats-new-in-aspnet-mvc-4/_static/image54.png "rozšíření procházení služby WebMatrix")</span><span class="sxs-lookup"><span data-stu-id="0bf25-656">![Browsing WebMatrix extensions](whats-new-in-aspnet-mvc-4/_static/image54.png "Browsing WebMatrix extensions")</span></span>

    <span data-ttu-id="0bf25-657">*Procházení rozšíření pro službu WebMatrix*</span><span class="sxs-lookup"><span data-stu-id="0bf25-657">*Browsing WebMatrix extensions*</span></span>
4. <span data-ttu-id="0bf25-658">V podrobnosti balíčku, klikněte na **nainstalovat** Chcete-li pokračovat v instalaci rozšíření.</span><span class="sxs-lookup"><span data-stu-id="0bf25-658">In the package details, click **Install** to continue with the extension installation.</span></span>

    <span data-ttu-id="0bf25-659">![iPhone simulátoru rozšíření](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone simulátoru rozšíření")</span><span class="sxs-lookup"><span data-stu-id="0bf25-659">![iPhone Simulator extension](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone Simulator extension")</span></span>

    <span data-ttu-id="0bf25-660">*iPhone simulátoru rozšíření*</span><span class="sxs-lookup"><span data-stu-id="0bf25-660">*iPhone Simulator extension*</span></span>
5. <span data-ttu-id="0bf25-661">Přečtěte si a přijměte rozšíření smlouvy EULA.</span><span class="sxs-lookup"><span data-stu-id="0bf25-661">Read and accept the extension EULA.</span></span>

    <span data-ttu-id="0bf25-662">![Rozšíření prostředí WebMatrix smlouvy EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "rozšíření prostředí WebMatrix smlouvy EULA")</span><span class="sxs-lookup"><span data-stu-id="0bf25-662">![WebMatrix extension EULA](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix extension EULA")</span></span>

    <span data-ttu-id="0bf25-663">*Rozšíření prostředí WebMatrix smlouvy EULA*</span><span class="sxs-lookup"><span data-stu-id="0bf25-663">*WebMatrix extension EULA*</span></span>
6. <span data-ttu-id="0bf25-664">Webové stránky můžete nyní spustit ze služby WebMatrix pomocí simulátoru možnost iPhone.</span><span class="sxs-lookup"><span data-stu-id="0bf25-664">Now, you can run your Web site from WebMatrix using the iPhone Simulator option.</span></span>

    <span data-ttu-id="0bf25-665">![Spouštět s využitím iPhone](whats-new-in-aspnet-mvc-4/_static/image57.png "spouštět s využitím iPhone")</span><span class="sxs-lookup"><span data-stu-id="0bf25-665">![Run using iPhone](whats-new-in-aspnet-mvc-4/_static/image57.png "Run using iPhone")</span></span>

    <span data-ttu-id="0bf25-666">*Spouštět s využitím iPhone*</span><span class="sxs-lookup"><span data-stu-id="0bf25-666">*Run using iPhone*</span></span>

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a><span data-ttu-id="0bf25-667">Úloha 3 – konfigurace sady Visual Studio 2012 ke spuštění iPhone simulátoru</span><span class="sxs-lookup"><span data-stu-id="0bf25-667">Task 3 - Configuring Visual Studio 2012 to run iPhone Simulator</span></span>

1. <span data-ttu-id="0bf25-668">Otevřete **Visual Studio 2012** a otevřít libovolný web, nebo vytvořte nový projekt.</span><span class="sxs-lookup"><span data-stu-id="0bf25-668">Open **Visual Studio 2012** and open any Web site or create a new project.</span></span>
2. <span data-ttu-id="0bf25-669">Klikněte na šipku dolů z tlačítko Spustit a vyberte **procházet s**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-669">Click the down arrow from the Run button and select **Browse with**.</span></span>

    <span data-ttu-id="0bf25-670">![Procházet s](whats-new-in-aspnet-mvc-4/_static/image58.png "procházet s")</span><span class="sxs-lookup"><span data-stu-id="0bf25-670">![Browse with](whats-new-in-aspnet-mvc-4/_static/image58.png "Browse with")</span></span>

    <span data-ttu-id="0bf25-671">*Procházet s*</span><span class="sxs-lookup"><span data-stu-id="0bf25-671">*Browse with*</span></span>
3. <span data-ttu-id="0bf25-672">V &quot;procházet s&quot; dialogové okno, klikněte na tlačítko **přidat**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-672">In the &quot;Browse With&quot; dialog, click **Add**.</span></span>
4. <span data-ttu-id="0bf25-673">V &quot;přidat Program&quot; dialogové okno, použijte následující hodnoty:</span><span class="sxs-lookup"><span data-stu-id="0bf25-673">In the &quot;Add Program&quot; dialog, use the following values:</span></span>

    - <span data-ttu-id="0bf25-674">**Program**: C:\Users\*{CurrentUser}*\AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(aktualizace odpovídajícím způsobem cestu)*</span><span class="sxs-lookup"><span data-stu-id="0bf25-674">**Program**: C:\Users\*{CurrentUser}*\AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(update the path accordingly)*</span></span>
    - <span data-ttu-id="0bf25-675">**Argumenty**: &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="0bf25-675">**Arguments**: &quot;1&quot;</span></span>
    - <span data-ttu-id="0bf25-676">**Popisný název**: iPhone simulátoru</span><span class="sxs-lookup"><span data-stu-id="0bf25-676">**Friendly name**: iPhone Simulator</span></span>

    <span data-ttu-id="0bf25-677">![Přidat program](whats-new-in-aspnet-mvc-4/_static/image59.png "přidat program")</span><span class="sxs-lookup"><span data-stu-id="0bf25-677">![Add program](whats-new-in-aspnet-mvc-4/_static/image59.png "Add program")</span></span>

    <span data-ttu-id="0bf25-678">*Přidejte program procházet s*</span><span class="sxs-lookup"><span data-stu-id="0bf25-678">*Add program to browse with*</span></span>
5. <span data-ttu-id="0bf25-679">Klikněte na tlačítko **OK** a zavřete dialogová okna.</span><span class="sxs-lookup"><span data-stu-id="0bf25-679">Click **OK** and close the dialogs.</span></span>
6. <span data-ttu-id="0bf25-680">Nyní budete moci spustit vaší webové aplikace v simulátoru iPhone ze sady Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="0bf25-680">Now you are able to run your Web applications in the iPhone simulator from Visual Studio 2012.</span></span>

    <span data-ttu-id="0bf25-681">![Procházet s iPhone simulátoru](whats-new-in-aspnet-mvc-4/_static/image60.png "procházet s iPhone simulátoru")</span><span class="sxs-lookup"><span data-stu-id="0bf25-681">![Browse with iPhone Simulator](whats-new-in-aspnet-mvc-4/_static/image60.png "Browse with iPhone Simulator")</span></span>

    <span data-ttu-id="0bf25-682">*Procházet s iPhone simulátoru*</span><span class="sxs-lookup"><span data-stu-id="0bf25-682">*Browse with iPhone Simulator*</span></span>

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="0bf25-683">Příloha D: publikování aplikace ASP.NET MVC 4 pomocí nástroje nasazení webu</span><span class="sxs-lookup"><span data-stu-id="0bf25-683">Appendix D: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="0bf25-684">Tento dodatek vám ukáže, jak vytvořit nový web z portálu Windows Azure Management Portal a publikovat aplikace, kterou jste získali podle testovacím prostředí, využívat výhod nasazení webu publikování funkce poskytované služby Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="0bf25-684">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="0bf25-685">Úloha 1 – Vytvoření nového webu ze systému Windows Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0bf25-685">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="0bf25-686">Přejděte na [Windows Azure Management Portal](https://manage.windowsazure.com/) a přihlaste se pomocí přihlašovacích údajů společnosti Microsoft, které jsou spojené s vaším předplatným.</span><span class="sxs-lookup"><span data-stu-id="0bf25-686">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0bf25-687">S Windows Azure můžete bezplatné hostování 10 webů ASP.NET a pak škálujte podle rozšiřujícího se provozu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-687">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="0bf25-688">Můžete si zaregistrovat [zde](http://aka.ms/aspnet-hol-azure).</span><span class="sxs-lookup"><span data-stu-id="0bf25-688">You can sign up [here](http://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="0bf25-689">![Přihlaste se k portálu Windows Azure](whats-new-in-aspnet-mvc-4/_static/image61.png "Přihlaste se k portálu Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="0bf25-689">![Log on to Windows Azure portal](whats-new-in-aspnet-mvc-4/_static/image61.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="0bf25-690">*Přihlaste se k Windows Azure Management Portal*</span><span class="sxs-lookup"><span data-stu-id="0bf25-690">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="0bf25-691">Klikněte na tlačítko **nový** na panelu příkazů.</span><span class="sxs-lookup"><span data-stu-id="0bf25-691">Click **New** on the command bar.</span></span>

    <span data-ttu-id="0bf25-692">![Vytvoření nového webu](whats-new-in-aspnet-mvc-4/_static/image62.png "vytváření nového webu")</span><span class="sxs-lookup"><span data-stu-id="0bf25-692">![Creating a new Web Site](whats-new-in-aspnet-mvc-4/_static/image62.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="0bf25-693">*Vytvoření nového webu*</span><span class="sxs-lookup"><span data-stu-id="0bf25-693">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="0bf25-694">Klikněte na tlačítko **výpočetní** | **webu**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-694">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="0bf25-695">Potom vyberte **rychle vytvořit** možnost.</span><span class="sxs-lookup"><span data-stu-id="0bf25-695">Then select **Quick Create** option.</span></span> <span data-ttu-id="0bf25-696">Zadejte adresu URL k dispozici pro nový web a klikněte na tlačítko **vytvoření webu**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-696">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0bf25-697">Web systému Windows Azure je hostitel pro spouštění v cloudu, ve kterém můžete řídit a spravovat webovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="0bf25-697">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="0bf25-698">Možnost rychle vytvořit můžete nasadit hotové webové aplikace na Windows Azure web z mimo portál.</span><span class="sxs-lookup"><span data-stu-id="0bf25-698">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="0bf25-699">Postup pro nastavení databáze neobsahuje.</span><span class="sxs-lookup"><span data-stu-id="0bf25-699">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="0bf25-700">![Vytvoření nového webu pomocí metody rychlého vytvoření](whats-new-in-aspnet-mvc-4/_static/image63.png "vytváření nového webu pomocí metody rychlého vytvoření")</span><span class="sxs-lookup"><span data-stu-id="0bf25-700">![Creating a new Web Site using Quick Create](whats-new-in-aspnet-mvc-4/_static/image63.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="0bf25-701">*Vytvoření nového webu pomocí metody rychlého vytvoření*</span><span class="sxs-lookup"><span data-stu-id="0bf25-701">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="0bf25-702">Počkejte, dokud nové **webu** je vytvořena.</span><span class="sxs-lookup"><span data-stu-id="0bf25-702">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="0bf25-703">Po vytvoření webu klikněte na odkaz v části **URL** sloupce.</span><span class="sxs-lookup"><span data-stu-id="0bf25-703">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="0bf25-704">Zkontrolujte, zda je funkční nový web.</span><span class="sxs-lookup"><span data-stu-id="0bf25-704">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="0bf25-705">![Procházení na nový web](whats-new-in-aspnet-mvc-4/_static/image64.png "procházení na nový web")</span><span class="sxs-lookup"><span data-stu-id="0bf25-705">![Browsing to the new web site](whats-new-in-aspnet-mvc-4/_static/image64.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="0bf25-706">*Procházení na nový web*</span><span class="sxs-lookup"><span data-stu-id="0bf25-706">*Browsing to the new web site*</span></span>

    <span data-ttu-id="0bf25-707">![Webový server spuštěn](whats-new-in-aspnet-mvc-4/_static/image65.png "webu systémem")</span><span class="sxs-lookup"><span data-stu-id="0bf25-707">![Web site running](whats-new-in-aspnet-mvc-4/_static/image65.png "Web site running")</span></span>

    <span data-ttu-id="0bf25-708">*Spuštění webu*</span><span class="sxs-lookup"><span data-stu-id="0bf25-708">*Web site running*</span></span>
6. <span data-ttu-id="0bf25-709">Přejděte zpět na portál a klikněte na název webu v části **název** sloupec pro zobrazení stránky pro správu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-709">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="0bf25-710">![Otevření stránky Správa webu](whats-new-in-aspnet-mvc-4/_static/image66.png "otevření stránek správu webového serveru")</span><span class="sxs-lookup"><span data-stu-id="0bf25-710">![Opening the web site management pages](whats-new-in-aspnet-mvc-4/_static/image66.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="0bf25-711">*Otevření stránek správu webového serveru*</span><span class="sxs-lookup"><span data-stu-id="0bf25-711">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="0bf25-712">V **řídicí panel** v části **rychlého přehledu** klikněte na položku **stažení profilu publikování** odkaz.</span><span class="sxs-lookup"><span data-stu-id="0bf25-712">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0bf25-713">*Profilu publikování* obsahuje všechny informace požadované pro publikování webové aplikace na web služby Windows Azure pro každou metodu povoleno publikace.</span><span class="sxs-lookup"><span data-stu-id="0bf25-713">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="0bf25-714">Profil publikování obsahuje adresy URL, přihlašovací údaje uživatele a řetězců databází, které jsou potřebné k připojení k a ověřování na základě těchto koncových bodů, pro které je metoda publikace povolena.</span><span class="sxs-lookup"><span data-stu-id="0bf25-714">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="0bf25-715">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express pro Web** a **sadu Microsoft Visual Studio 2012** podporu čtení publikační profily k automatické konfiguraci těchto programů pro publikování webové aplikace na weby služby Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="0bf25-715">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="0bf25-716">![Na webu stažení profilu publikování](whats-new-in-aspnet-mvc-4/_static/image67.png "stahování webové stránky profilu publikování")</span><span class="sxs-lookup"><span data-stu-id="0bf25-716">![Downloading the web site publish profile](whats-new-in-aspnet-mvc-4/_static/image67.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="0bf25-717">*Na webu stažení profilu publikování*</span><span class="sxs-lookup"><span data-stu-id="0bf25-717">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="0bf25-718">Stáhněte si soubor profil publikování do vhodného umístění.</span><span class="sxs-lookup"><span data-stu-id="0bf25-718">Download the publish profile file to a known location.</span></span> <span data-ttu-id="0bf25-719">Dále v tomto cvičení uvidíte jak používat tento soubor k publikování webové aplikace na weby systému Windows Azure ze sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0bf25-719">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="0bf25-720">![Ukládání souboru profilu publikování](whats-new-in-aspnet-mvc-4/_static/image68.png "ukládání profilu publikování")</span><span class="sxs-lookup"><span data-stu-id="0bf25-720">![Saving the publish profile file](whats-new-in-aspnet-mvc-4/_static/image68.png "Saving the publish profile")</span></span>

    <span data-ttu-id="0bf25-721">*Ukládání souboru profilu publikování*</span><span class="sxs-lookup"><span data-stu-id="0bf25-721">*Saving the publish profile file*</span></span>

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="0bf25-722">Úloha 2 – konfigurování serveru databáze</span><span class="sxs-lookup"><span data-stu-id="0bf25-722">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="0bf25-723">Pokud vaše aplikace využívá systému SQL Server, databáze, budete muset vytvořit databázi SQL server.</span><span class="sxs-lookup"><span data-stu-id="0bf25-723">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="0bf25-724">Pokud chcete nasadit jednoduchou aplikaci, která nepoužívá systém SQL Server může tuto úlohu přeskočit.</span><span class="sxs-lookup"><span data-stu-id="0bf25-724">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="0bf25-725">Budete potřebovat databázi SQL serveru pro ukládání databázi aplikace.</span><span class="sxs-lookup"><span data-stu-id="0bf25-725">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="0bf25-726">Databáze SQL servery můžete zobrazit ze svého předplatného na portál Windows Azure Management **databází Sql** | **servery** | **serveru Řídicí panel**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-726">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="0bf25-727">Pokud nemáte server vytvořeno, můžete vytvořit jeden pomocí **přidat** tlačítka na panelu příkazů.</span><span class="sxs-lookup"><span data-stu-id="0bf25-727">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="0bf25-728">Poznamenejte si **název serveru a adresa URL, správce přihlašovací jméno a heslo**, jako je použijete v další úkoly.</span><span class="sxs-lookup"><span data-stu-id="0bf25-728">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="0bf25-729">Nevytvářejte databáze ještě, jak bude vytvořen v pozdější fázi.</span><span class="sxs-lookup"><span data-stu-id="0bf25-729">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="0bf25-730">![Řídicí panel serveru databáze SQL](whats-new-in-aspnet-mvc-4/_static/image69.png "řídicího panelu serveru databáze SQL")</span><span class="sxs-lookup"><span data-stu-id="0bf25-730">![SQL Database Server Dashboard](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="0bf25-731">*Řídicí panel serveru databáze SQL*</span><span class="sxs-lookup"><span data-stu-id="0bf25-731">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="0bf25-732">V dalším úkolem budete testovat připojení k databázi ze sady Visual Studio, proto je nutné zahrnout místní IP adresa serveru seznamu **povolené IP adresy**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-732">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="0bf25-733">To lze provést, klikněte na tlačítko **konfigurace**, vyberte IP adresu z **aktuální IP adresa klienta** a vkládání na **počáteční IP adresa** a **Koncová IP adresa** textová pole a kliknutím ![add-client-ip-address-ok-button](whats-new-in-aspnet-mvc-4/_static/image70.png) tlačítko.</span><span class="sxs-lookup"><span data-stu-id="0bf25-733">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](whats-new-in-aspnet-mvc-4/_static/image70.png) button.</span></span>

    ![Přidávání IP adresy klienta](whats-new-in-aspnet-mvc-4/_static/image71.png)

    <span data-ttu-id="0bf25-735">*Přidávání IP adresy klienta*</span><span class="sxs-lookup"><span data-stu-id="0bf25-735">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="0bf25-736">Jednou **IP adresa klienta** je povolené IP adresy do seznamu, klikněte na **Uložit** potvrďte změny.</span><span class="sxs-lookup"><span data-stu-id="0bf25-736">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![Potvrzení změn](whats-new-in-aspnet-mvc-4/_static/image72.png)

    <span data-ttu-id="0bf25-738">*Potvrzení změn*</span><span class="sxs-lookup"><span data-stu-id="0bf25-738">*Confirm Changes*</span></span>

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="0bf25-739">Úloha 3 – publikování aplikace ASP.NET MVC 4 pomocí nástroje nasazení webu</span><span class="sxs-lookup"><span data-stu-id="0bf25-739">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="0bf25-740">Přejděte zpět na ASP.NET MVC 4 řešení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-740">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="0bf25-741">V **Průzkumníku řešení**, klikněte pravým tlačítkem na webový projekt a vyberte **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-741">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="0bf25-742">![Publikování aplikace](whats-new-in-aspnet-mvc-4/_static/image73.png "publikování aplikace")</span><span class="sxs-lookup"><span data-stu-id="0bf25-742">![Publishing the Application](whats-new-in-aspnet-mvc-4/_static/image73.png "Publishing the Application")</span></span>

    <span data-ttu-id="0bf25-743">*Publikování webu*</span><span class="sxs-lookup"><span data-stu-id="0bf25-743">*Publishing the web site*</span></span>
2. <span data-ttu-id="0bf25-744">Umožňuje naimportujte profil publikování, který jste uložili v první úloze.</span><span class="sxs-lookup"><span data-stu-id="0bf25-744">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="0bf25-745">![Import profilu publikování](whats-new-in-aspnet-mvc-4/_static/image74.png "import profilu publikování")</span><span class="sxs-lookup"><span data-stu-id="0bf25-745">![Importing the publish profile](whats-new-in-aspnet-mvc-4/_static/image74.png "Importing the publish profile")</span></span>

    <span data-ttu-id="0bf25-746">*Import profilu publikování*</span><span class="sxs-lookup"><span data-stu-id="0bf25-746">*Importing publish profile*</span></span>
3. <span data-ttu-id="0bf25-747">Klikněte na tlačítko **ověření připojení**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-747">Click **Validate Connection**.</span></span> <span data-ttu-id="0bf25-748">Po dokončení ověření klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-748">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0bf25-749">Ověření je hotová, jakmile se zobrazí zelené zaškrtnutí zobrazí vedle tlačítko ověřit připojení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-749">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="0bf25-750">![Ověření připojení](whats-new-in-aspnet-mvc-4/_static/image75.png "ověřování připojení")</span><span class="sxs-lookup"><span data-stu-id="0bf25-750">![Validating connection](whats-new-in-aspnet-mvc-4/_static/image75.png "Validating connection")</span></span>

    <span data-ttu-id="0bf25-751">*Ověření připojení*</span><span class="sxs-lookup"><span data-stu-id="0bf25-751">*Validating connection*</span></span>
4. <span data-ttu-id="0bf25-752">V **nastavení** v části **databáze** části, klikněte na tlačítko vedle připojení databáze textové pole (tj. **objekt DefaultConnection**).</span><span class="sxs-lookup"><span data-stu-id="0bf25-752">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="0bf25-753">![Konfigurace nasazení webu](whats-new-in-aspnet-mvc-4/_static/image76.png "konfigurace nasazení webu")</span><span class="sxs-lookup"><span data-stu-id="0bf25-753">![Web deploy configuration](whats-new-in-aspnet-mvc-4/_static/image76.png "Web deploy configuration")</span></span>

    <span data-ttu-id="0bf25-754">*Konfigurace nasazení webu*</span><span class="sxs-lookup"><span data-stu-id="0bf25-754">*Web deploy configuration*</span></span>
5. <span data-ttu-id="0bf25-755">Připojení k databázi nakonfigurujte následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="0bf25-755">Configure the database connection as follows:</span></span>

    - <span data-ttu-id="0bf25-756">V **název serveru** zadejte vaše databáze SQL serveru adresu URL pomocí *tcp:* předponu.</span><span class="sxs-lookup"><span data-stu-id="0bf25-756">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
    - <span data-ttu-id="0bf25-757">V **uživatelské jméno** zadejte vaše přihlašovací jméno správce serveru.</span><span class="sxs-lookup"><span data-stu-id="0bf25-757">In **User name** type your server administrator login name.</span></span>
    - <span data-ttu-id="0bf25-758">V **heslo** zadejte přihlašovací heslo správce serveru.</span><span class="sxs-lookup"><span data-stu-id="0bf25-758">In **Password** type your server administrator login password.</span></span>
    - <span data-ttu-id="0bf25-759">Zadejte nový název databáze, například: *MVC4SampleDB*.</span><span class="sxs-lookup"><span data-stu-id="0bf25-759">Type a new database name, for example: *MVC4SampleDB*.</span></span>

    <span data-ttu-id="0bf25-760">![Konfigurace cílový připojovací řetězec](whats-new-in-aspnet-mvc-4/_static/image77.png "konfigurace cílový připojovací řetězec")</span><span class="sxs-lookup"><span data-stu-id="0bf25-760">![Configuring destination connection string](whats-new-in-aspnet-mvc-4/_static/image77.png "Configuring destination connection string")</span></span>

    <span data-ttu-id="0bf25-761">*Konfigurace cílový připojovací řetězec*</span><span class="sxs-lookup"><span data-stu-id="0bf25-761">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="0bf25-762">Pak klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-762">Then click **OK**.</span></span> <span data-ttu-id="0bf25-763">Po zobrazení výzvy k vytvoření databáze, klikněte na tlačítko **Ano**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-763">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="0bf25-764">![Vytvoření databáze](whats-new-in-aspnet-mvc-4/_static/image78.png "vytváření řetězec databáze")</span><span class="sxs-lookup"><span data-stu-id="0bf25-764">![Creating the database](whats-new-in-aspnet-mvc-4/_static/image78.png "Creating the database string")</span></span>

    <span data-ttu-id="0bf25-765">*Vytvoření databáze*</span><span class="sxs-lookup"><span data-stu-id="0bf25-765">*Creating the database*</span></span>
7. <span data-ttu-id="0bf25-766">Připojovací řetězec, který budete používat pro připojení k databázi SQL v systému Windows Azure je uvedené v rámci textbox výchozí připojení.</span><span class="sxs-lookup"><span data-stu-id="0bf25-766">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="0bf25-767">Pak klikněte na tlačítko **Další**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-767">Then click **Next**.</span></span>

    <span data-ttu-id="0bf25-768">![Připojovací řetězec odkazující na databázi SQL](whats-new-in-aspnet-mvc-4/_static/image79.png "připojovací řetězec odkazující na databázi SQL")</span><span class="sxs-lookup"><span data-stu-id="0bf25-768">![Connection string pointing to SQL Database](whats-new-in-aspnet-mvc-4/_static/image79.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="0bf25-769">*Připojovací řetězec odkazující na databázi SQL*</span><span class="sxs-lookup"><span data-stu-id="0bf25-769">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="0bf25-770">V **Preview** klikněte na tlačítko **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="0bf25-770">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="0bf25-771">![Publikování webové aplikace](whats-new-in-aspnet-mvc-4/_static/image80.png "publikování webové aplikace")</span><span class="sxs-lookup"><span data-stu-id="0bf25-771">![Publishing the web application](whats-new-in-aspnet-mvc-4/_static/image80.png "Publishing the web application")</span></span>

    <span data-ttu-id="0bf25-772">*Publikování webové aplikace*</span><span class="sxs-lookup"><span data-stu-id="0bf25-772">*Publishing the web application*</span></span>
9. <span data-ttu-id="0bf25-773">Jakmile proces publikování dokončí, otevře se výchozí prohlížeč publikované webové stránky.</span><span class="sxs-lookup"><span data-stu-id="0bf25-773">Once the publishing process finishes, your default browser will open the published web site.</span></span>

    <span data-ttu-id="0bf25-774">![Aplikace publikována do služby Windows Azure](whats-new-in-aspnet-mvc-4/_static/image81.png "aplikace publikována do služby Windows Azure")</span><span class="sxs-lookup"><span data-stu-id="0bf25-774">![Application published to Windows Azure](whats-new-in-aspnet-mvc-4/_static/image81.png "Application published to Windows Azure")</span></span>

    <span data-ttu-id="0bf25-775">*Aplikace, které jsou publikovány do služby Windows Azure*</span><span class="sxs-lookup"><span data-stu-id="0bf25-775">*Application published to Windows Azure*</span></span>