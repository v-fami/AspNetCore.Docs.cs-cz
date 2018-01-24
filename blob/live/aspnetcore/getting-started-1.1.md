---
title: "Začínáme s ASP.NET Core 1.1"
author: rick-anderson
description: "Rychlý kurz, který vytvoří a spustí jednoduchou aplikaci Hello World pomocí ASP.NET Core 1.1."
ms.author: riande
manager: wpickett
ms.date: 08/07/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: getting-started-1.1
ms.openlocfilehash: 7f178618508e1a1e9c49d8ace619b9f942998dae
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/19/2018
---
# <a name="getting-started-with-aspnet-core-11"></a><span data-ttu-id="2aa82-103">Začínáme s ASP.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="2aa82-103">Getting Started with ASP.NET Core 1.1</span></span>

> [!NOTE]
> <span data-ttu-id="2aa82-104">Tyto pokyny jsou určené pro ASP.NET Core 1.1.</span><span class="sxs-lookup"><span data-stu-id="2aa82-104">These instructions are for ASP.NET Core 1.1.</span></span> <span data-ttu-id="2aa82-105">Hledáte nejnovější verzi?</span><span class="sxs-lookup"><span data-stu-id="2aa82-105">Looking for the latest version?</span></span> <span data-ttu-id="2aa82-106">V tématu [aktuální verzi v tomto kurzu](xref:getting-started).</span><span class="sxs-lookup"><span data-stu-id="2aa82-106">See [the current version of this tutorial](xref:getting-started).</span></span>

1. <span data-ttu-id="2aa82-107">Instalace .NET Core **instalační program sady SDK** pro sadu SDK 1.0.4 z [.NET Core 1.0.5 & 1.1.2 SDK 1.0.4 stáhne stránky](https://github.com/dotnet/core/blob/master/release-notes/download-archives/1.0.5-download.md).</span><span class="sxs-lookup"><span data-stu-id="2aa82-107">Install the .NET Core **SDK Installer** for SDK 1.0.4 from the [.NET Core 1.0.5 & 1.1.2 SDK 1.0.4 downloads page](https://github.com/dotnet/core/blob/master/release-notes/download-archives/1.0.5-download.md).</span></span>

2. <span data-ttu-id="2aa82-108">Vytvořte složku pro nový projekt .NET Core.</span><span class="sxs-lookup"><span data-stu-id="2aa82-108">Create a folder for a new .NET Core project.</span></span>

   <span data-ttu-id="2aa82-109">V systému macOS a Linux otevřete okno terminálu.</span><span class="sxs-lookup"><span data-stu-id="2aa82-109">On macOS and Linux, open a terminal window.</span></span> <span data-ttu-id="2aa82-110">V systému Windows otevřete příkazový řádek.</span><span class="sxs-lookup"><span data-stu-id="2aa82-110">On Windows, open a command prompt.</span></span>

   ```terminal
   mkdir aspnetcoreapp
   cd aspnetcoreapp
   ```

2. <span data-ttu-id="2aa82-111">Pokud jste nainstalovali novější verze sady SDK na váš počítač, vytvořte *global.json* soubor a vyberte 1.0.4 SDK.</span><span class="sxs-lookup"><span data-stu-id="2aa82-111">If you have installed a later SDK version on your machine, create a *global.json* file to select the 1.0.4 SDK.</span></span>

   ```json
   {
     "sdk": { "version": "1.0.4" }
   }
   ```

2. <span data-ttu-id="2aa82-112">Vytvoření nového projektu .NET Core.</span><span class="sxs-lookup"><span data-stu-id="2aa82-112">Create a new .NET Core project.</span></span>

   ```terminal
   dotnet new web
   ```
   
3.  <span data-ttu-id="2aa82-113">Obnovení balíčků.</span><span class="sxs-lookup"><span data-stu-id="2aa82-113">Restore the packages.</span></span>

    ```terminal
    dotnet restore
    ```

4. <span data-ttu-id="2aa82-114">Spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="2aa82-114">Run the app.</span></span>

   <span data-ttu-id="2aa82-115">`dotnet run` Příkaz sestavení aplikace nejprve v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="2aa82-115">The `dotnet run` command builds the app first if needed.</span></span>

   ```terminal
   dotnet run
   ```

5. <span data-ttu-id="2aa82-116">Přejděte na`http://localhost:5000`</span><span class="sxs-lookup"><span data-stu-id="2aa82-116">Browse to `http://localhost:5000`</span></span>

<!-- H3 to avoid a single-entry internal TOC -->
### <a name="next-steps"></a><span data-ttu-id="2aa82-117">Další kroky</span><span class="sxs-lookup"><span data-stu-id="2aa82-117">Next steps</span></span>

<span data-ttu-id="2aa82-118">Kurzy Začínáme najdete v části [kurzy jádro ASP.NET](tutorials/index.md)</span><span class="sxs-lookup"><span data-stu-id="2aa82-118">For getting-started tutorials, see [ASP.NET Core Tutorials](tutorials/index.md)</span></span>

<span data-ttu-id="2aa82-119">Úvod do ASP.NET základní koncepty a architektury, najdete v části [ASP.NET Core ÚVOD](index.md) a [ASP.NET Core Základy](fundamentals/index.md).</span><span class="sxs-lookup"><span data-stu-id="2aa82-119">For an introduction to ASP.NET Core concepts and architecture, see [ASP.NET Core Introduction](index.md) and [ASP.NET Core Fundamentals](fundamentals/index.md).</span></span>

<span data-ttu-id="2aa82-120">Aplikace ASP.NET Core pomocí .NET Core nebo základní rozhraní .NET Framework – knihovna tříd a modulu runtime.</span><span class="sxs-lookup"><span data-stu-id="2aa82-120">An ASP.NET Core app can use the .NET Core or .NET Framework Base Class Library and runtime.</span></span> <span data-ttu-id="2aa82-121">Další informace najdete v tématu [výběru mezi .NET Core a rozhraní .NET Framework](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server).</span><span class="sxs-lookup"><span data-stu-id="2aa82-121">For more information, see [Choosing between .NET Core and .NET Framework](https://docs.microsoft.com/dotnet/articles/standard/choosing-core-framework-server).</span></span>