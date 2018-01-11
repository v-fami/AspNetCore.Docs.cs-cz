---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
title: "Použití více ovládacích prvků místní (VB) | Microsoft Docs"
author: wenz
description: "Rozšiřujícího objektu PopupControl v Toolkitu AJAX nabízí snadný způsob, jak aktivovat místní okno, pokud je aktivován další ovládací prvek. Je také možné použít m..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 4da43d77-f6c4-43a8-9124-f1e8e1c8f0a2
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 32e170ebd78a6f849004e789f53c03d9cd40be01
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/10/2017
---
<a name="using-multiple-popup-controls-vb"></a>Použití více ovládacích prvků místní (VB)
====================
podle [Christian Wenz](https://github.com/wenz)

[Stáhněte si kód](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.vb.zip) nebo [stáhnout PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1VB.pdf)

> Rozšiřujícího objektu PopupControl v Toolkitu AJAX nabízí snadný způsob, jak aktivovat místní okno, pokud je aktivován další ovládací prvek. Je také možné použít více než jeden prvek automaticky otevřeném okně na jedné stránce.


## <a name="overview"></a>Přehled

Rozšiřujícího objektu PopupControl v Toolkitu AJAX nabízí snadný způsob, jak aktivovat místní okno, pokud je aktivován další ovládací prvek. Je také možné použít více než jeden prvek automaticky otevřeném okně na jedné stránce.

## <a name="steps"></a>Kroky

Chcete aktivovat funkce ASP.NET AJAX a sady nástrojů ovládacího prvku `ScriptManager` řízení musíte umístit kdekoli na stránce (ale uvnitř `<form>` element):

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample1.aspx)]

Dál přidejte panel, který slouží jako místní nabídce. Scénář, aktuální, obsahuje panel `Calendar` ovládacího prvku. Aby se zabránilo aktualizace stránky způsobené postback v kalendáři, panelu zprovozněn v rámci `UpdatePanel` ovládacího prvku:

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample2.aspx)]

Tato stránka také obsahuje dvě textová pole. Pro každého textového pole se zobrazí místní nabídka kalendáře po aktivaci textového pole.

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample3.aspx)]

Nyní rozšiřte každou z do dvou textových polí s `PopupControlExtender`. `TargetControlID` Atribut poskytuje ID ovládacího prvku vázáno rozšiřujícího objektu. `PopupControlID` Atribut obsahuje ID místní panelu. V takovém případě obou Extender zobrazit panel stejné, ale jiné panelů je také možné.

[!code-aspx[Main](using-multiple-popup-controls-vb/samples/sample4.aspx)]

Nyní vždy, když kliknete na tlačítko v textovém poli, kalendář se objeví pod polem, což vám umožní vybrat datum. (Získávání vybrané data zpět do textových polí se budeme v různých kurzu.)


[![Kalendář se zobrazí, když uživatel klikne do textového pole](using-multiple-popup-controls-vb/_static/image2.png)](using-multiple-popup-controls-vb/_static/image1.png)

Kalendář se zobrazí, když uživatel klikne do textového pole ([Kliknutím zobrazit obrázek v plné velikosti](using-multiple-popup-controls-vb/_static/image3.png))

>[!div class="step-by-step"]
[Předchozí](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs.md)
[další](handling-postbacks-from-a-popup-control-with-an-updatepanel-vb.md)