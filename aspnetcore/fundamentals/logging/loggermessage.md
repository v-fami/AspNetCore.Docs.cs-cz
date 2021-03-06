---
title: Protokolování s vysokým výkonem pomocí LoggerMessage v ASP.NET Core
author: rick-anderson
description: Naučte se používat LoggerMessage k vytváření protokolovaných delegátů, kteří vyžadují méně přidělení objektů pro scénáře protokolování s vysokým výkonem.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 08/26/2019
uid: fundamentals/logging/loggermessage
ms.openlocfilehash: 48ebba69b5c15a0f9a42f7f6b3d2c1fcb0a2211c
ms.sourcegitcommit: 9a129f5f3e31cc449742b164d5004894bfca90aa
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78663217"
---
# <a name="high-performance-logging-with-loggermessage-in-aspnet-core"></a>Protokolování s vysokým výkonem pomocí LoggerMessage v ASP.NET Core

::: moniker range=">= aspnetcore-3.0"

<xref:Microsoft.Extensions.Logging.LoggerMessage> funkce vytvářejí delegáty, které umožňují ukládání do mezipaměti, které vyžadují méně přidělení objektů a snižují výpočetní režii v porovnání s [metodami rozšíření protokolovacího](xref:Microsoft.Extensions.Logging.LoggerExtensions)nástroje, jako jsou <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogInformation*> a <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogDebug*>. Pro scénáře protokolování s vysokým výkonem použijte model <xref:Microsoft.Extensions.Logging.LoggerMessage>.

<xref:Microsoft.Extensions.Logging.LoggerMessage> poskytuje následující výhody výkonu prostřednictvím rozšiřujících metod protokolovacího nástroje:

* Metody rozšíření protokolovacího nástroje vyžadují "zabalení" (převod) typů hodnot, například `int`, do `object`. Vzor <xref:Microsoft.Extensions.Logging.LoggerMessage> zabraňuje zabalení pomocí statických <xref:System.Action> polí a metod rozšíření s parametry silného typu.
* Metody rozšíření protokolovacího nástroje musí při každém zápisu zprávy protokolu analyzovat šablonu zprávy (pojmenovaný řetězec formátu). <xref:Microsoft.Extensions.Logging.LoggerMessage> vyžaduje pouze analýzu šablony při definování zprávy.

[Zobrazit nebo stáhnout ukázkový kód](https://github.com/dotnet/AspNetCore.Docs/tree/master/aspnetcore/fundamentals/logging/loggermessage/samples/) ([Jak stáhnout](xref:index#how-to-download-a-sample))

Ukázková aplikace předvádí <xref:Microsoft.Extensions.Logging.LoggerMessage> funkce se základním systémem pro sledování nabídek. Aplikace přidá a odstraní uvozovky pomocí databáze v paměti. Při výskytu těchto operací se zprávy protokolu generují pomocí <xref:Microsoft.Extensions.Logging.LoggerMessage>ho vzoru.

## <a name="loggermessagedefine"></a>LoggerMessage. define

[Define (LogLevel, ID události, String)](xref:Microsoft.Extensions.Logging.LoggerMessage.Define*) vytvoří delegáta <xref:System.Action> pro protokolování zprávy. <xref:Microsoft.Extensions.Logging.LoggerMessage.Define*> přetížení umožňuje předat až šest parametrů typu pojmenovanému formátovacímu řetězci (šabloně).

Řetězec poskytnutý metodě <xref:Microsoft.Extensions.Logging.LoggerMessage.Define*> je šablona, nikoli interpolovaná řetězec. Zástupné symboly jsou vyplněny v pořadí, v jakém jsou typy zadány. Zástupné názvy v šabloně by měly být popisné a konzistentní v rámci šablon. Slouží jako názvy vlastností v rámci strukturovaných dat protokolu. Pro názvy zástupných symbolů doporučujeme použít [velká písmena Pascal](/dotnet/standard/design-guidelines/capitalization-conventions) . Například `{Count}``{FirstName}`.

Každá zpráva protokolu je <xref:System.Action> uchovávána ve statickém poli vytvořeném pomocí [LoggerMessage. define](xref:Microsoft.Extensions.Logging.LoggerMessage.Define*). Ukázková aplikace například vytvoří pole pro popis zprávy protokolu pro požadavek GET na stránku indexu (*interní/LoggerExtensions. cs*):

[!code-csharp[](loggermessage/samples/3.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet1)]

Pro <xref:System.Action>zadejte:

* Úroveň protokolování
* Jedinečný identifikátor události (<xref:Microsoft.Extensions.Logging.EventId>) s názvem statické metody rozšíření.
* Šablona zprávy (pojmenovaný řetězec formátu). 

Požadavek na stránku index ukázkové aplikace nastaví:

* Úroveň protokolu `Information`.
* ID události, která se má `1` s názvem metody `IndexPageRequested`
* Šablona zprávy (pojmenovaný řetězec formátu) k řetězci.

[!code-csharp[](loggermessage/samples/3.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet5)]

Úložiště strukturovaného protokolování můžou použít název události, když se poskytne s ID události pro rozšíření protokolování. [Serilog](https://github.com/serilog/serilog-extensions-logging) například používá název události.

<xref:System.Action> je vyvolána prostřednictvím rozšiřující metody silného typu. Metoda `IndexPageRequested` zaznamená zprávu o žádosti o načtení stránky indexu v ukázkové aplikaci:

[!code-csharp[](loggermessage/samples/3.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet9)]

`IndexPageRequested` se volá v protokolovacím nástroji v metodě `OnGetAsync` na *stránce pages/index. cshtml. cs*:

[!code-csharp[](loggermessage/samples/3.x/LoggerMessageSample/Pages/Index.cshtml.cs?name=snippet2&highlight=3)]

Zkontrolujte výstup konzoly aplikace:

```console
info: LoggerMessageSample.Pages.IndexModel[1]
      => RequestId:0HL90M6E7PHK4:00000001 RequestPath:/ => /Index
      GET request for Index page
```

Chcete-li předat parametry do zprávy protokolu, definujte při vytváření statického pole až šest typů. Ukázková aplikace při přidávání nabídky zapisuje řetězec definováním typu `string` pro pole <xref:System.Action>:

[!code-csharp[](loggermessage/samples/3.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet2)]

Šablona zprávy protokolu delegáta přijímá své zástupné hodnoty z poskytnutých typů. Ukázková aplikace definuje delegáta pro přidání nabídky, kde je parametr Quota `string`:

[!code-csharp[](loggermessage/samples/3.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet6)]

Statická rozšiřující metoda pro přidání nabídky, `QuoteAdded`, přijímá hodnotu argumentu citace a předá ji delegátovi <xref:System.Action>:

[!code-csharp[](loggermessage/samples/3.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet10)]

V modelu stránky indexu stránky (*pages/index. cshtml. cs*) se volá `QuoteAdded` k zaznamenání zprávy:

[!code-csharp[](loggermessage/samples/3.x/LoggerMessageSample/Pages/Index.cshtml.cs?name=snippet3&highlight=6)]

Zkontrolujte výstup konzoly aplikace:

```console
info: LoggerMessageSample.Pages.IndexModel[2]
      => RequestId:0HL90M6E7PHK5:0000000A RequestPath:/ => /Index
      Quote added (Quote = 'You can avoid reality, but you cannot avoid the 
          consequences of avoiding reality. - Ayn Rand')
```

Ukázková aplikace implementuje vzor [zachycení try&ndash;](/dotnet/csharp/language-reference/keywords/try-catch) pro odstranění nabídky. Informační zpráva se zaznamená do protokolu pro úspěšnou operaci odstranění. Pokud je vyvolána výjimka, je zaznamenána chybová zpráva pro operaci odstranění. Zpráva protokolu pro neúspěšnou operaci odstranění zahrnuje trasování zásobníku výjimky (*interní/LoggerExtensions. cs*):

[!code-csharp[](loggermessage/samples/3.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet3)]

[!code-csharp[](loggermessage/samples/3.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet7)]

Všimněte si, jak je výjimka předána delegátovi v `QuoteDeleteFailed`:

[!code-csharp[](loggermessage/samples/3.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet11)]

V modelu stránky pro stránku indexu volání úspěšného odstranění citace volá metodu `QuoteDeleted` v protokolovacím nástroji. Pokud se nabídka nenajde pro odstranění, vyvolá se <xref:System.ArgumentNullException>. Výjimka je zachycena příkazem [try&ndash;catch](/dotnet/csharp/language-reference/keywords/try-catch) a zaznamenána voláním metody `QuoteDeleteFailed` v protokolovacím nástroji v bloku [catch](/dotnet/csharp/language-reference/keywords/try-catch) (*pages/index. cshtml. cs*):

[!code-csharp[](loggermessage/samples/3.x/LoggerMessageSample/Pages/Index.cshtml.cs?name=snippet5&highlight=9,13)]

Po úspěšném odstranění nabídky zkontrolujte výstup konzoly aplikace:

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:00000016 RequestPath:/ => /Index
      Quote deleted (Quote = 'You can avoid reality, but you cannot avoid the 
          consequences of avoiding reality. - Ayn Rand' Id = 1)
```

Pokud se odstranění citace nepovede, zkontrolujte výstup konzoly aplikace. Všimněte si, že je tato výjimka součástí zprávy protokolu:

```console
LoggerMessageSample.Pages.IndexModel: Error: Quote delete failed (Id = 999)

System.NullReferenceException: Object reference not set to an instance of an object.
   at lambda_method(Closure , ValueBuffer )
   at System.Linq.Enumerable.SelectEnumerableIterator`2.MoveNext()
   at Microsoft.EntityFrameworkCore.InMemory.Query.Internal.InMemoryShapedQueryCompilingExpressionVisitor.AsyncQueryingEnumerable`1.AsyncEnumerator.MoveNextAsync()
   at Microsoft.EntityFrameworkCore.Query.ShapedQueryCompilingExpressionVisitor.SingleOrDefaultAsync[TSource](IAsyncEnumerable`1 asyncEnumerable, CancellationToken cancellationToken)
   at Microsoft.EntityFrameworkCore.Query.ShapedQueryCompilingExpressionVisitor.SingleOrDefaultAsync[TSource](IAsyncEnumerable`1 asyncEnumerable, CancellationToken cancellationToken)
   at LoggerMessageSample.Pages.IndexModel.OnPostDeleteQuoteAsync(Int32 id) in c:\Users\guard\Documents\GitHub\Docs\aspnetcore\fundamentals\logging\loggermessage\samples\3.x\LoggerMessageSample\Pages\Index.cshtml.cs:line 77
```

## <a name="loggermessagedefinescope"></a>LoggerMessage. Definescope –

[Definescope – (String)](xref:Microsoft.Extensions.Logging.LoggerMessage.DefineScope*) vytvoří delegáta <xref:System.Func%601> pro definování [oboru protokolu](xref:fundamentals/logging/index#log-scopes). <xref:Microsoft.Extensions.Logging.LoggerMessage.DefineScope*> přetížení povoluje předání až tří parametrů typu pojmenovanému formátovacímu řetězci (Template).

Stejně jako v případě metody <xref:Microsoft.Extensions.Logging.LoggerMessage.Define*> je řetězec poskytnutý metodě <xref:Microsoft.Extensions.Logging.LoggerMessage.DefineScope*> šablona, nikoli interpolovaná řetězcová metoda. Zástupné symboly jsou vyplněny v pořadí, v jakém jsou typy zadány. Zástupné názvy v šabloně by měly být popisné a konzistentní v rámci šablon. Slouží jako názvy vlastností v rámci strukturovaných dat protokolu. Pro názvy zástupných symbolů doporučujeme použít [velká písmena Pascal](/dotnet/standard/design-guidelines/capitalization-conventions) . Například `{Count}``{FirstName}`.

Zadejte [Rozsah protokolu](xref:fundamentals/logging/index#log-scopes) , který se má použít pro řadu zpráv protokolu pomocí metody <xref:Microsoft.Extensions.Logging.LoggerMessage.DefineScope*>.

Ukázková aplikace má tlačítko **Zrušit vše** pro odstranění všech nabídek v databázi. Tyto nabídky jsou odstraněny po jednom jejich odebráním. Pokaždé, když je odstraněna citace, je volána metoda `QuoteDeleted` pro protokolovací nástroj. Do těchto zpráv protokolu se přidá rozsah protokolu.

Povolit `IncludeScopes` v části protokolovacího nástroje konzoly *appSettings. JSON*:

[!code-csharp[](loggermessage/samples/3.x/LoggerMessageSample/appsettings.json?highlight=3-5)]

Chcete-li vytvořit rozsah protokolu, přidejte pole pro blokování <xref:System.Func%601> delegáta oboru. Ukázková aplikace vytvoří pole s názvem `_allQuotesDeletedScope` (*interní/LoggerExtensions. cs*):

[!code-csharp[](loggermessage/samples/3.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet4)]

K vytvoření delegáta použijte <xref:Microsoft.Extensions.Logging.LoggerMessage.DefineScope*>. Až tři typy lze zadat pro použití jako argumenty šablony při volání delegáta. Ukázková aplikace používá šablonu zprávy, která obsahuje počet odstraněných uvozovek (`int` typ):

[!code-csharp[](loggermessage/samples/3.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet8)]

Zadejte statickou metodu rozšíření pro zprávu protokolu. Zahrňte všechny parametry typu pro pojmenované vlastnosti, které se zobrazí v šabloně zprávy. Ukázková aplikace přebírá `count` nabídky k odstranění a vrácení `_allQuotesDeletedScope`:

[!code-csharp[](loggermessage/samples/3.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet12)]

Obor zabalí volání rozšíření protokolování v bloku [using](/dotnet/csharp/language-reference/keywords/using-statement) :

[!code-csharp[](loggermessage/samples/3.x/LoggerMessageSample/Pages/Index.cshtml.cs?name=snippet4&highlight=5-6,14)]

Zkontrolujte zprávy protokolu ve výstupu konzoly aplikace. Následující výsledek obsahuje tři nabídky odstraněné se zprávou rozsah protokolu, která je součástí:

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => 
          All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 1' Id = 2)
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => 
          All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 2' Id = 3)
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => 
          All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 3' Id = 4)
```

::: moniker-end

::: moniker range="< aspnetcore-3.0"

<xref:Microsoft.Extensions.Logging.LoggerMessage> funkce vytvářejí delegáty, které umožňují ukládání do mezipaměti, které vyžadují méně přidělení objektů a snižují výpočetní režii v porovnání s [metodami rozšíření protokolovacího](xref:Microsoft.Extensions.Logging.LoggerExtensions)nástroje, jako jsou <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogInformation*> a <xref:Microsoft.Extensions.Logging.LoggerExtensions.LogDebug*>. Pro scénáře protokolování s vysokým výkonem použijte model <xref:Microsoft.Extensions.Logging.LoggerMessage>.

<xref:Microsoft.Extensions.Logging.LoggerMessage> poskytuje následující výhody výkonu prostřednictvím rozšiřujících metod protokolovacího nástroje:

* Metody rozšíření protokolovacího nástroje vyžadují "zabalení" (převod) typů hodnot, například `int`, do `object`. Vzor <xref:Microsoft.Extensions.Logging.LoggerMessage> zabraňuje zabalení pomocí statických <xref:System.Action> polí a metod rozšíření s parametry silného typu.
* Metody rozšíření protokolovacího nástroje musí při každém zápisu zprávy protokolu analyzovat šablonu zprávy (pojmenovaný řetězec formátu). <xref:Microsoft.Extensions.Logging.LoggerMessage> vyžaduje pouze analýzu šablony při definování zprávy.

[Zobrazit nebo stáhnout ukázkový kód](https://github.com/dotnet/AspNetCore.Docs/tree/master/aspnetcore/fundamentals/logging/loggermessage/samples/) ([Jak stáhnout](xref:index#how-to-download-a-sample))

Ukázková aplikace předvádí <xref:Microsoft.Extensions.Logging.LoggerMessage> funkce se základním systémem pro sledování nabídek. Aplikace přidá a odstraní uvozovky pomocí databáze v paměti. Při výskytu těchto operací se zprávy protokolu generují pomocí <xref:Microsoft.Extensions.Logging.LoggerMessage>ho vzoru.

## <a name="loggermessagedefine"></a>LoggerMessage. define

[Define (LogLevel, ID události, String)](xref:Microsoft.Extensions.Logging.LoggerMessage.Define*) vytvoří delegáta <xref:System.Action> pro protokolování zprávy. <xref:Microsoft.Extensions.Logging.LoggerMessage.Define*> přetížení umožňuje předat až šest parametrů typu pojmenovanému formátovacímu řetězci (šabloně).

Řetězec poskytnutý metodě <xref:Microsoft.Extensions.Logging.LoggerMessage.Define*> je šablona, nikoli interpolovaná řetězec. Zástupné symboly jsou vyplněny v pořadí, v jakém jsou typy zadány. Zástupné názvy v šabloně by měly být popisné a konzistentní v rámci šablon. Slouží jako názvy vlastností v rámci strukturovaných dat protokolu. Pro názvy zástupných symbolů doporučujeme použít [velká písmena Pascal](/dotnet/standard/design-guidelines/capitalization-conventions) . Například `{Count}``{FirstName}`.

Každá zpráva protokolu je <xref:System.Action> uchovávána ve statickém poli vytvořeném pomocí [LoggerMessage. define](xref:Microsoft.Extensions.Logging.LoggerMessage.Define*). Ukázková aplikace například vytvoří pole pro popis zprávy protokolu pro požadavek GET na stránku indexu (*interní/LoggerExtensions. cs*):

[!code-csharp[](loggermessage/samples/2.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet1)]

Pro <xref:System.Action>zadejte:

* Úroveň protokolování
* Jedinečný identifikátor události (<xref:Microsoft.Extensions.Logging.EventId>) s názvem statické metody rozšíření.
* Šablona zprávy (pojmenovaný řetězec formátu). 

Požadavek na stránku index ukázkové aplikace nastaví:

* Úroveň protokolu `Information`.
* ID události, která se má `1` s názvem metody `IndexPageRequested`
* Šablona zprávy (pojmenovaný řetězec formátu) k řetězci.

[!code-csharp[](loggermessage/samples/2.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet5)]

Úložiště strukturovaného protokolování můžou použít název události, když se poskytne s ID události pro rozšíření protokolování. [Serilog](https://github.com/serilog/serilog-extensions-logging) například používá název události.

<xref:System.Action> je vyvolána prostřednictvím rozšiřující metody silného typu. Metoda `IndexPageRequested` zaznamená zprávu o žádosti o načtení stránky indexu v ukázkové aplikaci:

[!code-csharp[](loggermessage/samples/2.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet9)]

`IndexPageRequested` se volá v protokolovacím nástroji v metodě `OnGetAsync` na *stránce pages/index. cshtml. cs*:

[!code-csharp[](loggermessage/samples/2.x/LoggerMessageSample/Pages/Index.cshtml.cs?name=snippet2&highlight=3)]

Zkontrolujte výstup konzoly aplikace:

```console
info: LoggerMessageSample.Pages.IndexModel[1]
      => RequestId:0HL90M6E7PHK4:00000001 RequestPath:/ => /Index
      GET request for Index page
```

Chcete-li předat parametry do zprávy protokolu, definujte při vytváření statického pole až šest typů. Ukázková aplikace při přidávání nabídky zapisuje řetězec definováním typu `string` pro pole <xref:System.Action>:

[!code-csharp[](loggermessage/samples/2.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet2)]

Šablona zprávy protokolu delegáta přijímá své zástupné hodnoty z poskytnutých typů. Ukázková aplikace definuje delegáta pro přidání nabídky, kde je parametr Quota `string`:

[!code-csharp[](loggermessage/samples/2.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet6)]

Statická rozšiřující metoda pro přidání nabídky, `QuoteAdded`, přijímá hodnotu argumentu citace a předá ji delegátovi <xref:System.Action>:

[!code-csharp[](loggermessage/samples/2.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet10)]

V modelu stránky indexu stránky (*pages/index. cshtml. cs*) se volá `QuoteAdded` k zaznamenání zprávy:

[!code-csharp[](loggermessage/samples/2.x/LoggerMessageSample/Pages/Index.cshtml.cs?name=snippet3&highlight=6)]

Zkontrolujte výstup konzoly aplikace:

```console
info: LoggerMessageSample.Pages.IndexModel[2]
      => RequestId:0HL90M6E7PHK5:0000000A RequestPath:/ => /Index
      Quote added (Quote = 'You can avoid reality, but you cannot avoid the 
          consequences of avoiding reality. - Ayn Rand')
```

Ukázková aplikace implementuje vzor [zachycení try&ndash;](/dotnet/csharp/language-reference/keywords/try-catch) pro odstranění nabídky. Informační zpráva se zaznamená do protokolu pro úspěšnou operaci odstranění. Pokud je vyvolána výjimka, je zaznamenána chybová zpráva pro operaci odstranění. Zpráva protokolu pro neúspěšnou operaci odstranění zahrnuje trasování zásobníku výjimky (*interní/LoggerExtensions. cs*):

[!code-csharp[](loggermessage/samples/2.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet3)]

[!code-csharp[](loggermessage/samples/2.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet7)]

Všimněte si, jak je výjimka předána delegátovi v `QuoteDeleteFailed`:

[!code-csharp[](loggermessage/samples/2.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet11)]

V modelu stránky pro stránku indexu volání úspěšného odstranění citace volá metodu `QuoteDeleted` v protokolovacím nástroji. Pokud se nabídka nenajde pro odstranění, vyvolá se <xref:System.ArgumentNullException>. Výjimka je zachycena příkazem [try&ndash;catch](/dotnet/csharp/language-reference/keywords/try-catch) a zaznamenána voláním metody `QuoteDeleteFailed` v protokolovacím nástroji v bloku [catch](/dotnet/csharp/language-reference/keywords/try-catch) (*pages/index. cshtml. cs*):

[!code-csharp[](loggermessage/samples/2.x/LoggerMessageSample/Pages/Index.cshtml.cs?name=snippet5&highlight=14,18)]

Po úspěšném odstranění nabídky zkontrolujte výstup konzoly aplikace:

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:00000016 RequestPath:/ => /Index
      Quote deleted (Quote = 'You can avoid reality, but you cannot avoid the 
          consequences of avoiding reality. - Ayn Rand' Id = 1)
```

Pokud se odstranění citace nepovede, zkontrolujte výstup konzoly aplikace. Všimněte si, že je tato výjimka součástí zprávy protokolu:

```console
fail: LoggerMessageSample.Pages.IndexModel[5]
      => RequestId:0HL90M6E7PHK5:00000010 RequestPath:/ => /Index
      Quote delete failed (Id = 999)
System.ArgumentNullException: Value cannot be null.
Parameter name: entity
   at Microsoft.EntityFrameworkCore.Utilities.Check.NotNull[T]
       (T value, String parameterName)
   at Microsoft.EntityFrameworkCore.DbContext.Remove[TEntity](TEntity entity)
   at Microsoft.EntityFrameworkCore.Internal.InternalDbSet`1.Remove(TEntity entity)
   at LoggerMessageSample.Pages.IndexModel.<OnPostDeleteQuoteAsync>d__14.MoveNext() 
      in <PATH>\sample\Pages\Index.cshtml.cs:line 87
```

## <a name="loggermessagedefinescope"></a>LoggerMessage. Definescope –

[Definescope – (String)](xref:Microsoft.Extensions.Logging.LoggerMessage.DefineScope*) vytvoří delegáta <xref:System.Func%601> pro definování [oboru protokolu](xref:fundamentals/logging/index#log-scopes). <xref:Microsoft.Extensions.Logging.LoggerMessage.DefineScope*> přetížení povoluje předání až tří parametrů typu pojmenovanému formátovacímu řetězci (Template).

Stejně jako v případě metody <xref:Microsoft.Extensions.Logging.LoggerMessage.Define*> je řetězec poskytnutý metodě <xref:Microsoft.Extensions.Logging.LoggerMessage.DefineScope*> šablona, nikoli interpolovaná řetězcová metoda. Zástupné symboly jsou vyplněny v pořadí, v jakém jsou typy zadány. Zástupné názvy v šabloně by měly být popisné a konzistentní v rámci šablon. Slouží jako názvy vlastností v rámci strukturovaných dat protokolu. Pro názvy zástupných symbolů doporučujeme použít [velká písmena Pascal](/dotnet/standard/design-guidelines/capitalization-conventions) . Například `{Count}``{FirstName}`.

Zadejte [Rozsah protokolu](xref:fundamentals/logging/index#log-scopes) , který se má použít pro řadu zpráv protokolu pomocí metody <xref:Microsoft.Extensions.Logging.LoggerMessage.DefineScope*>.

Ukázková aplikace má tlačítko **Zrušit vše** pro odstranění všech nabídek v databázi. Tyto nabídky jsou odstraněny po jednom jejich odebráním. Pokaždé, když je odstraněna citace, je volána metoda `QuoteDeleted` pro protokolovací nástroj. Do těchto zpráv protokolu se přidá rozsah protokolu.

Povolit `IncludeScopes` v části protokolovacího nástroje konzoly *appSettings. JSON*:

[!code-csharp[](loggermessage/samples/2.x/LoggerMessageSample/appsettings.json?highlight=3-5)]

Chcete-li vytvořit rozsah protokolu, přidejte pole pro blokování <xref:System.Func%601> delegáta oboru. Ukázková aplikace vytvoří pole s názvem `_allQuotesDeletedScope` (*interní/LoggerExtensions. cs*):

[!code-csharp[](loggermessage/samples/2.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet4)]

K vytvoření delegáta použijte <xref:Microsoft.Extensions.Logging.LoggerMessage.DefineScope*>. Až tři typy lze zadat pro použití jako argumenty šablony při volání delegáta. Ukázková aplikace používá šablonu zprávy, která obsahuje počet odstraněných uvozovek (`int` typ):

[!code-csharp[](loggermessage/samples/2.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet8)]

Zadejte statickou metodu rozšíření pro zprávu protokolu. Zahrňte všechny parametry typu pro pojmenované vlastnosti, které se zobrazí v šabloně zprávy. Ukázková aplikace přebírá `count` nabídky k odstranění a vrácení `_allQuotesDeletedScope`:

[!code-csharp[](loggermessage/samples/2.x/LoggerMessageSample/Internal/LoggerExtensions.cs?name=snippet12)]

Obor zabalí volání rozšíření protokolování v bloku [using](/dotnet/csharp/language-reference/keywords/using-statement) :

[!code-csharp[](loggermessage/samples/2.x/LoggerMessageSample/Pages/Index.cshtml.cs?name=snippet4&highlight=5-6,14)]

Zkontrolujte zprávy protokolu ve výstupu konzoly aplikace. Následující výsledek obsahuje tři nabídky odstraněné se zprávou rozsah protokolu, která je součástí:

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => 
          All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 1' Id = 2)
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => 
          All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 2' Id = 3)
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => 
          All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 3' Id = 4)
```

::: moniker-end

## <a name="additional-resources"></a>Další zdroje

* [Protokolování](xref:fundamentals/logging/index)
