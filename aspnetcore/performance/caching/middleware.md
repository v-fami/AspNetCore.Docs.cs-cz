---
title: "Ukládání do mezipaměti Middleware v ASP.NET Core odpovědi"
author: guardrex
description: "Zjistěte, jak konfigurovat a používat Middleware ukládání do mezipaměti odpovědi v aplikacích ASP.NET Core."
ms.author: riande
manager: wpickett
ms.date: 08/22/2017
ms.topic: article
ms.prod: asp.net-core
uid: performance/caching/middleware
ms.openlocfilehash: f3312d0c333b47169c71891eea79f03be0abcfa3
ms.sourcegitcommit: 216dfac27542f10a79274a9ce60dc449e888ed20
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/29/2017
---
# <a name="response-caching-middleware-in-aspnet-core"></a><span data-ttu-id="e8f3b-103">Ukládání do mezipaměti Middleware v ASP.NET Core odpovědi</span><span class="sxs-lookup"><span data-stu-id="e8f3b-103">Response Caching Middleware in ASP.NET Core</span></span>

<span data-ttu-id="e8f3b-104">Podle [Luke Latham](https://github.com/guardrex) a [Luo Jan](https://github.com/JunTaoLuo)</span><span class="sxs-lookup"><span data-stu-id="e8f3b-104">By [Luke Latham](https://github.com/guardrex) and [John Luo](https://github.com/JunTaoLuo)</span></span>

<span data-ttu-id="e8f3b-105">[Zobrazit nebo stáhnout ukázkový kód](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/middleware/samples) ([stažení](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="e8f3b-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/middleware/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="e8f3b-106">Tento dokument obsahuje podrobnosti o tom, jak nakonfigurovat Middleware ukládání do mezipaměti odpovědi v aplikacích ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-106">This document provides details on how to configure the Response Caching Middleware in ASP.NET Core apps.</span></span> <span data-ttu-id="e8f3b-107">Middleware Určuje, pokud jsou odpovědi lze uložit do mezipaměti, ukládá odpovědi a slouží odpovědi z mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-107">The middleware determines when responses are cacheable, stores responses, and serves responses from cache.</span></span> <span data-ttu-id="e8f3b-108">Úvod do ukládání do mezipaměti HTTP a `ResponseCache` atributů najdete v tématu [ukládání odpovědí do mezipaměti](response.md).</span><span class="sxs-lookup"><span data-stu-id="e8f3b-108">For an introduction to HTTP caching and the `ResponseCache` attribute, see [Response Caching](response.md).</span></span>

## <a name="package"></a><span data-ttu-id="e8f3b-109">Balíček</span><span class="sxs-lookup"><span data-stu-id="e8f3b-109">Package</span></span>
<span data-ttu-id="e8f3b-110">Pokud chcete middleware v projektu, přidejte odkaz na [ `Microsoft.AspNetCore.ResponseCaching` ](https://www.nuget.org/packages/Microsoft.AspNetCore.ResponseCaching/) balíček nebo použít [ `Microsoft.AspNetCore.All` ](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) balíčku.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-110">To include the middleware in a project, add a reference to the [`Microsoft.AspNetCore.ResponseCaching`](https://www.nuget.org/packages/Microsoft.AspNetCore.ResponseCaching/) package or use the [`Microsoft.AspNetCore.All`](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) package.</span></span>

## <a name="configuration"></a><span data-ttu-id="e8f3b-111">Konfigurace</span><span class="sxs-lookup"><span data-stu-id="e8f3b-111">Configuration</span></span>
<span data-ttu-id="e8f3b-112">V `ConfigureServices`, přidat middleware ke kolekci služby.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-112">In `ConfigureServices`, add the middleware to the service collection.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="e8f3b-113">ASP.NET základní 2.x</span><span class="sxs-lookup"><span data-stu-id="e8f3b-113">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](middleware/samples/2.x/Program.cs?name=snippet1&highlight=4)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="e8f3b-114">ASP.NET základní 1.x</span><span class="sxs-lookup"><span data-stu-id="e8f3b-114">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](middleware/samples/1.x/Startup.cs?name=snippet1&highlight=3)]

---

<span data-ttu-id="e8f3b-115">Nakonfigurovat aplikaci, aby používala middlewaru s `UseResponseCaching` metoda rozšíření, která přidá middleware kanálu zpracování požadavků.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-115">Configure the app to use the middleware with the `UseResponseCaching` extension method, which adds the middleware to the request processing pipeline.</span></span> <span data-ttu-id="e8f3b-116">Ukázková aplikace přidá [ `Cache-Control` ](https://tools.ietf.org/html/rfc7234#section-5.2) hlavičky odpovědi, který ukládá do mezipaměti odpovědi lze uložit do mezipaměti pro až 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-116">The sample app adds a [`Cache-Control`](https://tools.ietf.org/html/rfc7234#section-5.2) header to the response that caches cacheable responses for up to 10 seconds.</span></span> <span data-ttu-id="e8f3b-117">Odesílá vzorek [ `Vary` ](https://tools.ietf.org/html/rfc7231#section-7.1.4) záhlaví pro konfiguraci middlewaru k obsluze odpovědi v mezipaměti pouze v případě [ `Accept-Encoding` ](https://tools.ietf.org/html/rfc7231#section-5.3.4) záhlaví následných žádostí se shoduje s původní žádost.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-117">The sample sends a [`Vary`](https://tools.ietf.org/html/rfc7231#section-7.1.4) header to configure the middleware to serve a cached response only if the [`Accept-Encoding`](https://tools.ietf.org/html/rfc7231#section-5.3.4) header of subsequent requests matches that of the original request.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="e8f3b-118">ASP.NET základní 2.x</span><span class="sxs-lookup"><span data-stu-id="e8f3b-118">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

[!code-csharp[Main](middleware/samples/2.x/Program.cs?name=snippet1&highlight=8)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="e8f3b-119">ASP.NET základní 1.x</span><span class="sxs-lookup"><span data-stu-id="e8f3b-119">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

[!code-csharp[Main](middleware/samples/1.x/Startup.cs?name=snippet2&highlight=3)]

---

<span data-ttu-id="e8f3b-120">Middleware ukládání do mezipaměti odpovědi pouze ukládá do mezipaměti odpovědi serveru 200 (OK).</span><span class="sxs-lookup"><span data-stu-id="e8f3b-120">The Response Caching Middleware only caches 200 (OK) server responses.</span></span> <span data-ttu-id="e8f3b-121">Žádné jiné reakce, včetně [chybové stránky](xref:fundamentals/error-handling), ignorují middlewarem.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-121">Any other responses, including [error pages](xref:fundamentals/error-handling), are ignored by the middleware.</span></span>

> [!WARNING]
> <span data-ttu-id="e8f3b-122">Odpovědím obsahujícím obsah pro klienty ověřené musí být označen jako není Uložitelný, aby se zabránilo middleware z ukládání a současné obsluhování těchto odpovědí.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-122">Responses containing content for authenticated clients must be marked as not cacheable to prevent the middleware from storing and serving those responses.</span></span> <span data-ttu-id="e8f3b-123">V tématu [podmínky pro ukládání do mezipaměti](#conditions-for-caching) podrobnosti o tom, jak middleware Určuje, zda odpověď lze uložit do mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-123">See [Conditions for caching](#conditions-for-caching) for details on how the middleware determines if a response is cacheable.</span></span>

## <a name="options"></a><span data-ttu-id="e8f3b-124">Možnosti</span><span class="sxs-lookup"><span data-stu-id="e8f3b-124">Options</span></span>
<span data-ttu-id="e8f3b-125">Middleware nabízí tři možnosti pro řízení ukládání do mezipaměti odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-125">The middleware offers three options for controlling response caching.</span></span>

| <span data-ttu-id="e8f3b-126">Možnost</span><span class="sxs-lookup"><span data-stu-id="e8f3b-126">Option</span></span>                | <span data-ttu-id="e8f3b-127">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="e8f3b-127">Default Value</span></span> |
| --------------------- | ------------- |
| <span data-ttu-id="e8f3b-128">UseCaseSensitivePaths</span><span class="sxs-lookup"><span data-stu-id="e8f3b-128">UseCaseSensitivePaths</span></span> | <span data-ttu-id="e8f3b-129">Určuje, pokud jsou odpovědi ukládat do mezipaměti na malá a velká písmena cesty.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-129">Determines if responses are cached on case-sensitive paths.</span></span></p><p><span data-ttu-id="e8f3b-130">Výchozí hodnota je `false`.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-130">The default value is `false`.</span></span> |
| <span data-ttu-id="e8f3b-131">MaximumBodySize</span><span class="sxs-lookup"><span data-stu-id="e8f3b-131">MaximumBodySize</span></span>       | <span data-ttu-id="e8f3b-132">Největší velikost lze uložit do mezipaměti pro text odpovědi v bajtech.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-132">The largest cacheable size for the response body in bytes.</span></span></p><span data-ttu-id="e8f3b-133">Výchozí hodnota je `64 * 1024 * 1024` (64 MB).</span><span class="sxs-lookup"><span data-stu-id="e8f3b-133">The default value is `64 * 1024 * 1024` (64 MB).</span></span> |
| <span data-ttu-id="e8f3b-134">SizeLimit</span><span class="sxs-lookup"><span data-stu-id="e8f3b-134">SizeLimit</span></span>             | <span data-ttu-id="e8f3b-135">Omezení velikosti pro middleware mezipaměti odpovědi v bajtech.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-135">The size limit for the response cache middleware in bytes.</span></span> <span data-ttu-id="e8f3b-136">Výchozí hodnota je `100 * 1024 * 1024` (100 MB).</span><span class="sxs-lookup"><span data-stu-id="e8f3b-136">The default value is `100 * 1024 * 1024` (100 MB).</span></span> |

<span data-ttu-id="e8f3b-137">Následující příklad konfiguruje middleware do mezipaměti odpovědi menší než nebo rovna 1024 bajtů pomocí cesty malá a velká písmena, ukládání odpovědí na `/page1` a `/Page1` samostatně.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-137">The following example configures the middleware to cache responses smaller than or equal to 1,024 bytes using case-sensitive paths, storing the responses to `/page1` and `/Page1` separately.</span></span>

```csharp
services.AddResponseCaching(options =>
{
    options.UseCaseSensitivePaths = true;
    options.MaximumBodySize = 1024;
});
```

## <a name="varybyquerykeys"></a><span data-ttu-id="e8f3b-138">VaryByQueryKeys</span><span class="sxs-lookup"><span data-stu-id="e8f3b-138">VaryByQueryKeys</span></span>
<span data-ttu-id="e8f3b-139">Při použití MVC, `ResponseCache` atribut určuje parametry, které jsou nezbytné pro nastavení odpovídající hlavičky pro ukládání odpovědí do mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-139">When using MVC, the `ResponseCache` attribute specifies the parameters necessary for setting appropriate headers for response caching.</span></span> <span data-ttu-id="e8f3b-140">Parametr pouze `ResponseCache` je atribut, který vyžaduje výhradně middleware `VaryByQueryKeys`, který neodpovídá skutečné záhlaví HTTP.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-140">The only parameter of the `ResponseCache` attribute that strictly requires the middleware is `VaryByQueryKeys`, which doesn't correspond to an actual HTTP header.</span></span> <span data-ttu-id="e8f3b-141">Další informace najdete v tématu [ResponseCache atribut](response.md#responsecache-attribute).</span><span class="sxs-lookup"><span data-stu-id="e8f3b-141">For more information, see [ResponseCache Attribute](response.md#responsecache-attribute).</span></span>

<span data-ttu-id="e8f3b-142">Pokud nepoužíváte MVC, můžete měnit ukládání do mezipaměti odpovědi `VaryByQueryKeys` funkce.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-142">When not using MVC, you can vary response caching with the `VaryByQueryKeys` feature.</span></span> <span data-ttu-id="e8f3b-143">Použití `ResponseCachingFeature` přímo z `IFeatureCollection` z `HttpContext`:</span><span class="sxs-lookup"><span data-stu-id="e8f3b-143">Use the `ResponseCachingFeature` directly from the `IFeatureCollection` of the `HttpContext`:</span></span>

```csharp
var responseCachingFeature = context.HttpContext.Features.Get<IResponseCachingFeature>();
if (responseCachingFeature != null)
{
    responseCachingFeature.VaryByQueryKeys = new[] { "MyKey" };
}
```

## <a name="http-headers-used-by-response-caching-middleware"></a><span data-ttu-id="e8f3b-144">Hlavičky HTTP používaný Middleware ukládání do mezipaměti odpovědi</span><span class="sxs-lookup"><span data-stu-id="e8f3b-144">HTTP headers used by Response Caching Middleware</span></span>
<span data-ttu-id="e8f3b-145">Ukládání do mezipaměti podle middleware odpovědi je nakonfigurován pomocí hlavičky protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-145">Response caching by the middleware is configured via HTTP headers.</span></span> <span data-ttu-id="e8f3b-146">Relevantní hlavičky jsou uvedeny pod poznámky na tom, jak ovlivňují ukládání do mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-146">The relevant headers are listed below with notes on how they affect caching.</span></span>

| <span data-ttu-id="e8f3b-147">Záhlaví</span><span class="sxs-lookup"><span data-stu-id="e8f3b-147">Header</span></span> | <span data-ttu-id="e8f3b-148">Podrobnosti</span><span class="sxs-lookup"><span data-stu-id="e8f3b-148">Details</span></span> |
| ------ | ------- |
| <span data-ttu-id="e8f3b-149">Autorizace</span><span class="sxs-lookup"><span data-stu-id="e8f3b-149">Authorization</span></span> | <span data-ttu-id="e8f3b-150">Odpověď není v mezipaměti, pokud existuje hlavička.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-150">The response isn't cached if the header exists.</span></span> |
| <span data-ttu-id="e8f3b-151">Cache-Control</span><span class="sxs-lookup"><span data-stu-id="e8f3b-151">Cache-Control</span></span> | <span data-ttu-id="e8f3b-152">Middleware uvažuje pouze ukládání do mezipaměti odpovědi, které jsou označené jako `public` direktiva mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-152">The middleware only considers caching responses marked with the `public` cache directive.</span></span> <span data-ttu-id="e8f3b-153">Můžete řídit ukládání do mezipaměti s následujícími parametry:</span><span class="sxs-lookup"><span data-stu-id="e8f3b-153">You can control caching with the following parameters:</span></span><ul><li><span data-ttu-id="e8f3b-154">Maximální stáří</span><span class="sxs-lookup"><span data-stu-id="e8f3b-154">max-age</span></span></li><li><span data-ttu-id="e8f3b-155">maximální počet zastaralé &#8224;</span><span class="sxs-lookup"><span data-stu-id="e8f3b-155">max-stale&#8224;</span></span></li><li><span data-ttu-id="e8f3b-156">čerstvě min.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-156">min-fresh</span></span></li><li><span data-ttu-id="e8f3b-157">musí revalidate</span><span class="sxs-lookup"><span data-stu-id="e8f3b-157">must-revalidate</span></span></li><li><span data-ttu-id="e8f3b-158">Ne mezipaměti</span><span class="sxs-lookup"><span data-stu-id="e8f3b-158">no-cache</span></span></li><li><span data-ttu-id="e8f3b-159">Ne – úložiště</span><span class="sxs-lookup"><span data-stu-id="e8f3b-159">no-store</span></span></li><li><span data-ttu-id="e8f3b-160">pouze v případě mezipaměti</span><span class="sxs-lookup"><span data-stu-id="e8f3b-160">only-if-cached</span></span></li><li><span data-ttu-id="e8f3b-161">private</span><span class="sxs-lookup"><span data-stu-id="e8f3b-161">private</span></span></li><li><span data-ttu-id="e8f3b-162">public</span><span class="sxs-lookup"><span data-stu-id="e8f3b-162">public</span></span></li><li><span data-ttu-id="e8f3b-163">s maxage</span><span class="sxs-lookup"><span data-stu-id="e8f3b-163">s-maxage</span></span></li><li><span data-ttu-id="e8f3b-164">proxy server revalidate &#8225;</span><span class="sxs-lookup"><span data-stu-id="e8f3b-164">proxy-revalidate&#8225;</span></span></li></ul><span data-ttu-id="e8f3b-165">&#8224; Pokud není zadáno žádné omezení na `max-stale`, middleware neprovede žádnou akci.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-165">&#8224;If no limit is specified to `max-stale`, the middleware takes no action.</span></span><br><span data-ttu-id="e8f3b-166">&#8225; `proxy-revalidate` má stejný účinek jako `must-revalidate`.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-166">&#8225;`proxy-revalidate` has the same effect as `must-revalidate`.</span></span><br><br><span data-ttu-id="e8f3b-167">Další informace najdete v tématu [RFC 7231: požadavku direktivy Cache-Control](https://tools.ietf.org/html/rfc7234#section-5.2.1).</span><span class="sxs-lookup"><span data-stu-id="e8f3b-167">For more information, see [RFC 7231: Request Cache-Control Directives](https://tools.ietf.org/html/rfc7234#section-5.2.1).</span></span> |
| <span data-ttu-id="e8f3b-168">Direktiva pragma</span><span class="sxs-lookup"><span data-stu-id="e8f3b-168">Pragma</span></span> | <span data-ttu-id="e8f3b-169">A `Pragma: no-cache` hlavičky v požadavku vytváří stejného efektu jako `Cache-Control: no-cache`.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-169">A `Pragma: no-cache` header in the request produces the same effect as `Cache-Control: no-cache`.</span></span> <span data-ttu-id="e8f3b-170">Tuto hlavičku je přepsat relevantní direktivy v `Cache-Control` záhlaví, pokud je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-170">This header is overridden by the relevant directives in the `Cache-Control` header, if present.</span></span> <span data-ttu-id="e8f3b-171">Za pro zpětnou kompatibilitu s HTTP/1.0.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-171">Considered for backward compatibility with HTTP/1.0.</span></span> |
| <span data-ttu-id="e8f3b-172">Set-Cookie</span><span class="sxs-lookup"><span data-stu-id="e8f3b-172">Set-Cookie</span></span> | <span data-ttu-id="e8f3b-173">Odpověď není v mezipaměti, pokud existuje hlavička.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-173">The response isn't cached if the header exists.</span></span> |
| <span data-ttu-id="e8f3b-174">lišit</span><span class="sxs-lookup"><span data-stu-id="e8f3b-174">Vary</span></span> | <span data-ttu-id="e8f3b-175">`Vary` Záhlaví slouží k odlišení odpověď uložená v mezipaměti jiné záhlaví.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-175">The `Vary` header is used to vary the cached response by another header.</span></span> <span data-ttu-id="e8f3b-176">Například můžete pomocí kódování zahrnutím mezipaměti odpovědi `Vary: Accept-Encoding` hlavičky, která ukládá do mezipaměti odpovědi pro požadavky s hlavičky `Accept-Encoding: gzip` a `Accept-Encoding: text/plain` samostatně.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-176">For example, you can cache responses by encoding by including the `Vary: Accept-Encoding` header, which caches responses for requests with headers `Accept-Encoding: gzip` and `Accept-Encoding: text/plain` separately.</span></span> <span data-ttu-id="e8f3b-177">Odpověď se hodnota hlavičky `*` nikdy neuloží.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-177">A response with a header value of `*` is never stored.</span></span> |
| <span data-ttu-id="e8f3b-178">Vypršení platnosti</span><span class="sxs-lookup"><span data-stu-id="e8f3b-178">Expires</span></span> | <span data-ttu-id="e8f3b-179">Odpovědi, které tuto hlavičku považují za zastaralé není uložen nebo načíst, pokud není přepsána jiná `Cache-Control` hlavičky.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-179">A response deemed stale by this header isn't stored or retrieved unless overridden by other `Cache-Control` headers.</span></span> |
| <span data-ttu-id="e8f3b-180">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="e8f3b-180">If-None-Match</span></span> | <span data-ttu-id="e8f3b-181">Úplnou odpověď je zpracovat z mezipaměti, pokud hodnota není `*` a `ETag` odpovědi neodpovídá zadanými hodnotami.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-181">The full response is served from cache if the value isn't `*` and the `ETag` of the response doesn't match any of the values provided.</span></span> <span data-ttu-id="e8f3b-182">Odpověď 304 (upraveno), jinak je zpracovat.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-182">Otherwise, a 304 (Not Modified) response is served.</span></span> |
| <span data-ttu-id="e8f3b-183">Pokud upravit – od</span><span class="sxs-lookup"><span data-stu-id="e8f3b-183">If-Modified-Since</span></span> | <span data-ttu-id="e8f3b-184">Pokud `If-None-Match` hlavičky není přítomen, úplnou odpověď je zpracovat z mezipaměti, pokud je novější než hodnota zadaná data odpovědi v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-184">If the `If-None-Match` header isn't present, a full response is served from cache if the cached response date is newer than the value provided.</span></span> <span data-ttu-id="e8f3b-185">Odpověď 304 (upraveno), jinak je zpracovat.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-185">Otherwise, a 304 (Not Modified) response is served.</span></span> |
| <span data-ttu-id="e8f3b-186">Datum</span><span class="sxs-lookup"><span data-stu-id="e8f3b-186">Date</span></span> | <span data-ttu-id="e8f3b-187">Když obsluhující z mezipaměti, `Date` záhlaví je nastavení middleware, pokud nebyl zadán v původní odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-187">When serving from cache, the `Date` header is set by the middleware if it wasn't provided on the original response.</span></span> |
| <span data-ttu-id="e8f3b-188">Délka obsahu</span><span class="sxs-lookup"><span data-stu-id="e8f3b-188">Content-Length</span></span> | <span data-ttu-id="e8f3b-189">Když obsluhující z mezipaměti, `Content-Length` záhlaví je nastavení middleware, pokud nebyl zadán v původní odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-189">When serving from cache, the `Content-Length` header is set by the middleware if it wasn't provided on the original response.</span></span> |
| <span data-ttu-id="e8f3b-190">stáří</span><span class="sxs-lookup"><span data-stu-id="e8f3b-190">Age</span></span> | <span data-ttu-id="e8f3b-191">`Age` Záhlaví odeslaný v odpovědi původní je ignorována.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-191">The `Age` header sent in the original response is ignored.</span></span> <span data-ttu-id="e8f3b-192">Middleware vypočítá novou hodnotu, pokud obsluhující odpovědi v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-192">The middleware computes a new value when serving a cached response.</span></span> |

## <a name="caching-respects-request-cache-control-directives"></a><span data-ttu-id="e8f3b-193">Ukládání do mezipaměti respektuje direktivy požadavek Cache-Control</span><span class="sxs-lookup"><span data-stu-id="e8f3b-193">Caching respects request Cache-Control directives</span></span>

<span data-ttu-id="e8f3b-194">Middleware respektuje pravidla [ukládání do mezipaměti HTTP 1.1 specifikace](https://tools.ietf.org/html/rfc7234#section-5.2).</span><span class="sxs-lookup"><span data-stu-id="e8f3b-194">The middleware respects the rules of the [HTTP 1.1 Caching specification](https://tools.ietf.org/html/rfc7234#section-5.2).</span></span> <span data-ttu-id="e8f3b-195">Pravidla vyžadovat mezipaměti vyhovět platná `Cache-Control` hlavička odeslaná klientem.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-195">The rules require a cache to honor a valid `Cache-Control` header sent by the client.</span></span> <span data-ttu-id="e8f3b-196">V části specifikace, klient provádět požadavky `no-cache` hodnota hlavičky a force serveru pro generování novou odpověď pro každý požadavek.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-196">Under the specification, a client can make requests with a `no-cache` header value and force a server to generate a new response for every request.</span></span> <span data-ttu-id="e8f3b-197">V současné době není žádné vývojáři řídit toto chování ukládání do mezipaměti při použití middleware, protože middleware dodržuje specifikaci oficiální ukládání do mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-197">Currently, there's no developer control over this caching behavior when using the middleware because the middleware adheres to the official caching specification.</span></span>

<span data-ttu-id="e8f3b-198">[Budoucí vylepšení middleware](https://github.com/aspnet/ResponseCaching/issues/96) povolí přístup konfigurace middleware pro ukládání do mezipaměti scénáře kde žádost `Cache-Control` záhlaví třeba ji ignorovat při rozhodování, která bude sloužit odpovědi v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-198">[Future enhancements to the middleware](https://github.com/aspnet/ResponseCaching/issues/96) will permit configuring the middleware for caching scenarios where the request `Cache-Control` header should be ignored when deciding to serve a cached response.</span></span> <span data-ttu-id="e8f3b-199">Při hledání větší kontrolu nad chování ukládání do mezipaměti, prozkoumejte jiné funkce ukládání do mezipaměti ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-199">If you seek more control over caching behavior, explore other caching features of ASP.NET Core.</span></span> <span data-ttu-id="e8f3b-200">Najdete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="e8f3b-200">See the following topics:</span></span>

* [<span data-ttu-id="e8f3b-201">Ukládání do mezipaměti v paměti</span><span class="sxs-lookup"><span data-stu-id="e8f3b-201">In-memory caching</span></span>](xref:performance/caching/memory)
* [<span data-ttu-id="e8f3b-202">Práce s distribuované mezipaměti</span><span class="sxs-lookup"><span data-stu-id="e8f3b-202">Working with a distributed cache</span></span>](xref:performance/caching/distributed)
* [<span data-ttu-id="e8f3b-203">Značka Pomocník jádro ASP.NET MVC do mezipaměti</span><span class="sxs-lookup"><span data-stu-id="e8f3b-203">Cache Tag Helper in ASP.NET Core MVC</span></span>](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [<span data-ttu-id="e8f3b-204">Pomocník značky distribuované mezipaměti</span><span class="sxs-lookup"><span data-stu-id="e8f3b-204">Distributed Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)

## <a name="troubleshooting"></a><span data-ttu-id="e8f3b-205">Poradce při potížích</span><span class="sxs-lookup"><span data-stu-id="e8f3b-205">Troubleshooting</span></span>
<span data-ttu-id="e8f3b-206">Není-li chování ukládání do mezipaměti podle očekávání, ověřte, zda jsou odpovědí lze uložit do mezipaměti a je schopný obsluhovány z mezipaměti tak, že prověří hlavičky příchozí žádosti a odpovědi na odchozí.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-206">If caching behavior isn't as you expect, confirm that responses are cacheable and capable of being served from the cache by examining the request's incoming headers and the response's outgoing headers.</span></span> <span data-ttu-id="e8f3b-207">Povolení [protokolování](xref:fundamentals/logging/index) může pomoci při ladění.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-207">Enabling [logging](xref:fundamentals/logging/index) can help when debugging.</span></span> <span data-ttu-id="e8f3b-208">Middleware protokoly ukládání do mezipaměti chování, pokud je odpověď načten z mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-208">The middleware logs caching behavior and when a response is retrieved from cache.</span></span>

<span data-ttu-id="e8f3b-209">Při testování a řešení potíží s chování ukládání do mezipaměti, prohlížeče může nastavit hlavičky žádosti, které ovlivňují ukládání do nežádoucího způsoby.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-209">When testing and troubleshooting caching behavior, a browser may set request headers that affect caching in undesirable ways.</span></span> <span data-ttu-id="e8f3b-210">Například může nastavit prohlížeče `Cache-Control` hlavičky k `no-cache` při aktualizaci stránky.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-210">For example, a browser may set the `Cache-Control` header to `no-cache` when you refresh the page.</span></span> <span data-ttu-id="e8f3b-211">Tyto nástroje můžete explicitně nastavit hlavičky požadavku a jsou upřednostněny testování ukládání do mezipaměti:</span><span class="sxs-lookup"><span data-stu-id="e8f3b-211">The following tools can explicitly set request headers, and are preferred for testing caching:</span></span>

* [<span data-ttu-id="e8f3b-212">Fiddler</span><span class="sxs-lookup"><span data-stu-id="e8f3b-212">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="e8f3b-213">FireBug</span><span class="sxs-lookup"><span data-stu-id="e8f3b-213">Firebug</span></span>](http://getfirebug.com/)
* [<span data-ttu-id="e8f3b-214">Postman</span><span class="sxs-lookup"><span data-stu-id="e8f3b-214">Postman</span></span>](https://www.getpostman.com/)

### <a name="conditions-for-caching"></a><span data-ttu-id="e8f3b-215">Podmínky pro ukládání do mezipaměti</span><span class="sxs-lookup"><span data-stu-id="e8f3b-215">Conditions for caching</span></span>
* <span data-ttu-id="e8f3b-216">Žádost musí mít za následek 200 (OK) odpověď ze serveru.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-216">The request must result in a 200 (OK) response from the server.</span></span>
* <span data-ttu-id="e8f3b-217">Metoda požadavku musí být GET nebo HEAD.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-217">The request method must be GET or HEAD.</span></span>
* <span data-ttu-id="e8f3b-218">Terminálu middleware, jako je například Middleware statické soubory, nesmí zpracovat odpověď před Middleware ukládání do mezipaměti odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-218">Terminal middleware, such as Static File Middleware, must not process the response prior to the Response Caching Middleware.</span></span>
* <span data-ttu-id="e8f3b-219">`Authorization` Nesmí být záhlaví.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-219">The `Authorization` header must not be present.</span></span>
* <span data-ttu-id="e8f3b-220">`Cache-Control`Hlavička parametry musí být platný, a odpovědi musí být označen `public` a nesmí být označený `private`.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-220">`Cache-Control` header parameters must be valid, and the response must be marked `public` and not marked `private`.</span></span>
* <span data-ttu-id="e8f3b-221">`Pragma: no-cache` Nebo hodnota hlavičky se nesmějí vyskytovat Pokud `Cache-Control` hlavičky není přítomný, jako `Cache-Control` záhlaví přepsání `Pragma` záhlaví, pokud jsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-221">The `Pragma: no-cache` header/value must not be present if the `Cache-Control` header isn't present, as the `Cache-Control` header overrides the `Pragma` header when present.</span></span>
* <span data-ttu-id="e8f3b-222">`Set-Cookie` Nesmí být záhlaví.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-222">The `Set-Cookie` header must not be present.</span></span>
* <span data-ttu-id="e8f3b-223">`Vary`Hlavička parametry musí být platný a není rovno `*`.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-223">`Vary` header parameters must be valid and not equal to `*`.</span></span>
* <span data-ttu-id="e8f3b-224">`Content-Length` Hodnota hlavičky (Pokud nastavit) musí odpovídat velikost textu odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-224">The `Content-Length` header value (if set) must match the size of the response body.</span></span>
* <span data-ttu-id="e8f3b-225">[IHttpSendFileFeature](/aspnet/core/api/microsoft.aspnetcore.http.features.ihttpsendfilefeature) nepoužívá.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-225">The [IHttpSendFileFeature](/aspnet/core/api/microsoft.aspnetcore.http.features.ihttpsendfilefeature) isn't used.</span></span>
* <span data-ttu-id="e8f3b-226">Odpověď nesmí být zastaralé podle specifikace `Expires` záhlaví a `max-age` a `s-maxage` mezipaměti direktivy.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-226">The response must not be stale as specified by the `Expires` header and the `max-age` and `s-maxage` cache directives.</span></span>
* <span data-ttu-id="e8f3b-227">Ukládání odpovědi do vyrovnávací paměti je úspěšné, a velikost odpovědi je menší než nakonfigurované nebo výchozí `SizeLimit`.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-227">Response buffering is successful, and the size of the response is smaller than the configured or default `SizeLimit`.</span></span>
* <span data-ttu-id="e8f3b-228">Odpovědi musí být lze uložit do mezipaměti podle požadavků [RFC 7234](https://tools.ietf.org/html/rfc7234) specifikace.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-228">The response must be cacheable according to the [RFC 7234](https://tools.ietf.org/html/rfc7234) specifications.</span></span> <span data-ttu-id="e8f3b-229">Například `no-store` – direktiva nesmí existovat v pole hlavičky požadavku nebo odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-229">For example, the `no-store` directive must not exist in request or response header fields.</span></span> <span data-ttu-id="e8f3b-230">V tématu *část 3: uložení odpovědí v mezipaměti* z [RFC 7234](https://tools.ietf.org/html/rfc7234) podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-230">See *Section 3: Storing Responses in Caches* of [RFC 7234](https://tools.ietf.org/html/rfc7234) for details.</span></span>

> [!NOTE]
> <span data-ttu-id="e8f3b-231">Antiforgery systému ke generování tokenů zabezpečení, aby se zabránilo webů požadavku padělání (proti útokům CSRF) před útoky nastaví `Cache-Control` a `Pragma` záhlaví `no-cache` tak, aby se neukládají do mezipaměti odpovědi.</span><span class="sxs-lookup"><span data-stu-id="e8f3b-231">The Antiforgery system for generating secure tokens to prevent Cross-Site Request Forgery (CSRF) attacks sets the `Cache-Control` and `Pragma` headers to `no-cache` so that responses aren't cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e8f3b-232">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="e8f3b-232">Additional resources</span></span>

* [<span data-ttu-id="e8f3b-233">Spuštění aplikace</span><span class="sxs-lookup"><span data-stu-id="e8f3b-233">Application Startup</span></span>](xref:fundamentals/startup)
* [<span data-ttu-id="e8f3b-234">Middleware</span><span class="sxs-lookup"><span data-stu-id="e8f3b-234">Middleware</span></span>](xref:fundamentals/middleware)
* [<span data-ttu-id="e8f3b-235">Ukládání do mezipaměti v paměti</span><span class="sxs-lookup"><span data-stu-id="e8f3b-235">In-memory caching</span></span>](xref:performance/caching/memory)
* [<span data-ttu-id="e8f3b-236">Práce s distribuované mezipaměti</span><span class="sxs-lookup"><span data-stu-id="e8f3b-236">Working with a distributed cache</span></span>](xref:performance/caching/distributed)
* [<span data-ttu-id="e8f3b-237">Detekovat změny s tokeny změn</span><span class="sxs-lookup"><span data-stu-id="e8f3b-237">Detect changes with change tokens</span></span>](xref:fundamentals/primitives/change-tokens)
* [<span data-ttu-id="e8f3b-238">Ukládání odpovědí do mezipaměti</span><span class="sxs-lookup"><span data-stu-id="e8f3b-238">Response caching</span></span>](xref:performance/caching/response)
* [<span data-ttu-id="e8f3b-239">Pomocník značky mezipaměti</span><span class="sxs-lookup"><span data-stu-id="e8f3b-239">Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [<span data-ttu-id="e8f3b-240">Pomocník značky distribuované mezipaměti</span><span class="sxs-lookup"><span data-stu-id="e8f3b-240">Distributed Cache Tag Helper</span></span>](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)