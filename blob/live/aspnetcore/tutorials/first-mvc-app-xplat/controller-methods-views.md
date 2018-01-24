---
title: "Metody kontroleru a zobrazení"
author: rick-anderson
description: "Práce s metody kontroleru, zobrazení a DataAnnotations"
ms.author: riande
manager: wpickett
ms.date: 04/07/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app-xplat/controller-methods-views
ms.openlocfilehash: 1d9258d8f52bf7030ae34ac4069b1b02a51de51b
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/19/2018
---
# <a name="controller-methods-and-views"></a><span data-ttu-id="074aa-103">Metody kontroleru a zobrazení</span><span class="sxs-lookup"><span data-stu-id="074aa-103">Controller methods and views</span></span>

<span data-ttu-id="074aa-104">Podle [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="074aa-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="074aa-105">Máme správné spuštění na filmová aplikace, ale prezentaci není ideální.</span><span class="sxs-lookup"><span data-stu-id="074aa-105">We have a good start to the movie app, but the presentation is not ideal.</span></span> <span data-ttu-id="074aa-106">Neradi najdete v části času (12:00:00 AM na obrázku níže) a **ReleaseDate** by měla být dva slova.</span><span class="sxs-lookup"><span data-stu-id="074aa-106">We don't want to see the time (12:00:00 AM in the image below) and **ReleaseDate** should be two words.</span></span>

![Index zobrazení: Datum vydání je jedno slovo (bez mezery) a každý datum vydání film zobrazuje čas 12: 00](../../tutorials/first-mvc-app/working-with-sql/_static/m55.png)

<span data-ttu-id="074aa-108">Otevřete *Models/Movie.cs* souboru a přidejte zvýrazněné řádky vidíte níže:</span><span class="sxs-lookup"><span data-stu-id="074aa-108">Open the *Models/Movie.cs* file and add the highlighted lines shown below:</span></span>

[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieDate.cs?name=snippet_1&highlight=2,11-12)]

<span data-ttu-id="074aa-109">Sestavte a spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="074aa-109">Build and run the app.</span></span>

<!-- include start
![MVC Movie application open browser showing movie data](../../tutorials/first-mvc-app/working-with-sql/_static/m55.png)

 -->

[!INCLUDE[adding-model](../../includes/mvc-intro/controller-methods-views.md)]

>[!div class="step-by-step"]
<span data-ttu-id="074aa-110">[Předchozí - práce s SQLite](working-with-sql.md)
[další – přidání vyhledávání](search.md)</span><span class="sxs-lookup"><span data-stu-id="074aa-110">[Previous - Working with SQLite](working-with-sql.md)
[Next - Add search](search.md)</span></span>  