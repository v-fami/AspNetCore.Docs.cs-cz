---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: "Přidání modelu | Microsoft Docs"
author: Rick-Anderson
description: "Poznámka: Aktualizovanou verzi tohoto kurzu je k dispozici, která používá ASP.NET MVC 5 a Visual Studio 2013. Je bezpečnější, mnohem jednodušší a postupujte podle ukázku..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 1d066e4bab866a2195647f43aa886279fee941db
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/10/2017
---
<a name="adding-a-model"></a><span data-ttu-id="d2bef-104">Přidání modelu</span><span class="sxs-lookup"><span data-stu-id="d2bef-104">Adding a Model</span></span>
====================
<span data-ttu-id="d2bef-105">Podle [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="d2bef-105">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="d2bef-106">Je k dispozici aktualizovaná verze tohoto kurzu [sem](../../getting-started/introduction/getting-started.md) používající ASP.NET MVC 5 a Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="d2bef-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="d2bef-107">Je bezpečnější, postupujte podle mnohem jednodušší a ukazuje další funkce.</span><span class="sxs-lookup"><span data-stu-id="d2bef-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>


<span data-ttu-id="d2bef-108">V této části přidáte některé třídy pro správu filmy v databázi.</span><span class="sxs-lookup"><span data-stu-id="d2bef-108">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="d2bef-109">Tyto třídy bude &quot;modelu&quot; součástí aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="d2bef-109">These classes will be the &quot;model&quot; part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="d2bef-110">Budete používat technologie pro přístup k datům rozhraní .NET Framework označuje jako [Entity Framework](https://msdn.microsoft.com/en-us/library/bb399572(VS.110).aspx) definovat a pracovat s tyto třídy modelu.</span><span class="sxs-lookup"><span data-stu-id="d2bef-110">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://msdn.microsoft.com/en-us/library/bb399572(VS.110).aspx) to define and work with these model classes.</span></span> <span data-ttu-id="d2bef-111">Podporuje rozhraní Entity Framework (často označované jako EF) vývoj zlepší názvem *Code First*.</span><span class="sxs-lookup"><span data-stu-id="d2bef-111">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="d2bef-112">Kód nejprve vám umožní vytvořit objekty modelu vytvořením jednoduchého třídy.</span><span class="sxs-lookup"><span data-stu-id="d2bef-112">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="d2bef-113">(Jedná se také označuje jako třídy objektů POCO, z &quot;objekty CLR prostý starý.&quot;) Pak můžete mít databázi vytvořené za chodu ze třídy, která umožňuje velmi vyčištění a rychlý vývoj pracovního postupu.</span><span class="sxs-lookup"><span data-stu-id="d2bef-113">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="d2bef-114">Přidání třídy modelu</span><span class="sxs-lookup"><span data-stu-id="d2bef-114">Adding Model Classes</span></span>

<span data-ttu-id="d2bef-115">V **Průzkumníku řešení**, klikněte pravým tlačítkem *modely* složky, vyberte **přidat**a potom vyberte **třída**.</span><span class="sxs-lookup"><span data-stu-id="d2bef-115">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="d2bef-116">Zadejte *třída* název &quot;film&quot;.</span><span class="sxs-lookup"><span data-stu-id="d2bef-116">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="d2bef-117">Následujících pět vlastnosti, které chcete přidat `Movie` třídy:</span><span class="sxs-lookup"><span data-stu-id="d2bef-117">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="d2bef-118">Použijeme `Movie` třída představující filmy v databázi.</span><span class="sxs-lookup"><span data-stu-id="d2bef-118">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="d2bef-119">Každá instance `Movie` objektu bude odpovídat na řádek v tabulce databáze a každou vlastnost `Movie` třída bude mapovat na sloupec v tabulce.</span><span class="sxs-lookup"><span data-stu-id="d2bef-119">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="d2bef-120">Do stejného souboru přidejte následující `MovieDBContext` třídy:</span><span class="sxs-lookup"><span data-stu-id="d2bef-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

<span data-ttu-id="d2bef-121">`MovieDBContext` Třída reprezentuje kontext Entity Framework film databáze, která zpracovává načítání, ukládání a aktualizace `Movie` třídy instance v databázi.</span><span class="sxs-lookup"><span data-stu-id="d2bef-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="d2bef-122">`MovieDBContext` Je odvozena z `DbContext` základní třída poskytuje rozhraní Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="d2bef-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="d2bef-123">Aby bylo možné odkazovat `DbContext` a `DbSet`, je nutné přidat následující `using` příkaz v horní části souboru:</span><span class="sxs-lookup"><span data-stu-id="d2bef-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="d2bef-124">Kompletní *Movie.cs* souboru je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="d2bef-124">The complete *Movie.cs* file is shown below.</span></span> <span data-ttu-id="d2bef-125">(Několik pomocí příkazů, které nejsou potřebné byly odebrány.)</span><span class="sxs-lookup"><span data-stu-id="d2bef-125">(Several using statements that are not needed have been removed.)</span></span>

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="d2bef-126">Vytvoření připojovacího řetězce a práci s LocalDB serveru SQL</span><span class="sxs-lookup"><span data-stu-id="d2bef-126">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="d2bef-127">`MovieDBContext` Třídy, které jste vytvořili zpracovává úlohu s připojením k databázi a mapování `Movie` objekty záznamy v databázi.</span><span class="sxs-lookup"><span data-stu-id="d2bef-127">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="d2bef-128">Jeden otázku může, ale je uveden postup určit se připojí k databázi.</span><span class="sxs-lookup"><span data-stu-id="d2bef-128">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="d2bef-129">Můžete to udělat tak, že přidáte informace o připojení v *Web.config* souboru aplikace.</span><span class="sxs-lookup"><span data-stu-id="d2bef-129">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="d2bef-130">Otevřete kořenový adresář aplikace *Web.config* souboru.</span><span class="sxs-lookup"><span data-stu-id="d2bef-130">Open the application root *Web.config* file.</span></span> <span data-ttu-id="d2bef-131">(Není *Web.config* v soubor *zobrazení* složky.) Otevřete *Web.config* souboru označeno červeně.</span><span class="sxs-lookup"><span data-stu-id="d2bef-131">(Not the *Web.config* file in the *Views* folder.) Open the *Web.config* file outlined in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="d2bef-132">Přidejte následující připojovací řetězec k `<connectionStrings>` element v *Web.config* souboru.</span><span class="sxs-lookup"><span data-stu-id="d2bef-132">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="d2bef-133">Následující příklad ukazuje část *Web.config* soubor s přidat nový připojovací řetězec:</span><span class="sxs-lookup"><span data-stu-id="d2bef-133">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

<span data-ttu-id="d2bef-134">Malé množství kódu a XML je všechno, co potřebujete k zápisu, aby bylo možné představují a ukládat data film v databázi.</span><span class="sxs-lookup"><span data-stu-id="d2bef-134">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="d2bef-135">Dále budete vytvářet nové `MoviesController` třídu, která můžete použít k zobrazení dat film a povolit uživatelům vytvářet nové výpisy film.</span><span class="sxs-lookup"><span data-stu-id="d2bef-135">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="d2bef-136">[Předchozí](adding-a-view.md)
[další](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="d2bef-136">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>