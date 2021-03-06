---
title: Vlastní formátovací moduly v ASP.NET Core Web API
author: rick-anderson
description: Naučte se vytvářet a používat vlastní formátovací moduly pro webová rozhraní API v ASP.NET Core.
ms.author: riande
ms.date: 02/08/2017
uid: web-api/advanced/custom-formatters
ms.openlocfilehash: dd25cda460ba758cd07de094eaadd1f2d8c28657
ms.sourcegitcommit: 9a129f5f3e31cc449742b164d5004894bfca90aa
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78667669"
---
# <a name="custom-formatters-in-aspnet-core-web-api"></a>Vlastní formátovací moduly v ASP.NET Core Web API

tím, že [Dykstra](https://github.com/tdykstra)

ASP.NET Core MVC podporuje výměnu dat ve webových rozhraních API pomocí formátování vstupu a výstupu. Vstupní formátovací moduly jsou používány [vazbami modelů](xref:mvc/models/model-binding). Výstupní formátovací moduly se používají k [formátování odpovědí](xref:web-api/advanced/formatting).

Rozhraní poskytuje předdefinované vstupní a výstupní formátovací moduly pro JSON a XML. Poskytuje vestavěný výstupní formátovací modul pro prostý text, ale neposkytuje vstupní formátovací modul pro prostý text.

Tento článek ukazuje, jak přidat podporu pro další formáty vytvořením vlastních formátovacích modulů. Příklad vlastního vstupního formátovacího modulu pro prostý text najdete v tématu [TextPlainInputFormatter](https://github.com/aspnet/Entropy/blob/master/samples/Mvc.Formatters/TextPlainInputFormatter.cs) na GitHubu.

[Zobrazit nebo stáhnout ukázkový kód](https://github.com/dotnet/AspNetCore.Docs/tree/master/aspnetcore/web-api/advanced/custom-formatters/sample) ([Jak stáhnout](xref:index#how-to-download-a-sample))

## <a name="when-to-use-custom-formatters"></a>Kdy použít vlastní formátovací moduly

Vlastní formátovací modul použijte v případě, že chcete, aby proces [vyjednávání obsahu](xref:web-api/advanced/formatting#content-negotiation) podporoval typ obsahu, který není podporován vestavěnými formátovacími moduly.

Pokud například někteří klienti webového rozhraní API mohou zpracovat formát [Protobuf](https://github.com/google/protobuf) , můžete chtít použít Protobuf u těchto klientů, protože je efektivnější. Nebo můžete chtít, aby vaše webové rozhraní API odesílalo jména kontaktů a adresy ve formátu [vCard](https://wikipedia.org/wiki/VCard) , což je běžně používaný formát pro výměnu dat kontaktů. Ukázková aplikace, která je součástí tohoto článku, implementuje jednoduchý formátovací modul vCard.

## <a name="overview-of-how-to-use-a-custom-formatter"></a>Přehled způsobu použití vlastního formátovacího modulu

Tady je postup vytvoření a použití vlastního formátovacího modulu:

* Vytvořte výstupní třídu formátování výstupu, pokud chcete serializovat data pro odeslání klientovi.
* Vytvořte vstupní třídu formátování, pokud chcete deserializovat data přijatá z klienta.
* Přidejte instance formátovacích modulů do kolekce `InputFormatters` a `OutputFormatters` v [MvcOptions](/dotnet/api/microsoft.aspnetcore.mvc.mvcoptions).

Následující části obsahují pokyny a příklady kódu pro každý z těchto kroků.

## <a name="how-to-create-a-custom-formatter-class"></a>Jak vytvořit vlastní třídu formátování

Vytvoření formátovacího modulu:

* Odvodit třídu od příslušné základní třídy.
* Zadejte platné typy médií a kódování v konstruktoru.
* Přepsat `CanReadType`/`CanWriteType` metody
* Přepsat `ReadRequestBodyAsync`/`WriteResponseBodyAsync` metody
  
### <a name="derive-from-the-appropriate-base-class"></a>Odvození od příslušné základní třídy

Pro typy textových médií (například vCard) je odvozen ze základní třídy [TextInputFormatter](/dotnet/api/microsoft.aspnetcore.mvc.formatters.textinputformatter) nebo [TextOutputFormatter](/dotnet/api/microsoft.aspnetcore.mvc.formatters.textoutputformatter) .

[!code-csharp[](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=classdef)]

Příklad vstupního formátovacího modulu najdete v [ukázkové aplikaci](https://github.com/dotnet/AspNetCore.Docs/tree/master/aspnetcore/web-api/advanced/custom-formatters/sample).

Pro binární typy je odvozeno od základní třídy [InputFormatter](/dotnet/api/microsoft.aspnetcore.mvc.formatters.inputformatter) nebo [OutputFormatter](/dotnet/api/microsoft.aspnetcore.mvc.formatters.outputformatter) .

### <a name="specify-valid-media-types-and-encodings"></a>Zadejte platné typy médií a kódování.

V konstruktoru zadejte platné typy médií a kódování přidáním do kolekce `SupportedMediaTypes` a `SupportedEncodings`.

[!code-csharp[](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=ctor&highlight=3,5-6)]

Příklad vstupního formátovacího modulu najdete v [ukázkové aplikaci](https://github.com/dotnet/AspNetCore.Docs/tree/master/aspnetcore/web-api/advanced/custom-formatters/sample).

> [!NOTE]
> Vložení závislosti konstruktoru nelze provést ve třídě formátovacího modulu. Například nemůžete získat protokolovací nástroj přidáním parametru protokolovacího nástroje do konstruktoru. Pro přístup ke službám je nutné použít objekt kontextu, který se předává do vašich metod. [Následující](#read-write) příklad kódu ukazuje, jak to provést.

### <a name="override-canreadtypecanwritetype"></a>Přepsat CanReadType/CanWriteType

Zadejte typ, který lze deserializovat nebo serializovat, přepsáním `CanReadType` nebo `CanWriteType`ch metod. Můžete například vytvořit text v vCard pouze z `Contact`ho typu a naopak.

[!code-csharp[](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=canwritetype)]

Příklad vstupního formátovacího modulu najdete v [ukázkové aplikaci](https://github.com/dotnet/AspNetCore.Docs/tree/master/aspnetcore/web-api/advanced/custom-formatters/sample).

#### <a name="the-canwriteresult-method"></a>Metoda CanWriteResult

V některých případech je nutné přepsat `CanWriteResult` místo `CanWriteType`. Pokud jsou splněné následující podmínky, použijte `CanWriteResult`:

* Vaše metoda akce vrátí třídu modelu.
* K dispozici jsou odvozené třídy, které mohou být vráceny za běhu.
* Je potřeba znát za běhu, který tato akce vrátila odvozenou třídu.

Předpokládejme například, že váš podpis metody akce vrací typ `Person`, ale může vracet `Student` nebo `Instructor` typ, který je odvozen od `Person`. Chcete-li, aby formátovací modul zpracovával pouze `Student` objekty, ověřte typ [objektu](/dotnet/api/microsoft.aspnetcore.mvc.formatters.outputformattercanwritecontext.object#Microsoft_AspNetCore_Mvc_Formatters_OutputFormatterCanWriteContext_Object) v objektu Context, který je k dispozici metodě `CanWriteResult`. Všimněte si, že není nutné použít `CanWriteResult`, když metoda akce vrátí `IActionResult`; v takovém případě metoda `CanWriteType` přijímá typ modulu runtime.

<a id="read-write"></a>

### <a name="override-readrequestbodyasyncwriteresponsebodyasync"></a>Override ReadRequestBodyAsync/WriteResponseBodyAsync

Provedete skutečnou práci při deserializaci nebo serializaci v `ReadRequestBodyAsync` nebo `WriteResponseBodyAsync`. Zvýrazněné řádky v následujícím příkladu ukazují, jak získat služby z kontejneru vkládání závislostí (nemůžete je získat z parametrů konstruktoru).

[!code-csharp[](custom-formatters/sample/Formatters/VcardOutputFormatter.cs?name=writeresponse&highlight=3-4)]

Příklad vstupního formátovacího modulu najdete v [ukázkové aplikaci](https://github.com/dotnet/AspNetCore.Docs/tree/master/aspnetcore/web-api/advanced/custom-formatters/sample).

## <a name="how-to-configure-mvc-to-use-a-custom-formatter"></a>Jak konfigurovat MVC pro použití vlastního formátovacího modulu

Chcete-li použít vlastní formátovací modul, přidejte instanci formátovací třídy do kolekce `InputFormatters` nebo `OutputFormatters`.

[!code-csharp[](custom-formatters/sample/Startup.cs?name=mvcoptions&highlight=3-4)]

Formátovací moduly jsou vyhodnocovány v pořadí, ve kterém je vložíte. První z nich má přednost.

## <a name="next-steps"></a>Další kroky

* [Ukázková aplikace pro tento dokument](https://github.com/dotnet/AspNetCore.Docs/tree/master/aspnetcore/web-api/advanced/custom-formatters/sample), která implementuje jednoduché formátovací a výstupní formátovací moduly vCard Aplikace čte a zapisuje soubory vCard, které vypadají jako v následujícím příkladu:

```
BEGIN:VCARD
VERSION:2.1
N:Davolio;Nancy
FN:Nancy Davolio
UID:20293482-9240-4d68-b475-325df4a83728
END:VCARD
```

Chcete-li zobrazit výstup v programu vCard, spusťte aplikaci a odešlete požadavek GET s hlavičkou Accept "text/vCard" do `http://localhost:63313/api/contacts/` (při spuštění ze sady Visual Studio) nebo `http://localhost:5000/api/contacts/` (při spuštění z příkazového řádku).

Chcete-li přidat soubor vCard do kolekce kontaktů v paměti, odešlete požadavek post na stejnou adresu URL s hlavičkou Content-Type "text/vCard" a textem vCard v těle, který je formátován jako příklad výše.
