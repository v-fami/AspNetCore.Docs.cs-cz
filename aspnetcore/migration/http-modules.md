---
title: Migrace obslužných rutin a modulů HTTP do ASP.NET Core middlewaru
author: rick-anderson
description: ''
ms.author: riande
ms.date: 12/07/2016
uid: migration/http-modules
ms.openlocfilehash: bdf27ccb742d4bc05bac71e6c96d71c38dcb4b62
ms.sourcegitcommit: 9a129f5f3e31cc449742b164d5004894bfca90aa
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78659682"
---
# <a name="migrate-http-handlers-and-modules-to-aspnet-core-middleware"></a>Migrace obslužných rutin a modulů HTTP do ASP.NET Core middlewaru

Tento článek ukazuje, jak migrovat existující [moduly a obslužné rutiny ASP.NET HTTP ze serveru System. webServer](/iis/configuration/system.webserver/) do ASP.NET Core [middlewaru](xref:fundamentals/middleware/index).

## <a name="modules-and-handlers-revisited"></a>Přenavštívené moduly a obslužné rutiny

Než začnete ASP.NET Core middlewaru, nejdřív si rekapitulace, jak fungují moduly HTTP a obslužné rutiny:

![Obslužná rutina modulů](http-modules/_static/moduleshandlers.png)

**Obslužné rutiny:**

* Třídy, které implementují [IHttpHandler](/dotnet/api/system.web.ihttphandler)

* Slouží ke zpracování požadavků s daným názvem nebo příponou souboru, například *. Report.*

* [Nakonfigurováno](/iis/configuration/system.webserver/handlers/) v *souboru Web. config*

**Moduly jsou:**

* Třídy, které implementují [IHttpModule](/dotnet/api/system.web.ihttpmodule)

* Vyvoláno pro každý požadavek

* Schopnost krátkodobého okruhu (zastavení dalšího zpracování žádosti)

* Může přidat do odpovědi HTTP nebo vytvořit vlastní.

* [Nakonfigurováno](/iis/configuration/system.webserver/modules/) v *souboru Web. config*

**Pořadí, ve kterém moduly zpracovávají příchozí požadavky, určuje:**

1. [Životní cyklus aplikace](https://msdn.microsoft.com/library/ms227673.aspx), což je události řady, které jsou aktivovány ASP.NET: [beginRequest](/dotnet/api/system.web.httpapplication.beginrequest), [AuthenticateRequest](/dotnet/api/system.web.httpapplication.authenticaterequest)atd. Každý modul může vytvořit obslužnou rutinu pro jednu nebo více událostí.

2. Pro stejnou událost, pořadí, ve kterém jsou konfigurovány v *souboru Web. config*.

Kromě modulů můžete přidat obslužné rutiny pro události životního cyklu do souboru *Global.asax.cs* . Tyto obslužné rutiny jsou spouštěny po obslužných rutinách v konfigurovaných modulech.

## <a name="from-handlers-and-modules-to-middleware"></a>Z obslužných rutin a modulů pro middleware

**Middleware jsou jednodušší než moduly HTTP a obslužné rutiny:**

* Moduly, obslužné rutiny, *Global.asax.cs*, *Web. config* (s výjimkou konfigurace služby IIS) a životní cyklus aplikace se odešlou.

* Služba middlewaru převzala role obou modulů i obslužných rutin.

* Middleware jsou nakonfigurovány pomocí kódu, nikoli v *souboru Web. config.*

* [Větvení kanálu](xref:fundamentals/middleware/index#use-run-and-map) vám umožňuje odesílat požadavky na konkrétní middleware na základě nejen adresy URL, ale také na hlavičkách žádostí, řetězcích dotazů atd.

**Middleware jsou velmi podobné modulům:**

* Vyvoláno v principu pro každý požadavek

* Může se stát, že žádost nebude v krátkém okruhu předávat [do dalšího middlewaru](#http-modules-shortcircuiting-middleware) .

* Schopné vytvořit vlastní odpověď HTTP

**Middleware a moduly jsou zpracovávány v jiném pořadí:**

* Pořadí middlewaru je založené na pořadí, ve kterém jsou vloženy do kanálu požadavků, zatímco pořadí modulů je založeno hlavně na událostech [životního cyklu aplikace](https://msdn.microsoft.com/library/ms227673.aspx) .

* Pořadí middlewaru pro odpovědi je opačné než u požadavků, zatímco pořadí modulů je u požadavků a odpovědí stejné.

* Viz [vytvoření kanálu middlewaru pomocí IApplicationBuilder](xref:fundamentals/middleware/index#create-a-middleware-pipeline-with-iapplicationbuilder)

![Middleware](http-modules/_static/middleware.png)

Všimněte si, jak je výše uvedený obrázek, ověřovací middleware krátce vyřídil požadavek.

## <a name="migrating-module-code-to-middleware"></a>Migrace kódu modulu do middlewaru

Existující modul HTTP bude vypadat nějak takto:

[!code-csharp[](../migration/http-modules/sample/Asp.Net4/Asp.Net4/Modules/MyModule.cs?highlight=6,8,24,31)]

Jak je znázorněno na stránce [middleware](xref:fundamentals/middleware/index) , ASP.NET Core middleware je třída, která zpřístupňuje `Invoke` metoda, která přebírá `HttpContext` a vrací `Task`. Váš nový middleware bude vypadat takto:

<a name="http-modules-usemiddleware"></a>

[!code-csharp[](../migration/http-modules/sample/Asp.Net.Core/Middleware/MyMiddleware.cs?highlight=9,13,20,24,28,30,32)]

Předchozí šablona middlewaru byla pořízena z oddílu o [zápisu middlewaru](xref:fundamentals/middleware/write).

Pomocná třída *MyMiddlewareExtensions* usnadňuje konfiguraci middlewaru ve vaší třídě `Startup`. Metoda `UseMyMiddleware` do kanálu požadavků přidá třídu middlewaru. Služby, které vyžaduje middleware, se vloží do konstruktoru middlewaru.

<a name="http-modules-shortcircuiting-middleware"></a>

Váš modul může ukončit žádost, například pokud uživatel není autorizovaný:

[!code-csharp[](../migration/http-modules/sample/Asp.Net4/Asp.Net4/Modules/MyTerminatingModule.cs?highlight=9,10,11,12,13&name=snippet_Terminate)]

Middleware to zpracovává tím, že nevolá `Invoke` u dalšího middlewaru v kanálu. Mějte na paměti, že to neukončí celý požadavek, protože předchozí middleware budou přesto vyvolány, když odpověď prochází způsobem kanálu.

[!code-csharp[](../migration/http-modules/sample/Asp.Net.Core/Middleware/MyTerminatingMiddleware.cs?highlight=7,8&name=snippet_Terminate)]

Když migrujete funkci modulu na nový middleware, může se stát, že váš kód nebude zkompilován, protože `HttpContext`á třída se v ASP.NET Core významně změnila. [Později](#migrating-to-the-new-httpcontext)se dozvíte, jak migrovat do nové ASP.NET Core HttpContext.

## <a name="migrating-module-insertion-into-the-request-pipeline"></a>Migruje se vložení modulu do kanálu požadavků.

Moduly HTTP se obvykle přidávají do kanálu požadavků pomocí *souboru Web. config*:

[!code-xml[](../migration/http-modules/sample/Asp.Net4/Asp.Net4/Web.config?highlight=6&range=1-3,32-33,36,43,50,101)]

Převeďte to [přidáním nového middlewaru](xref:fundamentals/middleware/index#create-a-middleware-pipeline-with-iapplicationbuilder) do kanálu požadavků ve vaší třídě `Startup`:

[!code-csharp[](../migration/http-modules/sample/Asp.Net.Core/Startup.cs?name=snippet_Configure&highlight=16)]

Přesné místo v kanálu, kam vložíte nový middleware, závisí na události, kterou zpracuje jako modul (`BeginRequest`, `EndRequest`atd.), a na pořadí v seznamu modulů v *souboru Web. config*.

Jak je uvedeno výše, v ASP.NET Core není žádný životní cyklus aplikace a pořadí, ve kterém jsou odpovědi zpracovávány middlewarem, se liší od pořadí používaného moduly. To může být náročnější na rozhodnutí o řazení.

Pokud se řazení stalo problémem, mohli byste svůj modul rozdělit do několika součástí middlewaru, které je možné seřadit nezávisle.

## <a name="migrating-handler-code-to-middleware"></a>Migrace kódu obslužné rutiny do middlewaru

Obslužná rutina HTTP vypadá nějak takto:

[!code-csharp[](../migration/http-modules/sample/Asp.Net4/Asp.Net4/HttpHandlers/ReportHandler.cs?highlight=5,7,13,14,15,16)]

V projektu ASP.NET Core byste ho přeložili na middleware podobnou této:

[!code-csharp[](../migration/http-modules/sample/Asp.Net.Core/Middleware/ReportHandlerMiddleware.cs?highlight=7,9,13,20,21,22,23,40,42,44)]

Tento middleware je velmi podobný middlewaru, který odpovídá modulům. Jediným skutečným rozdílem je, že zde není žádné volání `_next.Invoke(context)`. To dává smysl, protože obslužná rutina je na konci kanálu požadavků, takže nebudete moct vyvolat žádné další middleware.

## <a name="migrating-handler-insertion-into-the-request-pipeline"></a>Migrace vložení obslužné rutiny do kanálu žádosti

Konfigurace obslužné rutiny HTTP se provádí v *souboru Web. config* a vypadá nějak takto:

[!code-xml[](../migration/http-modules/sample/Asp.Net4/Asp.Net4/Web.config?highlight=6&range=1-3,32,46-48,50,101)]

To můžete převést přidáním nového middlewaru obslužné rutiny do kanálu požadavků ve vaší třídě `Startup`, podobně jako middleware převedené z modulů. Problém s tímto přístupem je, že by poslal všechny žádosti do nového middlewaru obslužné rutiny. Nicméně budete chtít, aby žádosti s daným rozšířením dosáhly vašeho middlewaru. To vám poskytne stejné funkce jako u vaší obslužné rutiny HTTP.

Jedním z řešení je vytvořit větev kanálu pro žádosti s danou příponou pomocí metody rozšíření `MapWhen`. Provedete to ve stejné `Configure` metodě, do které přidáte další middleware:

[!code-csharp[](../migration/http-modules/sample/Asp.Net.Core/Startup.cs?name=snippet_Configure&highlight=27-34)]

`MapWhen` přebírá tyto parametry:

1. Výraz lambda, který přebírá `HttpContext` a vrátí `true`, pokud by požadavek měl přijít do větve. To znamená, že můžete požadavky větví nejenom na základě jejich rozšíření, ale také v hlavičkách žádostí, parametrech řetězce dotazu atd.

2. Lambda, který přebírá `IApplicationBuilder` a přidává všechny middleware pro větev. To znamená, že můžete přidat další middleware do větve před middlewarem vaší obslužné rutiny.

Middleware přidaný do kanálu před tím, než se větev vyvolá u všech požadavků; Tato větev nebude mít žádný vliv.

## <a name="loading-middleware-options-using-the-options-pattern"></a>Načítání možností middlewaru pomocí vzoru možností

Některé moduly a obslužné rutiny mají možnosti konfigurace, které jsou uloženy v *souboru Web. config*. V ASP.NET Core se však používá nový model konfigurace místo souboru *Web. config*.

Nový [konfigurační systém](xref:fundamentals/configuration/index) poskytuje tyto možnosti, jak tento problém vyřešit:

* Přímo do middlewaru založit možnosti, jak je znázorněno v [Další části](#loading-middleware-options-through-direct-injection).

* Použijte [vzor možností](xref:fundamentals/configuration/options):

1. Vytvořte třídu pro uložení vašich možností middlewaru, například:

   [!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/MyMiddlewareWithParams.cs?name=snippet_Options)]

2. Uložení hodnot možností

   Konfigurační systém umožňuje ukládat hodnoty možností kdekoli, kde chcete. Většina lokalit ale používá *appSettings. JSON*, takže probereme tento přístup:

   [!code-json[](http-modules/sample/Asp.Net.Core/appsettings.json?range=1,14-18)]

   *MyMiddlewareOptionsSection* je tady název oddílu. Nemusí být stejný jako název vaší třídy možností.

3. Přidružit hodnoty možnosti k třídě Options

    Vzor možností používá ASP.NET Core rozhraní pro vkládání závislostí k přidružení typu možností (například `MyMiddlewareOptions`) k objektu `MyMiddlewareOptions`, který má skutečné možnosti.

    Aktualizujte třídu `Startup`:

   1. Pokud používáte *appSettings. JSON*, přidejte jej do Tvůrce konfigurace v konstruktoru `Startup`:

      [!code-csharp[](../migration/http-modules/sample/Asp.Net.Core/Startup.cs?name=snippet_Ctor&highlight=5-6)]

   2. Nakonfigurujte službu možností:

      [!code-csharp[](../migration/http-modules/sample/Asp.Net.Core/Startup.cs?name=snippet_ConfigureServices&highlight=4)]

   3. Přidružte možnosti k vaší třídě možností:

      [!code-csharp[](../migration/http-modules/sample/Asp.Net.Core/Startup.cs?name=snippet_ConfigureServices&highlight=6-8)]

4. Vloží možnosti do konstruktoru middlewaru. To je podobné jako vkládání možností do kontroleru.

   [!code-csharp[](../migration/http-modules/sample/Asp.Net.Core/Middleware/MyMiddlewareWithParams.cs?name=snippet_MiddlewareWithParams&highlight=4,7,10,15-16)]

   Metoda rozšíření [UseMiddleware](#http-modules-usemiddleware) , která do `IApplicationBuilder` přidává váš middleware, se stará o vkládání závislostí.

   To není omezeno na `IOptions` objekty. Jakýkoli jiný objekt, který váš middleware vyžaduje, může být tímto způsobem vložen.

## <a name="loading-middleware-options-through-direct-injection"></a>Načítání možností middlewaru prostřednictvím přímého vkládání

Vzor možností má výhodu, že vytvoří volné propojení mezi hodnotami možností a jejich příjemci. Po přidružení třídy možností se skutečnými hodnotami možností může jakákoliv jiná třída získat přístup k možnostem prostřednictvím rozhraní injektáže pro vkládání závislostí. Nemusíte předávat hodnoty možností.

Tato možnost se ukončí, pokud chcete stejný middleware používat dvakrát a s různými možnostmi. Například autorizační middleware používaný v různých větvích umožňuje různé role. Nelze přidružit dva různé objekty možností s jednou třídou možností.

Řešením je získat objekty možností se skutečnými hodnotami možností ve vaší třídě `Startup` a předat je přímo do každé instance vašeho middlewaru.

1. Přidat druhý klíč do souboru *appSettings. JSON*

   Chcete-li přidat druhou sadu možností do souboru *appSettings. JSON* , použijte k jedinečné identifikaci nový klíč:

   [!code-json[](http-modules/sample/Asp.Net.Core/appsettings.json?range=1,10-18&highlight=2-5)]

2. Načtěte hodnoty možností a předejte je middlewaru. Metoda rozšíření `Use...` (která přidává váš middleware do kanálu) je logické místo, které se má předat v hodnotách možností: 

   [!code-csharp[](http-modules/sample/Asp.Net.Core/Startup.cs?name=snippet_Configure&highlight=20-23)]

3. Povolte middlewari, aby převzala parametr options. Poskytněte přetížení metody rozšíření `Use...` (která přebírá parametr options a předá ho `UseMiddleware`). Když je volána `UseMiddleware` s parametry, předá parametry konstruktoru middleware při vytváření instance objektu middleware.

   [!code-csharp[](../migration/http-modules/sample/Asp.Net.Core/Middleware/MyMiddlewareWithParams.cs?name=snippet_Extensions&highlight=9-14)]

   Všimněte si, jak toto zabalí objekt Options v objektu `OptionsWrapper`. To implementuje `IOptions`, jak je očekáván konstruktor middleware.

## <a name="migrating-to-the-new-httpcontext"></a>Migrace na novou HttpContext

Dříve jste viděli, že metoda `Invoke` ve vašem middlewaru převezme parametr typu `HttpContext`:

```csharp
public async Task Invoke(HttpContext context)
```

`HttpContext` se v ASP.NET Core podstatně změnily. V této části se dozvíte, jak přeložit nejčastěji používané vlastnosti [System. Web. HttpContext](/dotnet/api/system.web.httpcontext) na nový `Microsoft.AspNetCore.Http.HttpContext`.

### <a name="httpcontext"></a>HttpContext

**HttpContext. Items** se přeloží:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Items)]

**Jedinečné ID žádosti (žádný System. Web. HttpContext protějšek)**

Poskytuje jedinečné ID pro každý požadavek. Je velmi užitečné zahrnout do protokolů.

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Trace)]

### <a name="httpcontextrequest"></a>HttpContext. Request

**HttpContext. Request. HttpMethod** se překládá na:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Method)]

**HttpContext. Request. QueryString** se překládá na:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Query)]

**HttpContext. Request. URL** a **HttpContext. Request. RawUrl** přeložit na:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Url)]

**HttpContext. Request. IsSecureConnection** se překládá na:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Secure)]

**HttpContext. Request. UserHostAddress** se překládá na:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Host)]

**HttpContext. Request. cookies** se převede na:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Cookies)]

**HttpContext. Request. Třída requestContext. parametr RouteData** se překládá na:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Route)]

**HttpContext. Request. Headers** transformuje:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Headers)]

**HttpContext. Request. UserAgent** se převádí na:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Agent)]

**HttpContext. Request. UrlReferrer** se překládá na:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Referrer)]

**HttpContext. Request. ContentType** se překládá na:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Type)]

**HttpContext. Request. Form** se překládá na:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Form)]

> [!WARNING]
> Přečte hodnoty formuláře pouze v případě, že je podřízený typ obsahu *x-www-form-urlencoded* nebo *form-data*.

**HttpContext. Request. InputStream** se překládá na:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Input)]

> [!WARNING]
> Tento kód používejte pouze v middlewari typu pro zpracování, na konci kanálu.
>
>Nezpracovaný text si můžete přečíst, jak je znázorněno výše na vyžádání. Middleware, který se pokouší přečíst tělo po prvním čtení, načte prázdné tělo.
>
>To se nevztahuje na čtení formuláře uvedeného výše, protože to je hotové z vyrovnávací paměti.

### <a name="httpcontextresponse"></a>HttpContext.Response

**HttpContext. Response. status** a **HttpContext. Response. StatusDescription** přeložit na:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Status)]

**Vlastnost HttpContext. Response. ContentEncoding** a **HttpContext. Response. ContentType** se převede na:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_RespType)]

**HttpContext. Response. ContentType** sám o sobě také přeloží:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_RespTypeOnly)]

**HttpContext. Response. Output** se překládá na:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_Output)]

**HttpContext. Response. zpracování funkce TransmitFile**

Soubor [se zabývá](../fundamentals/request-features.md#middleware-and-request-features)popsáním souboru.

**HttpContext. Response. Headers**

Posílání hlaviček odpovědí je složité, protože pokud jste je nastavili po zapsání nějakého textu odpovědi, nebudou odeslány.

Řešením je nastavit metodu zpětného volání, která bude volána přímo před zápisem do odpovědi. To se nejlépe provádí na začátku `Invoke` metody ve vašem middlewaru. Je to metoda zpětného volání, která nastavuje hlavičky odpovědi.

Následující kód nastaví metodu zpětného volání s názvem `SetHeaders`:

```csharp
public async Task Invoke(HttpContext httpContext)
{
    // ...
    httpContext.Response.OnStarting(SetHeaders, state: httpContext);
```

Metoda zpětného volání `SetHeaders` by vypadala takto:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_SetHeaders)]

**HttpContext. Response. cookies**

Soubory cookie se cestují do prohlížeče v hlavičce odpovědi *souborového souboru cookie* . V důsledku toho odeslání souborů cookie vyžaduje stejné zpětné volání, které se používá k odesílání hlaviček odpovědí:

```csharp
public async Task Invoke(HttpContext httpContext)
{
    // ...
    httpContext.Response.OnStarting(SetCookies, state: httpContext);
    httpContext.Response.OnStarting(SetHeaders, state: httpContext);
```

Metoda zpětného volání `SetCookies` by vypadala takto:

[!code-csharp[](http-modules/sample/Asp.Net.Core/Middleware/HttpContextDemoMiddleware.cs?name=snippet_SetCookies)]

## <a name="additional-resources"></a>Další zdroje

* [Obslužné rutiny HTTP a moduly HTTP – přehled](/iis/configuration/system.webserver/)
* [Konfigurace](xref:fundamentals/configuration/index)
* [Spuštění aplikace](xref:fundamentals/startup)
* [Middleware](xref:fundamentals/middleware/index)
