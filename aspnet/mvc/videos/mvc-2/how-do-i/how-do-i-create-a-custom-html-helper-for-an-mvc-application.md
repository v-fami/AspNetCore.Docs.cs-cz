---
uid: mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
title: "Jak vytvořit I: Pomocník vlastní HTML pro aplikaci MVC? | Microsoft Docs"
author: rick-anderson
description: "V tomto videu Jan PEL ukazuje, jak vytvořit vlastní HtmlHelper, který není k dispozici v standardní sady v aplikaci MVC. První, ukázkové aplikace MVC..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/11/2009
ms.topic: article
ms.assetid: 58b5eb15-4160-4ce2-ae70-6ba94262ea73
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
msc.type: video
ms.openlocfilehash: 96e58c706101c8b304636947b723fc50cae7f3bc
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/10/2017
---
<a name="how-do-i-create-a-custom-html-helper-for-an-mvc-application"></a><span data-ttu-id="7f687-105">Jak vytvořit I: Pomocník vlastní HTML pro aplikaci MVC?</span><span class="sxs-lookup"><span data-stu-id="7f687-105">How Do I: Create a Custom HTML Helper for an MVC Application?</span></span>
====================
<span data-ttu-id="7f687-106">podle [PEL Jan](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="7f687-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="7f687-107">V tomto videu Jan PEL ukazuje, jak vytvořit vlastní HtmlHelper, který není k dispozici v standardní sady v aplikaci MVC.</span><span class="sxs-lookup"><span data-stu-id="7f687-107">In this video Chris Pels shows how to create a custom HtmlHelper that is not available in the standard set in an MVC application.</span></span> <span data-ttu-id="7f687-108">Ukázková aplikace MVC se nejprve vytvoří s ukázku řadiče a zobrazení otestovat vlastní HtmlHelper.</span><span class="sxs-lookup"><span data-stu-id="7f687-108">First, a sample MVC application is created with a demo controller and view to test the custom HtmlHelper.</span></span> <span data-ttu-id="7f687-109">V dalším kroku se vytvoří modul s veřejnou funkci, která je metody rozšíření, která představuje implementaci vlastní HtmlHelper.</span><span class="sxs-lookup"><span data-stu-id="7f687-109">Next, a module is created with a public function that is an extension method which represents the implementation of the custom HtmlHelper.</span></span> <span data-ttu-id="7f687-110">Je vlastního pomocného objektu pro vytváření &amp;lt; img&amp;gt; značky na stránce a přijímá několik příchozích parametry, včetně id, adresy url a alternativní text pro obrázek značky.</span><span class="sxs-lookup"><span data-stu-id="7f687-110">The custom helper is for creating &amp;lt;img&amp;gt; tags in a page and receives several inbound parameters including the id, url, and alt text for the image tag.</span></span> <span data-ttu-id="7f687-111">Logika se pak přidá funkce pro vrácení dokončené &amp;lt; img&amp;gt; značky se zadanými informacemi.</span><span class="sxs-lookup"><span data-stu-id="7f687-111">The logic is then added to the function for returning the completed &amp;lt;img&amp;gt; tag with the specified information.</span></span> <span data-ttu-id="7f687-112">Vlastní HtmlHelper je použita na stránce ukázku zobrazíte bitovou kopii.</span><span class="sxs-lookup"><span data-stu-id="7f687-112">Then the custom HtmlHelper is used on the demo page to display an image.</span></span> <span data-ttu-id="7f687-113">Nakonec je vlastní HtmlHelper rozšířit, aby obsahovaly více konstruktor přepsání, které poskytují flexibilitu pro více snadno vytváření jiný &amp;lt; img&amp;gt; značky.</span><span class="sxs-lookup"><span data-stu-id="7f687-113">Finally, the custom HtmlHelper is expanded to include multiple constructor overrides which provide flexibility for more easily creating different &amp;lt;img&amp;gt; tags.</span></span>

[<span data-ttu-id="7f687-114">&#9654; Podívejte se na video (18 minuty)</span><span class="sxs-lookup"><span data-stu-id="7f687-114">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-create-a-custom-html-helper-for-an-mvc-application)

>[!div class="step-by-step"]
<span data-ttu-id="7f687-115">[Předchozí](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
[další](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="7f687-115">[Previous](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
[Next](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span></span>