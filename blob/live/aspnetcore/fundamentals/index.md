---
title: "Základy ASP.NET Core"
author: rick-anderson
description: "Zjistit základní koncepty pro vytváření aplikací ASP.NET Core."
ms.author: riande
manager: wpickett
ms.date: 09/30/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/index
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d977c13eb5f4cbe8bac261733bdc747e6c19b2a
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/19/2018
---
# <a name="aspnet-core-fundamentals"></a><span data-ttu-id="e1409-103">Základy ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e1409-103">ASP.NET Core fundamentals</span></span>

<span data-ttu-id="e1409-104">Aplikace ASP.NET Core je konzolovou aplikaci, která vytvoří webovým serverem v jeho `Main` metoda:</span><span class="sxs-lookup"><span data-stu-id="e1409-104">An ASP.NET Core application is a console app that creates a web server in its `Main` method:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="e1409-105">ASP.NET základní 2.x</span><span class="sxs-lookup"><span data-stu-id="e1409-105">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](../getting-started/sample/aspnetcoreapp/Program2x.cs)]

<span data-ttu-id="e1409-106">`Main` Vyvolá metoda `WebHost.CreateDefaultBuilder`, který odpovídá vzorci Tvůrce vytvořit hostitel webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="e1409-106">The `Main` method invokes `WebHost.CreateDefaultBuilder`, which follows the builder pattern to create a web application host.</span></span> <span data-ttu-id="e1409-107">Tvůrce obsahuje metody, které definují webového serveru (například `UseKestrel`) a třída při spuštění (`UseStartup`).</span><span class="sxs-lookup"><span data-stu-id="e1409-107">The builder has methods that define the web server (for example, `UseKestrel`) and the startup class (`UseStartup`).</span></span> <span data-ttu-id="e1409-108">V předchozím příkladu [Kestrel](xref:fundamentals/servers/kestrel) webový server je automaticky přidělen.</span><span class="sxs-lookup"><span data-stu-id="e1409-108">In the preceding example, the [Kestrel](xref:fundamentals/servers/kestrel) web server is automatically allocated.</span></span> <span data-ttu-id="e1409-109">ASP.NET Core webového hostitele se pokusí o spuštění ve službě IIS, pokud je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="e1409-109">ASP.NET Core's web host attempts to run on IIS, if available.</span></span> <span data-ttu-id="e1409-110">Další webové servery, jako například [HTTP.sys](xref:fundamentals/servers/httpsys), mohou být využívána volání metody odpovídající rozšíření.</span><span class="sxs-lookup"><span data-stu-id="e1409-110">Other web servers, such as [HTTP.sys](xref:fundamentals/servers/httpsys), can be used by invoking the appropriate extension method.</span></span> <span data-ttu-id="e1409-111">`UseStartup`je vysvětleno v následující části Další.</span><span class="sxs-lookup"><span data-stu-id="e1409-111">`UseStartup` is explained further in the next section.</span></span>

<span data-ttu-id="e1409-112">`IWebHostBuilder`, návratový typ `WebHost.CreateDefaultBuilder` volání, nabízí mnoho způsobů volitelné.</span><span class="sxs-lookup"><span data-stu-id="e1409-112">`IWebHostBuilder`, the return type of the `WebHost.CreateDefaultBuilder` invocation, provides many optional methods.</span></span> <span data-ttu-id="e1409-113">Některé z těchto metod zahrnují `UseHttpSys` pro hostování aplikace v HTTP.sys a `UseContentRoot` pro zadání kořenový adresář s obsahem.</span><span class="sxs-lookup"><span data-stu-id="e1409-113">Some of these methods include `UseHttpSys` for hosting the app in HTTP.sys and `UseContentRoot` for specifying the root content directory.</span></span> <span data-ttu-id="e1409-114">`Build` a `Run` metody sestavení `IWebHost` objekt, který je hostitelem aplikace a začne naslouchat požadavkům HTTP.</span><span class="sxs-lookup"><span data-stu-id="e1409-114">The `Build` and `Run` methods build the `IWebHost` object that hosts the app and begins listening for HTTP requests.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="e1409-115">ASP.NET základní 1.x</span><span class="sxs-lookup"><span data-stu-id="e1409-115">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](../getting-started/sample/aspnetcoreapp/Program.cs)]

<span data-ttu-id="e1409-116">`Main` Používá metoda `WebHostBuilder`, který odpovídá vzorci Tvůrce vytvořit hostitel webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="e1409-116">The `Main` method uses `WebHostBuilder`, which follows the builder pattern to create a web application host.</span></span> <span data-ttu-id="e1409-117">Tvůrce obsahuje metody, které definují webového serveru (například `UseKestrel`) a třída při spuštění (`UseStartup`).</span><span class="sxs-lookup"><span data-stu-id="e1409-117">The builder has methods that define the web server (for example, `UseKestrel`) and the startup class (`UseStartup`).</span></span> <span data-ttu-id="e1409-118">V předchozím příkladu [Kestrel](xref:fundamentals/servers/kestrel) se používá webový server.</span><span class="sxs-lookup"><span data-stu-id="e1409-118">In the preceding example, the [Kestrel](xref:fundamentals/servers/kestrel) web server is used.</span></span> <span data-ttu-id="e1409-119">Další webové servery, jako například [WebListener](xref:fundamentals/servers/weblistener), mohou být využívána volání metody odpovídající rozšíření.</span><span class="sxs-lookup"><span data-stu-id="e1409-119">Other web servers, such as [WebListener](xref:fundamentals/servers/weblistener), can be used by invoking the appropriate extension method.</span></span> <span data-ttu-id="e1409-120">`UseStartup`je vysvětleno v následující části Další.</span><span class="sxs-lookup"><span data-stu-id="e1409-120">`UseStartup` is explained further in the next section.</span></span>

<span data-ttu-id="e1409-121">`WebHostBuilder`nabízí mnoho volitelné způsobů, včetně `UseIISIntegration` pro hostování v IIS a služby IIS Express a `UseContentRoot` pro zadání kořenový adresář s obsahem.</span><span class="sxs-lookup"><span data-stu-id="e1409-121">`WebHostBuilder` provides many optional methods, including `UseIISIntegration` for hosting in IIS and IIS Express and `UseContentRoot` for specifying the root content directory.</span></span> <span data-ttu-id="e1409-122">`Build` a `Run` metody sestavení `IWebHost` objekt, který je hostitelem aplikace a začne naslouchat požadavkům HTTP.</span><span class="sxs-lookup"><span data-stu-id="e1409-122">The `Build` and `Run` methods build the `IWebHost` object that hosts the app and begins listening for HTTP requests.</span></span>

---

## <a name="startup"></a><span data-ttu-id="e1409-123">Spuštění</span><span class="sxs-lookup"><span data-stu-id="e1409-123">Startup</span></span>

<span data-ttu-id="e1409-124">`UseStartup` Metodu `WebHostBuilder` Určuje `Startup` třídy pro aplikaci:</span><span class="sxs-lookup"><span data-stu-id="e1409-124">The `UseStartup` method on `WebHostBuilder` specifies the `Startup` class for your app:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="e1409-125">ASP.NET základní 2.x</span><span class="sxs-lookup"><span data-stu-id="e1409-125">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](../getting-started/sample/aspnetcoreapp/Program2x.cs?highlight=10&range=6-17)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="e1409-126">ASP.NET základní 1.x</span><span class="sxs-lookup"><span data-stu-id="e1409-126">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](../getting-started/sample/aspnetcoreapp/Program.cs?highlight=7&range=6-17)]

---

<span data-ttu-id="e1409-127">`Startup` Je třída, kde můžete definovat v kanálu zpracování požadavků a které jsou nakonfigurované všechny služby potřebné pro aplikaci.</span><span class="sxs-lookup"><span data-stu-id="e1409-127">The `Startup` class is where you define the request handling pipeline and where any services needed by the app are configured.</span></span> <span data-ttu-id="e1409-128">`Startup` Třída musí být veřejné a musí obsahovat následující metody:</span><span class="sxs-lookup"><span data-stu-id="e1409-128">The `Startup` class must be public and contain the following methods:</span></span>

```csharp
public class Startup
{
    // This method gets called by the runtime. Use this method
    // to add services to the container.
    public void ConfigureServices(IServiceCollection services)
    {
    }

    // This method gets called by the runtime. Use this method
    // to configure the HTTP request pipeline.
    public void Configure(IApplicationBuilder app)
    {
    }
}
```

<span data-ttu-id="e1409-129">`ConfigureServices`definuje [služby](#dependency-injection-services) používané vaší aplikace (například Identity Entity Framework Core, základní rozhraní ASP.NET MVC).</span><span class="sxs-lookup"><span data-stu-id="e1409-129">`ConfigureServices` defines the [Services](#dependency-injection-services) used by your app (for example, ASP.NET Core MVC, Entity Framework Core, Identity).</span></span> <span data-ttu-id="e1409-130">`Configure`definuje [middleware](xref:fundamentals/middleware) pro kanál požadavku.</span><span class="sxs-lookup"><span data-stu-id="e1409-130">`Configure` defines the [middleware](xref:fundamentals/middleware) for the request pipeline.</span></span>

<span data-ttu-id="e1409-131">Další informace najdete v tématu [spuštění aplikace](xref:fundamentals/startup).</span><span class="sxs-lookup"><span data-stu-id="e1409-131">For more information, see [Application startup](xref:fundamentals/startup).</span></span>

## <a name="content-root"></a><span data-ttu-id="e1409-132">Obsah kořenové</span><span class="sxs-lookup"><span data-stu-id="e1409-132">Content root</span></span>

<span data-ttu-id="e1409-133">Kořenu obsahu je základní cesta k žádný obsah používané aplikace, jako je například zobrazení, [stránky Razor](xref:mvc/razor-pages/index)a statické prostředky.</span><span class="sxs-lookup"><span data-stu-id="e1409-133">The content root is the base path to any content used by the app, such as views, [Razor Pages](xref:mvc/razor-pages/index), and static assets.</span></span> <span data-ttu-id="e1409-134">Ve výchozím nastavení kořenu obsahu je stejný jako základní cesta aplikace pro spustitelný soubor, který je hostitelem aplikace.</span><span class="sxs-lookup"><span data-stu-id="e1409-134">By default, the content root is the same as application base path for the executable hosting the app.</span></span>

## <a name="web-root"></a><span data-ttu-id="e1409-135">Kořenový web</span><span class="sxs-lookup"><span data-stu-id="e1409-135">Web root</span></span>

<span data-ttu-id="e1409-136">Kořenové webové aplikace je adresář v projektu obsahující veřejný, statické prostředky, například šablon stylů CSS, JavaScript a soubory obrázků.</span><span class="sxs-lookup"><span data-stu-id="e1409-136">The web root of an app is the directory in the project containing public, static resources, such as CSS, JavaScript, and image files.</span></span>

## <a name="dependency-injection-services"></a><span data-ttu-id="e1409-137">Vkládání závislostí (služby)</span><span class="sxs-lookup"><span data-stu-id="e1409-137">Dependency Injection (Services)</span></span>

<span data-ttu-id="e1409-138">Služba je komponenta, která je určená pro běžné používání v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="e1409-138">A service is a component that's intended for common consumption in an app.</span></span> <span data-ttu-id="e1409-139">Služby jsou dostupné prostřednictvím [vkládání závislostí (DI)](xref:fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="e1409-139">Services are made available through [dependency injection (DI)](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="e1409-140">ASP.NET Core zahrnuje nativní **I**nPro **o**f **C**kontejneru obrazit řídicí (IoC), který podporuje [konstruktor vkládání](xref:mvc/controllers/dependency-injection#constructor-injection) ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="e1409-140">ASP.NET Core includes a native **I**nversion **o**f **C**ontrol (IoC) container that supports [constructor injection](xref:mvc/controllers/dependency-injection#constructor-injection) by default.</span></span> <span data-ttu-id="e1409-141">Výchozí kontejner nativní můžete nahradit, pokud chcete.</span><span class="sxs-lookup"><span data-stu-id="e1409-141">You can replace the default native container if you wish.</span></span> <span data-ttu-id="e1409-142">Kromě jeho výhody volné párování DI umožňuje služby k dispozici v celé vaší aplikace (například [protokolování](xref:fundamentals/logging/index)).</span><span class="sxs-lookup"><span data-stu-id="e1409-142">In addition to its loose coupling benefit, DI makes services available throughout your app (for example, [logging](xref:fundamentals/logging/index)).</span></span>

<span data-ttu-id="e1409-143">Další informace najdete v tématu [vkládání závislostí](xref:fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="e1409-143">For more information, see [Dependency injection](xref:fundamentals/dependency-injection).</span></span>

## <a name="middleware"></a><span data-ttu-id="e1409-144">Middleware</span><span class="sxs-lookup"><span data-stu-id="e1409-144">Middleware</span></span>

<span data-ttu-id="e1409-145">V ASP.NET Core, vytvoříte pomocí kanálu požadavku [middleware](xref:fundamentals/middleware).</span><span class="sxs-lookup"><span data-stu-id="e1409-145">In ASP.NET Core, you compose your request pipeline using [middleware](xref:fundamentals/middleware).</span></span> <span data-ttu-id="e1409-146">ASP.NET Core middleware provede asynchronní logiku `HttpContext` a vyvolá další middleware v pořadí, nebo přímo ukončí žádosti.</span><span class="sxs-lookup"><span data-stu-id="e1409-146">ASP.NET Core middleware performs asynchronous logic on an `HttpContext` and then either invokes the next middleware in the sequence or terminates the request directly.</span></span> <span data-ttu-id="e1409-147">Přidá middleware komponenty s názvem "XYZ" se při vyvolání `UseXYZ` metoda rozšíření v `Configure` metoda.</span><span class="sxs-lookup"><span data-stu-id="e1409-147">A middleware component called "XYZ" is added by invoking an `UseXYZ` extension method in the `Configure` method.</span></span>

<span data-ttu-id="e1409-148">ASP.NET Core se dodává s bohatou sadu předdefinovaných middleware:</span><span class="sxs-lookup"><span data-stu-id="e1409-148">ASP.NET Core comes with a rich set of built-in middleware:</span></span>

* [<span data-ttu-id="e1409-149">Statické soubory</span><span class="sxs-lookup"><span data-stu-id="e1409-149">Static files</span></span>](xref:fundamentals/static-files)
* [<span data-ttu-id="e1409-150">Směrování</span><span class="sxs-lookup"><span data-stu-id="e1409-150">Routing</span></span>](xref:fundamentals/routing)
* [<span data-ttu-id="e1409-151">Ověřování</span><span class="sxs-lookup"><span data-stu-id="e1409-151">Authentication</span></span>](xref:security/authentication/index)
* [<span data-ttu-id="e1409-152">Middleware pro kompresi odpovědí</span><span class="sxs-lookup"><span data-stu-id="e1409-152">Response Compression Middleware</span></span>](xref:performance/response-compression)
* [<span data-ttu-id="e1409-153">Middleware pro přepis adres URL</span><span class="sxs-lookup"><span data-stu-id="e1409-153">URL Rewriting Middleware</span></span>](xref:fundamentals/url-rewriting)

<span data-ttu-id="e1409-154">[OWIN](http://owin.org)– na základě middlewaru je k dispozici pro aplikace ASP.NET Core a můžete napsat vlastní vlastní middleware.</span><span class="sxs-lookup"><span data-stu-id="e1409-154">[OWIN](http://owin.org)-based middleware is available for ASP.NET Core apps, and you can write your own custom middleware.</span></span>

<span data-ttu-id="e1409-155">Další informace najdete v tématu [Middleware](xref:fundamentals/middleware) a [Open Web Interface pro .NET (OWIN)](xref:fundamentals/owin).</span><span class="sxs-lookup"><span data-stu-id="e1409-155">For more information, see [Middleware](xref:fundamentals/middleware) and [Open Web Interface for .NET (OWIN)](xref:fundamentals/owin).</span></span>

## <a name="environments"></a><span data-ttu-id="e1409-156">Prostředí</span><span class="sxs-lookup"><span data-stu-id="e1409-156">Environments</span></span>

<span data-ttu-id="e1409-157">Prostředí, jako je například "Vývoj" a "Provozní", jsou hodnoty první třídy v ASP.NET Core a se dá nastavit pomocí proměnné prostředí.</span><span class="sxs-lookup"><span data-stu-id="e1409-157">Environments, such as "Development" and "Production", are a first-class notion in ASP.NET Core and can be set using environment variables.</span></span>

<span data-ttu-id="e1409-158">Další informace najdete v tématu [práce s několika prostředí](xref:fundamentals/environments).</span><span class="sxs-lookup"><span data-stu-id="e1409-158">For more information, see [Working with Multiple Environments](xref:fundamentals/environments).</span></span>

## <a name="configuration"></a><span data-ttu-id="e1409-159">Konfigurace</span><span class="sxs-lookup"><span data-stu-id="e1409-159">Configuration</span></span>

<span data-ttu-id="e1409-160">Jádro ASP.NET používá model konfigurace na základě párů název hodnota.</span><span class="sxs-lookup"><span data-stu-id="e1409-160">ASP.NET Core uses a configuration model based on name-value pairs.</span></span> <span data-ttu-id="e1409-161">Konfigurační model není založen na `System.Configuration` nebo *web.config*. Konfigurace obsahuje nastavení ze seřazené sadu poskytovatelů konfigurace.</span><span class="sxs-lookup"><span data-stu-id="e1409-161">The configuration model isn't based on `System.Configuration` or *web.config*. Configuration obtains settings from an ordered set of configuration providers.</span></span> <span data-ttu-id="e1409-162">Poskytovatelé předdefinované konfigurace podporují celou řadu formáty souborů (XML, JSON, INI) a proměnné prostředí umožňující konfiguraci na základě prostředí.</span><span class="sxs-lookup"><span data-stu-id="e1409-162">The built-in configuration providers support a variety of file formats (XML, JSON, INI) and environment variables to enable environment-based configuration.</span></span> <span data-ttu-id="e1409-163">Také můžete napsat vlastního zprostředkovatele vlastní konfigurace.</span><span class="sxs-lookup"><span data-stu-id="e1409-163">You can also write your own custom configuration providers.</span></span>

<span data-ttu-id="e1409-164">Další informace najdete v tématu [konfigurace](xref:fundamentals/configuration/index).</span><span class="sxs-lookup"><span data-stu-id="e1409-164">For more information, see [Configuration](xref:fundamentals/configuration/index).</span></span>

## <a name="logging"></a><span data-ttu-id="e1409-165">protokolování</span><span class="sxs-lookup"><span data-stu-id="e1409-165">Logging</span></span>

<span data-ttu-id="e1409-166">Jádro ASP.NET podporuje protokolování rozhraní API, která funguje s různými zprostředkovatelů protokolování.</span><span class="sxs-lookup"><span data-stu-id="e1409-166">ASP.NET Core supports a logging API that works with a variety of logging providers.</span></span> <span data-ttu-id="e1409-167">Předdefinované zprostředkovatele podporovat odesílání protokoly na jeden nebo více míst.</span><span class="sxs-lookup"><span data-stu-id="e1409-167">Built-in providers support sending logs to one or more destinations.</span></span> <span data-ttu-id="e1409-168">Můžete použít rozhraní protokolování třetích stran.</span><span class="sxs-lookup"><span data-stu-id="e1409-168">Third-party logging frameworks can be used.</span></span>

[<span data-ttu-id="e1409-169">Protokolování</span><span class="sxs-lookup"><span data-stu-id="e1409-169">Logging</span></span>](xref:fundamentals/logging/index)

## <a name="error-handling"></a><span data-ttu-id="e1409-170">Zpracování chyb</span><span class="sxs-lookup"><span data-stu-id="e1409-170">Error handling</span></span>

<span data-ttu-id="e1409-171">ASP.NET Core obsahuje integrované funkce pro zpracování chyb v aplikacích, včetně stránky výjimka developer, vlastní chybové stránky, statické stav znakové stránky a spuštění zpracování výjimek.</span><span class="sxs-lookup"><span data-stu-id="e1409-171">ASP.NET Core has built-in features for handling errors in apps, including a developer exception page, custom error pages, static status code pages, and startup exception handling.</span></span>

<span data-ttu-id="e1409-172">Další informace najdete v tématu [zpracování chyb](xref:fundamentals/error-handling).</span><span class="sxs-lookup"><span data-stu-id="e1409-172">For more information, see [Error Handling](xref:fundamentals/error-handling).</span></span>

## <a name="routing"></a><span data-ttu-id="e1409-173">Směrování</span><span class="sxs-lookup"><span data-stu-id="e1409-173">Routing</span></span>

<span data-ttu-id="e1409-174">ASP.NET Core nabízí funkce pro směrování požadavků app na obslužné rutiny trasy.</span><span class="sxs-lookup"><span data-stu-id="e1409-174">ASP.NET Core offers features for routing of app requests to route handlers.</span></span>

<span data-ttu-id="e1409-175">Další informace najdete v tématu [směrování](xref:fundamentals/routing).</span><span class="sxs-lookup"><span data-stu-id="e1409-175">For more information, see [Routing](xref:fundamentals/routing).</span></span>

## <a name="file-providers"></a><span data-ttu-id="e1409-176">Zprostředkovatelé souboru</span><span class="sxs-lookup"><span data-stu-id="e1409-176">File providers</span></span>

<span data-ttu-id="e1409-177">ASP.NET Core abstrahuje přístupu k systému souborů prostřednictvím poskytovatelů souboru, který nabízí společné rozhraní pro práci se soubory napříč platformami.</span><span class="sxs-lookup"><span data-stu-id="e1409-177">ASP.NET Core abstracts file system access through the use of File Providers, which offers a common interface for working with files across platforms.</span></span>

<span data-ttu-id="e1409-178">Další informace najdete v tématu [souboru zprostředkovatelé](xref:fundamentals/file-providers).</span><span class="sxs-lookup"><span data-stu-id="e1409-178">For more information, see [File Providers](xref:fundamentals/file-providers).</span></span>

## <a name="static-files"></a><span data-ttu-id="e1409-179">Statické soubory</span><span class="sxs-lookup"><span data-stu-id="e1409-179">Static files</span></span>

<span data-ttu-id="e1409-180">Statické soubory middleware poskytuje statické soubory, jako je například HTML, CSS, image a JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e1409-180">Static files middleware serves static files, such as HTML, CSS, image, and JavaScript.</span></span>

<span data-ttu-id="e1409-181">Další informace najdete v tématu [práce s statické soubory](xref:fundamentals/static-files).</span><span class="sxs-lookup"><span data-stu-id="e1409-181">For more information, see [Working with static files](xref:fundamentals/static-files).</span></span>

## <a name="hosting"></a><span data-ttu-id="e1409-182">Hostování</span><span class="sxs-lookup"><span data-stu-id="e1409-182">Hosting</span></span>

<span data-ttu-id="e1409-183">Aplikace ASP.NET Core nakonfigurovat a spustit *hostitele*, která je zodpovědná za spuštění a životního cyklu správy aplikací.</span><span class="sxs-lookup"><span data-stu-id="e1409-183">ASP.NET Core apps configure and launch a *host*, which is responsible for app startup and lifetime management.</span></span>

<span data-ttu-id="e1409-184">Další informace najdete v tématu [hostitelský](xref:fundamentals/hosting).</span><span class="sxs-lookup"><span data-stu-id="e1409-184">For more information, see [Hosting](xref:fundamentals/hosting).</span></span>

## <a name="session-and-application-state"></a><span data-ttu-id="e1409-185">Stav relace a aplikace</span><span class="sxs-lookup"><span data-stu-id="e1409-185">Session and application state</span></span>

<span data-ttu-id="e1409-186">Stav relace je funkce v ASP.NET Core, který můžete použít k ukládání a uchovávání dat uživatele, když uživatel prohlíží vaší webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="e1409-186">Session state is a feature in ASP.NET Core that you can use to save and store user data while the user browses your web app.</span></span>

<span data-ttu-id="e1409-187">Další informace najdete v tématu [relace a stav aplikace](xref:fundamentals/app-state).</span><span class="sxs-lookup"><span data-stu-id="e1409-187">For more information, see [Session and application state](xref:fundamentals/app-state).</span></span>

## <a name="servers"></a><span data-ttu-id="e1409-188">Servery</span><span class="sxs-lookup"><span data-stu-id="e1409-188">Servers</span></span>

<span data-ttu-id="e1409-189">Model hostování základní technologie ASP.NET není přímo naslouchat požadavkům.</span><span class="sxs-lookup"><span data-stu-id="e1409-189">The ASP.NET Core hosting model doesn't directly listen for requests.</span></span> <span data-ttu-id="e1409-190">Model hostování závisí na implementaci serveru HTTP k předání požadavku do aplikace.</span><span class="sxs-lookup"><span data-stu-id="e1409-190">The hosting model relies on an HTTP server implementation to forward the request to the app.</span></span> <span data-ttu-id="e1409-191">Předaný požadavek je zabalená jako sada objektů funkce, které je přístupné prostřednictvím rozhraní.</span><span class="sxs-lookup"><span data-stu-id="e1409-191">The forwarded request is wrapped as a set of feature objects that can be accessed through interfaces.</span></span> <span data-ttu-id="e1409-192">ASP.NET Core zahrnuje spravovaná, a platformy webového serveru, nazývá [Kestrel](xref:fundamentals/servers/kestrel).</span><span class="sxs-lookup"><span data-stu-id="e1409-192">ASP.NET Core includes a managed, cross-platform web server, called [Kestrel](xref:fundamentals/servers/kestrel).</span></span> <span data-ttu-id="e1409-193">Kestrel je často spouštět za produkční webového serveru, jako například [IIS](https://www.iis.net/) nebo [Nginx](http://nginx.org).</span><span class="sxs-lookup"><span data-stu-id="e1409-193">Kestrel is often run behind a production web server, such as [IIS](https://www.iis.net/) or [Nginx](http://nginx.org).</span></span> <span data-ttu-id="e1409-194">Kestrel můžete spouštět jako hraniční server.</span><span class="sxs-lookup"><span data-stu-id="e1409-194">Kestrel can be run as an edge server.</span></span>

<span data-ttu-id="e1409-195">Další informace najdete v tématu [servery](xref:fundamentals/servers/index) a v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="e1409-195">For more information, see [Servers](xref:fundamentals/servers/index) and the following topics:</span></span>

* [<span data-ttu-id="e1409-196">Kestrel</span><span class="sxs-lookup"><span data-stu-id="e1409-196">Kestrel</span></span>](xref:fundamentals/servers/kestrel)
* [<span data-ttu-id="e1409-197">Modul ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e1409-197">ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* <span data-ttu-id="e1409-198">[Ovladač HTTP.sys](xref:fundamentals/servers/httpsys) (dříve se označovaly jako [WebListener](xref:fundamentals/servers/weblistener))</span><span class="sxs-lookup"><span data-stu-id="e1409-198">[HTTP.sys](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener))</span></span>

## <a name="globalization-and-localization"></a><span data-ttu-id="e1409-199">Globalizace a lokalizace</span><span class="sxs-lookup"><span data-stu-id="e1409-199">Globalization and localization</span></span>

<span data-ttu-id="e1409-200">Vytvoření vícejazyčné webu pomocí ASP.NET Core umožňuje vaší lokality k dosažení širší cílovou skupinu.</span><span class="sxs-lookup"><span data-stu-id="e1409-200">Creating a multilingual website with ASP.NET Core allows your site to reach a wider audience.</span></span> <span data-ttu-id="e1409-201">Základní technologie ASP.NET poskytuje služby a middleware pro lokalizace do různých jazyků a kultur.</span><span class="sxs-lookup"><span data-stu-id="e1409-201">ASP.NET Core provides services and middleware for localizing into different languages and cultures.</span></span>

<span data-ttu-id="e1409-202">Další informace najdete v tématu [globalizace a lokalizace](xref:fundamentals/localization).</span><span class="sxs-lookup"><span data-stu-id="e1409-202">For more information, see [Globalization and localization](xref:fundamentals/localization).</span></span>

## <a name="request-features"></a><span data-ttu-id="e1409-203">Požadavky na funkce</span><span class="sxs-lookup"><span data-stu-id="e1409-203">Request features</span></span>

<span data-ttu-id="e1409-204">Související podrobnosti implementace webového serveru na požadavky HTTP a odpovědí jsou definovány v rozhraní.</span><span class="sxs-lookup"><span data-stu-id="e1409-204">Web server implementation details related to HTTP requests and responses are defined in interfaces.</span></span> <span data-ttu-id="e1409-205">Tato rozhraní jsou používány implementací serveru a middleware, vytvářet a upravovat hostování kanálu aplikace.</span><span class="sxs-lookup"><span data-stu-id="e1409-205">These interfaces are used by server implementations and middleware to create and modify the app's hosting pipeline.</span></span>

<span data-ttu-id="e1409-206">Další informace najdete v tématu [žádosti o funkce](xref:fundamentals/request-features).</span><span class="sxs-lookup"><span data-stu-id="e1409-206">For more information, see [Request Features](xref:fundamentals/request-features).</span></span>

## <a name="open-web-interface-for-net-owin"></a><span data-ttu-id="e1409-207">Spustit nástroj webové rozhraní pro platformu .NET (OWIN)</span><span class="sxs-lookup"><span data-stu-id="e1409-207">Open Web Interface for .NET (OWIN)</span></span>

<span data-ttu-id="e1409-208">Jádro ASP.NET podporuje Open Web Interface pro .NET (OWIN).</span><span class="sxs-lookup"><span data-stu-id="e1409-208">ASP.NET Core supports the Open Web Interface for .NET (OWIN).</span></span> <span data-ttu-id="e1409-209">OWIN umožňuje webových aplikací pro být odděleno od webové servery.</span><span class="sxs-lookup"><span data-stu-id="e1409-209">OWIN allows web apps to be decoupled from web servers.</span></span>

<span data-ttu-id="e1409-210">Další informace najdete v tématu [Open Web Interface pro .NET (OWIN)](xref:fundamentals/owin).</span><span class="sxs-lookup"><span data-stu-id="e1409-210">For more information, see [Open Web Interface for .NET (OWIN)](xref:fundamentals/owin).</span></span>

## <a name="websockets"></a><span data-ttu-id="e1409-211">Technologie WebSockets</span><span class="sxs-lookup"><span data-stu-id="e1409-211">WebSockets</span></span>

<span data-ttu-id="e1409-212">[Protokol WebSocket](https://wikipedia.org/wiki/WebSocket) je protokol, který umožňuje obousměrný trvalé komunikačních kanálů přes připojení TCP.</span><span class="sxs-lookup"><span data-stu-id="e1409-212">[WebSocket](https://wikipedia.org/wiki/WebSocket) is a protocol that enables two-way persistent communication channels over TCP connections.</span></span> <span data-ttu-id="e1409-213">Použije se pro aplikace, jako je například chat, kurzů akcií, hry a kdekoli požadavky v reálném čase funkce ve webové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="e1409-213">It's used for apps such as chat, stock tickers, games, and anywhere you desire real-time functionality in a web app.</span></span> <span data-ttu-id="e1409-214">Jádro ASP.NET podporuje webových funkcí produktu soketu.</span><span class="sxs-lookup"><span data-stu-id="e1409-214">ASP.NET Core supports web socket features.</span></span>

<span data-ttu-id="e1409-215">Další informace najdete v tématu [Websocket](xref:fundamentals/websockets).</span><span class="sxs-lookup"><span data-stu-id="e1409-215">For more information, see [WebSockets](xref:fundamentals/websockets).</span></span>

## <a name="microsoftaspnetcoreall-metapackage"></a><span data-ttu-id="e1409-216">Microsoft.AspNetCore.All metapackage</span><span class="sxs-lookup"><span data-stu-id="e1409-216">Microsoft.AspNetCore.All metapackage</span></span>

<span data-ttu-id="e1409-217">[Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) metapackage pro ASP.NET Core zahrnuje:</span><span class="sxs-lookup"><span data-stu-id="e1409-217">The [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All) metapackage for ASP.NET Core includes:</span></span>

* <span data-ttu-id="e1409-218">Všechny podporované balíčky tým ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="e1409-218">All supported packages by the ASP.NET Core team.</span></span>
* <span data-ttu-id="e1409-219">Všechny podporované balíčků základní Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="e1409-219">All supported packages by the Entity Framework Core.</span></span> 
* <span data-ttu-id="e1409-220">Interní a 3. stran závislosti používané ASP.NET Core a Entity Framework Core.</span><span class="sxs-lookup"><span data-stu-id="e1409-220">Internal and 3rd-party dependencies used by ASP.NET Core and Entity Framework Core.</span></span>

<span data-ttu-id="e1409-221">Další informace najdete v tématu [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span><span class="sxs-lookup"><span data-stu-id="e1409-221">For more information, see [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span></span>

## <a name="net-core-vs-net-framework-runtime"></a><span data-ttu-id="e1409-222">Modul runtime rozhraní .NET core a rozhraní .NET Framework</span><span class="sxs-lookup"><span data-stu-id="e1409-222">.NET Core vs. .NET Framework runtime</span></span>

<span data-ttu-id="e1409-223">Aplikace ASP.NET Core, můžete vybrat runtime .NET Core nebo rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="e1409-223">An ASP.NET Core app can target the .NET Core or .NET Framework runtime.</span></span>

<span data-ttu-id="e1409-224">Další informace najdete v tématu [výběru mezi .NET Core a rozhraní .NET Framework](/dotnet/articles/standard/choosing-core-framework-server).</span><span class="sxs-lookup"><span data-stu-id="e1409-224">For more information, see [Choosing between .NET Core and .NET Framework](/dotnet/articles/standard/choosing-core-framework-server).</span></span>

## <a name="choose-between-aspnet-core-and-aspnet"></a><span data-ttu-id="e1409-225">Zvolte mezi ASP.NET Core a ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e1409-225">Choose between ASP.NET Core and ASP.NET</span></span>

<span data-ttu-id="e1409-226">Další informace o výběru mezi ASP.NET Core a ASP.NET naleznete v tématu [zvolte mezi ASP.NET Core a ASP.NET](xref:fundamentals/choose-between-aspnet-and-aspnetcore).</span><span class="sxs-lookup"><span data-stu-id="e1409-226">For more information on choosing between ASP.NET Core and ASP.NET, see [Choose between ASP.NET Core and ASP.NET](xref:fundamentals/choose-between-aspnet-and-aspnetcore).</span></span>