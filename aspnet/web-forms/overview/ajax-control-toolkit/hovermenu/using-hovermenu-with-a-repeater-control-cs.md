---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
title: "HoverMenu pomocí ovládacího prvku opakovače (C#) | Microsoft Docs"
author: wenz
description: "HoverMenu ovládacího prvku AJAX Control Toolkit poskytuje jednoduché místní vliv: při umístění ukazatele myši nad elementem, se zobrazí místní okno na specifi..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: e7700e7b-edc3-4183-a713-70e507cc7490
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: aac5a26191cc633204549274c327e065578f4226
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/10/2017
---
<a name="using-hovermenu-with-a-repeater-control-c"></a>HoverMenu pomocí ovládacího prvku opakovače (C#)
====================
podle [Christian Wenz](https://github.com/wenz)

[Stáhněte si kód](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) nebo [stáhnout PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)

> HoverMenu ovládacího prvku AJAX Control Toolkit poskytuje jednoduché místní vliv: při umístění ukazatele myši nad elementem, se zobrazí místní okno na zadané pozici. Je také možné použít tento ovládací prvek v rámci prvku repeater.


## <a name="overview"></a>Přehled

`HoverMenu` Ovládacího prvku AJAX Control Toolkit poskytuje jednoduché místní vliv: při umístění ukazatele myši nad elementem, se zobrazí místní okno na zadané pozici. Je také možné použít tento ovládací prvek v rámci prvku repeater.

## <a name="steps"></a>Kroky

První řadě zdroj dat je vyžadován. Tato ukázka používá databázi AdventureWorks a Microsoft SQL Server 2005 Express Edition. Databáze je volitelná součást instalaci sady Visual Studio (včetně express edition) a je také k dispozici jako samostatný soubor ke stažení v rámci [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064). Databázi AdventureWorks je součástí sad SQL Server 2005 ukázky a ukázkové databáze (stáhnout na adrese [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Nejjednodušší způsob, jak nastavit databáze je použití Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx? FamilyID = c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) a připojte `AdventureWorks.mdf` soubor databáze.

Tato ukázka předpokládáme, že je název instance systému SQL Server 2005 Express Edition `SQLEXPRESS` a se nachází na stejném počítači jako webový server; toto je také výchozí nastavení. Pokud vaše instalace se liší, budete muset přizpůsobit informace o připojení pro databázi.

Chcete aktivovat funkce ASP.NET AJAX a sady nástrojů ovládacího prvku `ScriptManager` řízení musíte umístit kdekoli na stránce (ale uvnitř `<form>` element):

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

Pak přidejte zdroje dat na stránku. Chcete-li použít omezené množství dat, jsme vybrat pouze prvních pět položek v tabulce dodavatele databázi AdventureWorks. Pokud používáte pomocníkem pro Visual Studio k vytvoření zdroje dat, paměti, že chyby v aktuální verzi není předpony názvu tabulky (`Vendor`) s `Purchasing`. Následující kód ukazuje správnou syntaxi:

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

V dalším kroku přidejte panel, který slouží jako modální překryvné okno:

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

Nyní `HoverMenuExtender` dodává do play. Tak, aby každý prvek ve zdroji dat získá svůj vlastní místní, musíte být v rámci opakovače umístit rozšiřujícího objektu `<ItemTemplate>` části. Zde je kód:

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

Teď každá položka v datovém zdroji, zobrazí místní okno vpravo (`PopupPosition` atribut) po prodlevě 50 milisekund (`PopDelay` atributu).


[![V nabídce hover se zobrazí vedle každé položky v opakovači](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)

V nabídce hover se zobrazí vedle každé položky v opakovači ([Kliknutím zobrazit obrázek v plné velikosti](using-hovermenu-with-a-repeater-control-cs/_static/image3.png))

>[!div class="step-by-step"]
[Další](using-hovermenu-with-a-repeater-control-vb.md)