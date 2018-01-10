---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: "Část 2: Data Access Layer | Microsoft Docs"
author: JoeStagner
description: "Tento kurz řady podrobnosti všechny kroky k vytvoření ukázkové aplikace Tailspin Spyworks. Část 2 popisuje přidání vrstva přístupu k datům."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 8b07b320640c1bb0074a4d3a04ca7c5b7e7bb6cd
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/10/2017
---
<a name="part-2-data-access-layer"></a><span data-ttu-id="065ea-104">Část 2: Data Access Layer</span><span class="sxs-lookup"><span data-stu-id="065ea-104">Part 2: Data Access Layer</span></span>
====================
<span data-ttu-id="065ea-105">podle [Stagner Jan](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="065ea-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="065ea-106">Tailspin Spyworks ukazuje, jak neobvykle jednoduché je vytvoření efektivní a škálovatelné aplikace pro platformu .NET.</span><span class="sxs-lookup"><span data-stu-id="065ea-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="065ea-107">Zobrazuje vypnout používání skvělé nové funkce v rozhraní ASP.NET 4 k sestavení online úložiště, včetně nákupy, najdete v článku věnovaném a správu.</span><span class="sxs-lookup"><span data-stu-id="065ea-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="065ea-108">Tento kurz řady podrobnosti všechny kroky k vytvoření ukázkové aplikace Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="065ea-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="065ea-109">Část 2 popisuje přidání vrstva přístupu k datům.</span><span class="sxs-lookup"><span data-stu-id="065ea-109">Part 2 covers adding the data access layer.</span></span>


## <a id="_Toc260221668"></a><span data-ttu-id="065ea-110">Přidání Data Access Layer</span><span class="sxs-lookup"><span data-stu-id="065ea-110">Adding the Data Access Layer</span></span>

<span data-ttu-id="065ea-111">Naše aplikace pro elektronické obchodování bude záviset na dvě databáze.</span><span class="sxs-lookup"><span data-stu-id="065ea-111">Our ecommerce application will depend on two databases.</span></span>

<span data-ttu-id="065ea-112">Informace o odběrateli použijeme standardní databáze členství technologie ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="065ea-112">For customer information we'll use the standard ASP.NET Membership database.</span></span> <span data-ttu-id="065ea-113">Pro naše nákupní košík a produkt katalog jsme budete implementovat databázi SQL Express následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="065ea-113">For our shopping cart and product catalog we'll implement a SQL Express database as follows.</span></span>

![](tailspin-spyworks-part-2/_static/image1.jpg)

<span data-ttu-id="065ea-114">Obsahující vytvořené databáze (Commerce.mdf) v aplikaci aplikace\_složky dat je možné přejít k vytvoření naše Data Access Layer pomocí rozhraní .NET Framework Entity.</span><span class="sxs-lookup"><span data-stu-id="065ea-114">Having created the database (Commerce.mdf) in the application's App\_Data folder we can proceed to create our Data Access Layer using the .NET Entity Framework.</span></span>

<span data-ttu-id="065ea-115">Vytvoříme složku s názvem "Data\_přístup" a jejich klikněte pravým tlačítkem na této složky a vyberte možnost "Přidat novou položku".</span><span class="sxs-lookup"><span data-stu-id="065ea-115">We'll create a folder named "Data\_Access" and them right click on that folder and select "Add New Item".</span></span>

<span data-ttu-id="065ea-116">"Nainstalovaných šablonách" položku a pak vyberte položku "ADO.NET Entity Data Model" Zadejte EDM\_Commerce.edmx jako název a klikněte na tlačítko "Přidat".</span><span class="sxs-lookup"><span data-stu-id="065ea-116">In the "Installed Templates" item and then select "ADO.NET Entity Data Model" enter EDM\_Commerce.edmx as the name and click the "Add" button.</span></span>

![](tailspin-spyworks-part-2/_static/image2.jpg)

<span data-ttu-id="065ea-117">Zvolte "Generování z databáze".</span><span class="sxs-lookup"><span data-stu-id="065ea-117">Choose "Generate from Database".</span></span>

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

<span data-ttu-id="065ea-118">Uložit a sestavit.</span><span class="sxs-lookup"><span data-stu-id="065ea-118">Save and build.</span></span>

<span data-ttu-id="065ea-119">Nyní jsme připraveni přidat naše první funkce – Kategorie nabídky produktů.</span><span class="sxs-lookup"><span data-stu-id="065ea-119">Now we are ready to add our first feature – a product category menu.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="065ea-120">[Předchozí](tailspin-spyworks-part-1.md)
[další](tailspin-spyworks-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="065ea-120">[Previous](tailspin-spyworks-part-1.md)
[Next](tailspin-spyworks-part-3.md)</span></span>