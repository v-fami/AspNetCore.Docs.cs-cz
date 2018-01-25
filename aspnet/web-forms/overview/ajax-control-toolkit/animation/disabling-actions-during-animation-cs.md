---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-cs
title: "Zakázání akcí během animace (C#) | Microsoft Docs"
author: wenz
description: "V sadě nástrojů ovládacího prvku ASP.NET AJAX ovládacího prvku animace není právě ovládací prvek ale celé rozhraní pro přidání do ovládacího prvku animace. Také podporuje akce..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 918026b4-2f63-421d-8546-df12856960a8
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-cs
msc.type: authoredcontent
ms.openlocfilehash: 875c6be5e190c31fac030fc17ef040a934233f16
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/10/2017
---
<a name="disabling-actions-during-animation-c"></a><span data-ttu-id="624ce-104">Zakázání akcí během animace (C#)</span><span class="sxs-lookup"><span data-stu-id="624ce-104">Disabling Actions during Animation (C#)</span></span>
====================
<span data-ttu-id="624ce-105">podle [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="624ce-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="624ce-106">[Stáhněte si kód](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.cs.zip) nebo [stáhnout PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="624ce-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7CS.pdf)</span></span>

> <span data-ttu-id="624ce-107">V sadě nástrojů ovládacího prvku ASP.NET AJAX ovládacího prvku animace není právě ovládací prvek ale celé rozhraní pro přidání do ovládacího prvku animace.</span><span class="sxs-lookup"><span data-stu-id="624ce-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="624ce-108">Podporuje také akce, jako jsou kliknutí myší.</span><span class="sxs-lookup"><span data-stu-id="624ce-108">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="624ce-109">Ale při kliknutí myší spuštění animace, je třeba zakázat kliknutí myší během animace.</span><span class="sxs-lookup"><span data-stu-id="624ce-109">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>


## <a name="overview"></a><span data-ttu-id="624ce-110">Přehled</span><span class="sxs-lookup"><span data-stu-id="624ce-110">Overview</span></span>

<span data-ttu-id="624ce-111">V sadě nástrojů ovládacího prvku ASP.NET AJAX ovládacího prvku animace není právě ovládací prvek ale celé rozhraní pro přidání do ovládacího prvku animace.</span><span class="sxs-lookup"><span data-stu-id="624ce-111">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="624ce-112">Podporuje také akce, jako jsou kliknutí myší.</span><span class="sxs-lookup"><span data-stu-id="624ce-112">It also supports actions, like mouse clicks.</span></span> <span data-ttu-id="624ce-113">Ale při kliknutí myší spuštění animace, je třeba zakázat kliknutí myší během animace.</span><span class="sxs-lookup"><span data-stu-id="624ce-113">However when a mouse click starts an animation, it is desirable to disable mouse clicks during the animation.</span></span>

## <a name="steps"></a><span data-ttu-id="624ce-114">Kroky</span><span class="sxs-lookup"><span data-stu-id="624ce-114">Steps</span></span>

<span data-ttu-id="624ce-115">První řadě zahrnují `ScriptManager` na stránce; potom knihovny ASP.NET AJAX je načtena, aby bylo možné použít Toolkitu:</span><span class="sxs-lookup"><span data-stu-id="624ce-115">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample1.aspx)]

<span data-ttu-id="624ce-116">Animace se použijí k HTML tlačítko takto:</span><span class="sxs-lookup"><span data-stu-id="624ce-116">The animation will be applied to an HTML button like this:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample2.aspx)]

<span data-ttu-id="624ce-117">Upozorňujeme, že ovládací prvek jazyka HTML je místo ovládací prvek webu vzhledem k tomu, že jsme nechcete, aby tlačítko pro vytvoření zpětné volání; právě zahájí animace straně klienta pro nás.</span><span class="sxs-lookup"><span data-stu-id="624ce-117">Note that an HTML Control is used instead of a Web Control since we do not want the button to create a postback; it shall just launch the client-side animation for us.</span></span>

<span data-ttu-id="624ce-118">Poté, přidejte `AnimationExtender` na stránku, poskytuje `ID`, `TargetControlID` atribut a povinný údaj `runat="server"`:</span><span class="sxs-lookup"><span data-stu-id="624ce-118">Then, add the `AnimationExtender` to the page, providing an `ID`, the `TargetControlID` attribute and the obligatory `runat="server"`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample3.aspx)]

<span data-ttu-id="624ce-119">V rámci `<Animations>` uzlu `<OnClick>` je element správné zpracování kliknutí myší.</span><span class="sxs-lookup"><span data-stu-id="624ce-119">Within the `<Animations>` node, `<OnClick>` is the right element to handle the mouse click.</span></span> <span data-ttu-id="624ce-120">Však může být stisknuto během animace také.</span><span class="sxs-lookup"><span data-stu-id="624ce-120">However, the button could be clicked during the animation, as well.</span></span> <span data-ttu-id="624ce-121">`<EnableAction>` Element můžou starat o který.</span><span class="sxs-lookup"><span data-stu-id="624ce-121">The `<EnableAction>` element can take care of that.</span></span> <span data-ttu-id="624ce-122">Nastavení `Enabled="false"` zakáže tlačítko jako součást animace.</span><span class="sxs-lookup"><span data-stu-id="624ce-122">Setting `Enabled="false"` disables the button as part of the animation.</span></span> <span data-ttu-id="624ce-123">Vzhledem k tomu, že se používá několik jednotlivých animace (zakázání tlačítko a skutečný animace), `<Parallel>` element je potřeba dohledání jeden animací společně do jednoho.</span><span class="sxs-lookup"><span data-stu-id="624ce-123">Since we are using several individual animations (disabling the button and the actual animations), the `<Parallel>` element is required to glue the single animations together into one.</span></span> <span data-ttu-id="624ce-124">Tady je kompletní kód pro `AnimationExtender`:</span><span class="sxs-lookup"><span data-stu-id="624ce-124">Here is the complete markup for `AnimationExtender`:</span></span>

[!code-aspx[Main](disabling-actions-during-animation-cs/samples/sample4.aspx)]

<span data-ttu-id="624ce-125">Také je možné znovu zapnout. pro tlačítko po animace, pomocí následujícího elementu XML na konci tohoto seznamu:</span><span class="sxs-lookup"><span data-stu-id="624ce-125">It would also be possible to re-enable to button after the animation, using the following XML element at the end of the list:</span></span>

[!code-xml[Main](disabling-actions-during-animation-cs/samples/sample5.xml)]

<span data-ttu-id="624ce-126">Ale v této situaci by to byl nemá od tlačítko setmívá a není viditelný na konci animace.</span><span class="sxs-lookup"><span data-stu-id="624ce-126">However in the given scenario this would be useless since the button fades out and is not visible at the end of the animation.</span></span>


<span data-ttu-id="624ce-127">[![Tlačítko vypnutá při spuštění animace](disabling-actions-during-animation-cs/_static/image2.png)](disabling-actions-during-animation-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="624ce-127">[![The button is disabled as soon as the animation runs](disabling-actions-during-animation-cs/_static/image2.png)](disabling-actions-during-animation-cs/_static/image1.png)</span></span>

<span data-ttu-id="624ce-128">Tlačítko vypnutá při spuštění animace ([Kliknutím zobrazit obrázek v plné velikosti](disabling-actions-during-animation-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="624ce-128">The button is disabled as soon as the animation runs ([Click to view full-size image](disabling-actions-during-animation-cs/_static/image3.png))</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="624ce-129">[Předchozí](animating-in-response-to-user-interaction-cs.md)
[další](triggering-an-animation-in-another-control-cs.md)</span><span class="sxs-lookup"><span data-stu-id="624ce-129">[Previous](animating-in-response-to-user-interaction-cs.md)
[Next](triggering-an-animation-in-another-control-cs.md)</span></span>