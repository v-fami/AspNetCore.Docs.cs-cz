---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
title: "Spuštění animace v další ovládací prvek (VB) | Microsoft Docs"
author: wenz
description: "V sadě nástrojů ovládacího prvku ASP.NET AJAX ovládacího prvku animace není právě ovládací prvek ale celé rozhraní pro přidání do ovládacího prvku animace. Obecně platí, spouštění..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 25ebaf1f-5a9f-423d-98c7-1d694e93664f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-vb
msc.type: authoredcontent
ms.openlocfilehash: ce1d29cbd06ef8a470780ff4c7bda8039575d59f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/10/2017
---
<a name="triggering-an-animation-in-another-control-vb"></a>Spuštění animace v další ovládací prvek (VB)
====================
podle [Christian Wenz](https://github.com/wenz)

[Stáhněte si kód](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.vb.zip) nebo [stáhnout PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8VB.pdf)

> V sadě nástrojů ovládacího prvku ASP.NET AJAX ovládacího prvku animace není právě ovládací prvek ale celé rozhraní pro přidání do ovládacího prvku animace. Obecně platí spuštění animace se aktivuje interakce uživatele s stejný ovládací prvek. Je však také možné pracovat s jeden ovládací prvek a potom animace jiného ovládacího prvku.


## <a name="overview"></a>Přehled

V sadě nástrojů ovládacího prvku ASP.NET AJAX ovládacího prvku animace není právě ovládací prvek ale celé rozhraní pro přidání do ovládacího prvku animace. Obecně platí spuštění animace se aktivuje interakce uživatele s stejný ovládací prvek. Je však také možné pracovat s jeden ovládací prvek a potom animace jiného ovládacího prvku.

## <a name="steps"></a>Kroky

První řadě zahrnují `ScriptManager` na stránce; potom knihovny ASP.NET AJAX je načtena, aby bylo možné použít Toolkitu:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample1.aspx)]

Animace se použijí na panel textu, který vypadá takto:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample2.aspx)]

Související třídy CSS pro panel definovat barvu pozadí dobrý a také nastavit pevnou šířku pro panel:

[!code-css[Main](triggering-an-animation-in-another-control-vb/samples/sample3.css)]

Pokud chcete začít animace panelu, je HTML tlačítko použít. Všimněte si, že `<input type="button" />` je nejvyšších přes `<asp:Button />` vzhledem k tomu, že jsme nechcete, aby zpětné volání po kliknutí na toto tlačítko.

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample4.aspx)]

Poté, přidejte `AnimationExtender` na stránku, poskytuje `ID`, `TargetControlID` atribut a povinný údaj `runat="server"`. Je důležité nastavit `TargetControlID` na ID tlačítko (elementu spuštění animace), ne na ID panelu (elementu se animovaný)

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample5.aspx)]

V rámci `<Animations>` uzlu, místní animací jako obvykle. Aby bylo možné je změnit panelu, ne na tlačítko nastavit `AnimationTarget` atribut pro každý element animace, v rámci `AnimationExtender`. Hodnota `AnimationTarget` samozřejmě je ID panelu. Tímto způsobem animací dojít s panelem, ne při spouštěcí tlačítko. Tady je `AnimationExtender` kód pro tento scénář:

[!code-aspx[Main](triggering-an-animation-in-another-control-vb/samples/sample6.aspx)]

Všimněte si, speciální pořadí, ve kterém se zobrazují jednotlivé animace. Tlačítko získá první řadě deaktivovat po spuštění animace. Vzhledem k tomu, že je žádné `AnimationTarget` atribut `<EnableAction>` elementu, tato animace se použije pro původní ovládacího prvku: tlačítko. Animace následující dva kroky se provádějí parallelly (`<Parallel>` element). Mají obě jejich `AnimationTarget` atributy nastavit na `"Panel1"`, proto animace panelu, není tlačítko.


[![Panel animace spuštěna, myši klikněte na tlačítko](triggering-an-animation-in-another-control-vb/_static/image2.png)](triggering-an-animation-in-another-control-vb/_static/image1.png)

Panel animace spuštěna, myši klikněte na tlačítko ([Kliknutím zobrazit obrázek v plné velikosti](triggering-an-animation-in-another-control-vb/_static/image3.png))

>[!div class="step-by-step"]
[Předchozí](disabling-actions-during-animation-vb.md)
[další](modifying-animations-from-the-server-side-vb.md)