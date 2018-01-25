---
title: "Protokolování v ASP.NET Core"
author: ardalis
description: "Další informace o rozhraní protokolování v ASP.NET Core. Zjistit předdefinované protokolování zprostředkovatele a další informace o oblíbených poskytovatelů třetích stran."
ms.author: tdykstra
manager: wpickett
ms.date: 12/15/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/logging/index
ms.openlocfilehash: 387d19af9165d4b54ce3cb1a9b04412271da6fb0
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/19/2018
---
# <a name="introduction-to-logging-in-aspnet-core"></a><span data-ttu-id="3d876-104">Úvod k protokolování v ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="3d876-104">Introduction to logging in ASP.NET Core</span></span>

<span data-ttu-id="3d876-105">Podle [Steve Smith](https://ardalis.com/) a [tní Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="3d876-105">By [Steve Smith](https://ardalis.com/) and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="3d876-106">Jádro ASP.NET podporuje protokolování rozhraní API, která funguje s různými zprostředkovatelů protokolování.</span><span class="sxs-lookup"><span data-stu-id="3d876-106">ASP.NET Core supports a logging API that works with a variety of logging providers.</span></span> <span data-ttu-id="3d876-107">Předdefinované zprostředkovatele umožňují odeslat protokoly na jeden nebo více míst, a můžete zařadit rozhraní protokolování třetích stran.</span><span class="sxs-lookup"><span data-stu-id="3d876-107">Built-in providers let you send logs to one or more destinations, and you can plug in a third-party logging framework.</span></span> <span data-ttu-id="3d876-108">Tento článek ukazuje, jak používat rozhraní API pro integrované protokolování a poskytovatelé ve vašem kódu.</span><span class="sxs-lookup"><span data-stu-id="3d876-108">This article shows how to use the built-in logging API and providers in your code.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3d876-109">ASP.NET základní 2.x</span><span class="sxs-lookup"><span data-stu-id="3d876-109">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="3d876-110">[Zobrazit nebo stáhnout ukázkový kód](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/sample2) ([stažení](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="3d876-110">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/sample2) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3d876-111">ASP.NET základní 1.x</span><span class="sxs-lookup"><span data-stu-id="3d876-111">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="3d876-112">[Zobrazit nebo stáhnout ukázkový kód](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/sample) ([stažení](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="3d876-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/index/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

---

## <a name="how-to-create-logs"></a><span data-ttu-id="3d876-113">Postup vytvoření protokoly</span><span class="sxs-lookup"><span data-stu-id="3d876-113">How to create logs</span></span>

<span data-ttu-id="3d876-114">Pokud chcete vytvořit protokoly, získat `ILogger` objektu z [vkládání závislostí](xref:fundamentals/dependency-injection) kontejneru:</span><span class="sxs-lookup"><span data-stu-id="3d876-114">To create logs, get an `ILogger` object from the [dependency injection](xref:fundamentals/dependency-injection) container:</span></span>

[!code-csharp[](index/sample/Controllers/TodoController.cs?name=snippet_LoggerDI&highlight=7)]

<span data-ttu-id="3d876-115">Pak volejte metody protokolování pro tento objekt protokolovacího nástroje:</span><span class="sxs-lookup"><span data-stu-id="3d876-115">Then call logging methods on that logger object:</span></span>

[!code-csharp[](index/sample/Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

<span data-ttu-id="3d876-116">Tento příklad vytvoří protokoly s `TodoController` třídy jako *kategorie*.</span><span class="sxs-lookup"><span data-stu-id="3d876-116">This example creates logs with the `TodoController` class as the *category*.</span></span> <span data-ttu-id="3d876-117">Kategorie jsou vysvětleny [dále v tomto článku](#log-category).</span><span class="sxs-lookup"><span data-stu-id="3d876-117">Categories are explained [later in this article](#log-category).</span></span>

<span data-ttu-id="3d876-118">ASP.NET Core neposkytuje asynchronní metody protokolovacího nástroje protože protokolování by měla být tak rychlé, že není vhodné nákladů na použití asynchronní.</span><span class="sxs-lookup"><span data-stu-id="3d876-118">ASP.NET Core does not provide async logger methods because logging should be so fast that it isn't worth the cost of using async.</span></span> <span data-ttu-id="3d876-119">Pokud jste v situaci, kde to není pravda, zvažte změnu způsob přihlášení.</span><span class="sxs-lookup"><span data-stu-id="3d876-119">If you're in a situation where that's not true, consider changing the way you log.</span></span> <span data-ttu-id="3d876-120">Pokud data store je pomalé, zápis zpráv protokolu rychlé úložiště nejprve, pak přesuňte je pomalé úložiště později.</span><span class="sxs-lookup"><span data-stu-id="3d876-120">If your data store is slow, write the log messages to a fast store first, then move them to a slow store later.</span></span> <span data-ttu-id="3d876-121">Například Přihlaste se do fronty zpráv, který je pro čtení a uložit trvale na pomalé úložiště jiným procesem.</span><span class="sxs-lookup"><span data-stu-id="3d876-121">For example, log to a message queue that is read and persisted to slow storage by another process.</span></span>

## <a name="how-to-add-providers"></a><span data-ttu-id="3d876-122">Postup přidání zprostředkovatelů</span><span class="sxs-lookup"><span data-stu-id="3d876-122">How to add providers</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3d876-123">ASP.NET základní 2.x</span><span class="sxs-lookup"><span data-stu-id="3d876-123">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="3d876-124">Zprostředkovatel protokolování přijímá zprávy, které vytvoříte pomocí `ILogger` objektu a zobrazuje nebo je uloží.</span><span class="sxs-lookup"><span data-stu-id="3d876-124">A logging provider takes the messages that you create with an `ILogger` object and displays or stores them.</span></span> <span data-ttu-id="3d876-125">Například konzola poskytovatel zprávy zobrazí v konzole a zprostředkovatele služby Azure App Service je uložit do úložiště objektů blob Azure.</span><span class="sxs-lookup"><span data-stu-id="3d876-125">For example, the Console provider displays messages on the console, and the Azure App Service provider can store them in Azure blob storage.</span></span>

<span data-ttu-id="3d876-126">Chcete-li použít poskytovatele, volejte poskytovatele `Add<ProviderName>` metoda rozšíření v *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="3d876-126">To use a provider, call the provider's `Add<ProviderName>` extension method in *Program.cs*:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_ExpandDefault&highlight=16,17)]

<span data-ttu-id="3d876-127">Výchozí šablona projektu umožňuje protokolování pomocí [CreateDefaultBuilder](https://docs.microsoft.com/ dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder?view=aspnetcore-2.0#Microsoft_AspNetCore_WebHost_CreateDefaultBuilder_System_String___) metoda:</span><span class="sxs-lookup"><span data-stu-id="3d876-127">The default project template enables logging with the [CreateDefaultBuilder](https://docs.microsoft.com/ dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder?view=aspnetcore-2.0#Microsoft_AspNetCore_WebHost_CreateDefaultBuilder_System_String___) method:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_TemplateCode&highlight=7)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3d876-128">ASP.NET základní 1.x</span><span class="sxs-lookup"><span data-stu-id="3d876-128">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="3d876-129">Zprostředkovatel protokolování přijímá zprávy, které vytvoříte pomocí `ILogger` objektu a zobrazuje nebo je uloží.</span><span class="sxs-lookup"><span data-stu-id="3d876-129">A logging provider takes the messages that you create with an `ILogger` object and displays or stores them.</span></span> <span data-ttu-id="3d876-130">Například konzola poskytovatel zprávy zobrazí v konzole a zprostředkovatele služby Azure App Service je uložit do úložiště objektů blob Azure.</span><span class="sxs-lookup"><span data-stu-id="3d876-130">For example, the Console provider displays messages on the console, and the Azure App Service provider can store them in Azure blob storage.</span></span>

<span data-ttu-id="3d876-131">Pro použití poskytovatele, nainstalujte jeho balíček NuGet a volání metody rozšíření poskytovatele na instanci `ILoggerFactory`, jak je znázorněno v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="3d876-131">To use a provider, install its NuGet package and call the provider's extension method on an instance of `ILoggerFactory`, as shown in the following example.</span></span>

[!code-csharp[](index/sample//Startup.cs?name=snippet_AddConsoleAndDebug&highlight=3,5-7)]

<span data-ttu-id="3d876-132">ASP.NET Core [vkládání závislostí](xref:fundamentals/dependency-injection) (DI) poskytuje `ILoggerFactory` instance.</span><span class="sxs-lookup"><span data-stu-id="3d876-132">ASP.NET Core [dependency injection](xref:fundamentals/dependency-injection) (DI) provides the `ILoggerFactory` instance.</span></span> <span data-ttu-id="3d876-133">`AddConsole` a `AddDebug` rozšiřující metody jsou definovány v [Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console/) a [Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug/) balíčky.</span><span class="sxs-lookup"><span data-stu-id="3d876-133">The `AddConsole` and `AddDebug` extension methods are defined in the [Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console/) and [Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug/) packages.</span></span> <span data-ttu-id="3d876-134">Každá metoda rozšíření volá `ILoggerFactory.AddProvider` metodu předáním v instanci poskytovatele.</span><span class="sxs-lookup"><span data-stu-id="3d876-134">Each extension method calls the `ILoggerFactory.AddProvider` method, passing in an instance of the provider.</span></span> 

> [!NOTE]
> <span data-ttu-id="3d876-135">Přidá zprostředkovatele protokolování v ukázkové aplikace pro tento článek `Configure` metodu `Startup` – třída.</span><span class="sxs-lookup"><span data-stu-id="3d876-135">The sample application for this article adds logging providers in the `Configure` method of the `Startup` class.</span></span> <span data-ttu-id="3d876-136">Pokud chcete získat výstup protokolu z kódu, který provede dříve, přidejte zprostředkovatele protokolování v `Startup` místo třídy konstruktor.</span><span class="sxs-lookup"><span data-stu-id="3d876-136">If you want to get log output from code that executes earlier, add logging providers in the `Startup` class constructor instead.</span></span> 

---

<span data-ttu-id="3d876-137">Najdete zde informace o jednotlivých [integrované protokolování zprostředkovatele](#built-in-logging-providers) a obsahuje odkazy na [poskytovatelů třetích stran protokolování](#third-party-logging-providers) dále v článku.</span><span class="sxs-lookup"><span data-stu-id="3d876-137">You'll find information about each [built-in logging provider](#built-in-logging-providers) and links to [third-party logging providers](#third-party-logging-providers) later in the article.</span></span>

## <a name="sample-logging-output"></a><span data-ttu-id="3d876-138">Ukázkový výstup protokolování</span><span class="sxs-lookup"><span data-stu-id="3d876-138">Sample logging output</span></span>

<span data-ttu-id="3d876-139">Ukázkový kód uvedené v předchozí části se zobrazí protokoly v konzole při spuštění z příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="3d876-139">With the sample code shown in the preceding section, you'll see logs in the console when you run from the command line.</span></span> <span data-ttu-id="3d876-140">Tady je příklad výstupu konzoly:</span><span class="sxs-lookup"><span data-stu-id="3d876-140">Here's an example of console output:</span></span>

```console
info: Microsoft.AspNetCore.Hosting.Internal.WebHost[1]
      Request starting HTTP/1.1 GET http://localhost:5000/api/todo/0
info: Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker[1]
      Executing action method TodoApi.Controllers.TodoController.GetById (TodoApi) with arguments (0) - ModelState is Valid
info: TodoApi.Controllers.TodoController[1002]
      Getting item 0
warn: TodoApi.Controllers.TodoController[4000]
      GetById(0) NOT FOUND
info: Microsoft.AspNetCore.Mvc.StatusCodeResult[1]
      Executing HttpStatusCodeResult, setting HTTP status code 404
info: Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker[2]
      Executed action TodoApi.Controllers.TodoController.GetById (TodoApi) in 42.9286ms
info: Microsoft.AspNetCore.Hosting.Internal.WebHost[2]
      Request finished in 148.889ms 404
```
 
<span data-ttu-id="3d876-141">Tyto protokoly byly vytvořeny tak, že přejdete do `http://localhost:5000/api/todo/0`, která aktivuje spuštění obou `ILogger` volání uvedené v předchozí části.</span><span class="sxs-lookup"><span data-stu-id="3d876-141">These logs were created by going to `http://localhost:5000/api/todo/0`, which triggers execution of both `ILogger` calls shown in the preceding section.</span></span>

<span data-ttu-id="3d876-142">Tady je příklad stejné protokolů, jak jsou zobrazeny v okně ladění, když spustíte ukázkovou aplikaci v sadě Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="3d876-142">Here's an example of the same logs as they appear in the Debug window when you run the sample application in Visual Studio:</span></span>

```console
Microsoft.AspNetCore.Hosting.Internal.WebHost:Information: Request starting HTTP/1.1 GET http://localhost:53104/api/todo/0  
Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker:Information: Executing action method TodoApi.Controllers.TodoController.GetById (TodoApi) with arguments (0) - ModelState is Valid
TodoApi.Controllers.TodoController:Information: Getting item 0
TodoApi.Controllers.TodoController:Warning: GetById(0) NOT FOUND
Microsoft.AspNetCore.Mvc.StatusCodeResult:Information: Executing HttpStatusCodeResult, setting HTTP status code 404
Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker:Information: Executed action TodoApi.Controllers.TodoController.GetById (TodoApi) in 152.5657ms
Microsoft.AspNetCore.Hosting.Internal.WebHost:Information: Request finished in 316.3195ms 404 
```

<span data-ttu-id="3d876-143">Protokoly, které byly vytvořeny `ILogger` volání uvedené v předchozí části začínat řetězcem "TodoApi.Controllers.TodoController".</span><span class="sxs-lookup"><span data-stu-id="3d876-143">The logs that were created by the `ILogger` calls shown in the preceding section begin with "TodoApi.Controllers.TodoController".</span></span> <span data-ttu-id="3d876-144">Protokoly, které začínají kategorie "Microsoft" jsou z ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="3d876-144">The logs that begin with "Microsoft" categories are from ASP.NET Core.</span></span> <span data-ttu-id="3d876-145">ASP.NET Core sám a kódu aplikace používají stejné rozhraní API protokolování a poskytovateli stejné protokolování.</span><span class="sxs-lookup"><span data-stu-id="3d876-145">ASP.NET Core itself and your application code are using the same logging API and the same logging providers.</span></span>

<span data-ttu-id="3d876-146">Zbývající část tohoto článku popisuje některé podrobnosti a možnosti pro protokolování.</span><span class="sxs-lookup"><span data-stu-id="3d876-146">The remainder of this article explains some details and options for logging.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="3d876-147">Balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="3d876-147">NuGet packages</span></span>

<span data-ttu-id="3d876-148">`ILogger` a `ILoggerFactory` rozhraní jsou v [Microsoft.Extensions.Logging.Abstractions](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions/), a výchozí implementace pro ně jsou v [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/).</span><span class="sxs-lookup"><span data-stu-id="3d876-148">The `ILogger` and `ILoggerFactory` interfaces are in [Microsoft.Extensions.Logging.Abstractions](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions/), and default implementations for them are in [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/).</span></span>

## <a name="log-category"></a><span data-ttu-id="3d876-149">Kategorie protokolu</span><span class="sxs-lookup"><span data-stu-id="3d876-149">Log category</span></span>

<span data-ttu-id="3d876-150">A *kategorie* je zahrnut v každém protokolu, který vytvoříte.</span><span class="sxs-lookup"><span data-stu-id="3d876-150">A *category* is included with each log that you create.</span></span> <span data-ttu-id="3d876-151">Zadejte kategorii, při vytváření `ILogger` objektu.</span><span class="sxs-lookup"><span data-stu-id="3d876-151">You specify the category when you create an `ILogger` object.</span></span> <span data-ttu-id="3d876-152">Kategorie může být libovolný řetězec, ale konvenci, je použít plně kvalifikovaný název třídy, ze kterého se zapisují protokoly.</span><span class="sxs-lookup"><span data-stu-id="3d876-152">The category may be any string, but a convention is to use the fully qualified name of the class from which the logs are written.</span></span> <span data-ttu-id="3d876-153">Například: "TodoApi.Controllers.TodoController".</span><span class="sxs-lookup"><span data-stu-id="3d876-153">For example: "TodoApi.Controllers.TodoController".</span></span>

<span data-ttu-id="3d876-154">Můžete zadat kategorii jako řetězec nebo použijte metodu rozšíření, která je odvozena kategorii z typu.</span><span class="sxs-lookup"><span data-stu-id="3d876-154">You can specify the category as a string or use an extension method that derives the category from the type.</span></span> <span data-ttu-id="3d876-155">Chcete-li zadat kategorii jako řetězec, volejte `CreateLogger` na `ILoggerFactory` instance, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="3d876-155">To specify the category as a string, call `CreateLogger` on an `ILoggerFactory` instance, as shown below.</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_CreateLogger&highlight=7,10)]

<span data-ttu-id="3d876-156">Ve většině případů, je jednodušší použít `ILogger<T>`, jako v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="3d876-156">Most of the time, it will be easier to use `ILogger<T>`, as in the following example.</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_LoggerDI&highlight=7)]

<span data-ttu-id="3d876-157">Jde o ekvivalent volání `CreateLogger` s názvem plně kvalifikovaný typ `T`.</span><span class="sxs-lookup"><span data-stu-id="3d876-157">This is equivalent to calling `CreateLogger` with the fully qualified type name of `T`.</span></span>

## <a name="log-level"></a><span data-ttu-id="3d876-158">Úroveň protokolu</span><span class="sxs-lookup"><span data-stu-id="3d876-158">Log level</span></span>

<span data-ttu-id="3d876-159">Pokaždé, když napíšete protokolu, zadejte jeho [LogLevel](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loglevel).</span><span class="sxs-lookup"><span data-stu-id="3d876-159">Each time you write a log, you specify its [LogLevel](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loglevel).</span></span> <span data-ttu-id="3d876-160">Úroveň protokolu označuje stupeň závažnosti nebo důležitost.</span><span class="sxs-lookup"><span data-stu-id="3d876-160">The log level indicates the degree of severity or importance.</span></span> <span data-ttu-id="3d876-161">Můžete například napsat `Information` protokolu při ukončení metody za normálních okolností `Warning` po návratu metody, návratový kód 404 a protokolu `Error` protokolu při catch neočekávanou výjimku.</span><span class="sxs-lookup"><span data-stu-id="3d876-161">For example, you might write an `Information` log when a method ends normally, a `Warning` log when a method returns a 404 return code, and an `Error` log when you catch an unexpected exception.</span></span>

<span data-ttu-id="3d876-162">V následujícím příkladu kódu, názvy metod (například `LogWarning`) zadejte úroveň protokolu.</span><span class="sxs-lookup"><span data-stu-id="3d876-162">In the following code example, the names of the methods (for example, `LogWarning`) specify the log level.</span></span> <span data-ttu-id="3d876-163">První parametr je [protokolu událost s ID](#log-event-id).</span><span class="sxs-lookup"><span data-stu-id="3d876-163">The first parameter is the [Log event ID](#log-event-id).</span></span> <span data-ttu-id="3d876-164">Druhý parametr je [Šablona zprávy](#log-message-template) se zástupnými symboly pro argument hodnoty poskytované zbývající parametry metody.</span><span class="sxs-lookup"><span data-stu-id="3d876-164">The second parameter is a [message template](#log-message-template) with placeholders for argument values provided by the remaining method parameters.</span></span> <span data-ttu-id="3d876-165">Parametry metody jsou podrobně popsány dále v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="3d876-165">The method parameters are explained in more detail later in this article.</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

<span data-ttu-id="3d876-166">Metody protokolu, které obsahují úroveň v název metody jsou [rozšiřující metody pro objektu ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loggerextensions).</span><span class="sxs-lookup"><span data-stu-id="3d876-166">Log methods that include the level in the method name are [extension methods for ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loggerextensions).</span></span> <span data-ttu-id="3d876-167">Na pozadí volat tyto metody `Log` metody, která přijímá `LogLevel` parametr.</span><span class="sxs-lookup"><span data-stu-id="3d876-167">Behind the scenes, these methods call a `Log` method that takes a `LogLevel` parameter.</span></span> <span data-ttu-id="3d876-168">Můžete volat `Log` metoda přímo spíše než jeden z těchto metod rozšíření, ale syntaxe je poměrně složitá.</span><span class="sxs-lookup"><span data-stu-id="3d876-168">You can call the `Log` method directly rather than one of these extension methods, but the syntax is relatively complicated.</span></span> <span data-ttu-id="3d876-169">Další informace najdete v tématu [objektu ILogger rozhraní](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) a [rozšíření protokolovače zdrojový kód](https://github.com/aspnet/Logging/blob/master/src/Microsoft.Extensions.Logging.Abstractions/LoggerExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="3d876-169">For more information, see the [ILogger interface](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) and the [logger extensions source code](https://github.com/aspnet/Logging/blob/master/src/Microsoft.Extensions.Logging.Abstractions/LoggerExtensions.cs).</span></span>

<span data-ttu-id="3d876-170">ASP.NET Core definuje následující [protokolu úrovně](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loglevel), seřazené zde z minimálně na nejvyšší závažnosti.</span><span class="sxs-lookup"><span data-stu-id="3d876-170">ASP.NET Core defines the following [log levels](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.loglevel), ordered here from least to highest severity.</span></span>

* <span data-ttu-id="3d876-171">Trasování = 0</span><span class="sxs-lookup"><span data-stu-id="3d876-171">Trace = 0</span></span>

  <span data-ttu-id="3d876-172">Pro informace, které je vhodné pouze pro vývojáře, ladění problém.</span><span class="sxs-lookup"><span data-stu-id="3d876-172">For information that is valuable only to a developer debugging an issue.</span></span> <span data-ttu-id="3d876-173">Tyto zprávy mohou obsahovat citlivé aplikaci data a nemělo by být povolené v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="3d876-173">These messages may contain sensitive application data and so should not be enabled in a production environment.</span></span> <span data-ttu-id="3d876-174">*Zakázané ve výchozím nastavení.*</span><span class="sxs-lookup"><span data-stu-id="3d876-174">*Disabled by default.*</span></span> <span data-ttu-id="3d876-175">Příklad:`Credentials: {"User":"someuser", "Password":"P@ssword"}`</span><span class="sxs-lookup"><span data-stu-id="3d876-175">Example: `Credentials: {"User":"someuser", "Password":"P@ssword"}`</span></span>

* <span data-ttu-id="3d876-176">Debug = 1</span><span class="sxs-lookup"><span data-stu-id="3d876-176">Debug = 1</span></span>

  <span data-ttu-id="3d876-177">Informace, která má krátkodobou užitečnost při vývoji a ladění.</span><span class="sxs-lookup"><span data-stu-id="3d876-177">For information that has short-term usefulness during development and debugging.</span></span> <span data-ttu-id="3d876-178">Příklad: `Entering method Configure with flag set to true.` obvykle nebude povolit `Debug` úroveň protokolů v produkčním prostředí, pokud řešíte, kvůli velkému počtu protokoly.</span><span class="sxs-lookup"><span data-stu-id="3d876-178">Example: `Entering method Configure with flag set to true.` You typically would not enable `Debug` level logs in production unless you are troubleshooting, due to the high volume of logs.</span></span>

* <span data-ttu-id="3d876-179">Informace o = 2</span><span class="sxs-lookup"><span data-stu-id="3d876-179">Information = 2</span></span>

  <span data-ttu-id="3d876-180">Pro sledování obecný tok aplikace.</span><span class="sxs-lookup"><span data-stu-id="3d876-180">For tracking the general flow of the application.</span></span> <span data-ttu-id="3d876-181">Tyto protokoly obvykle mají některé dlouhodobé hodnoty.</span><span class="sxs-lookup"><span data-stu-id="3d876-181">These logs typically have some long-term value.</span></span> <span data-ttu-id="3d876-182">Příklad:`Request received for path /api/todo`</span><span class="sxs-lookup"><span data-stu-id="3d876-182">Example: `Request received for path /api/todo`</span></span>

* <span data-ttu-id="3d876-183">Upozornění = 3</span><span class="sxs-lookup"><span data-stu-id="3d876-183">Warning = 3</span></span>

  <span data-ttu-id="3d876-184">Nestandardní nebo neočekávané události v toku aplikací.</span><span class="sxs-lookup"><span data-stu-id="3d876-184">For abnormal or unexpected events in the application flow.</span></span> <span data-ttu-id="3d876-185">Ty mohou obsahovat chyby nebo jinými podmínkami, který nezpůsobí zastavení aplikace, ale které může potřebovat nutné prozkoumat.</span><span class="sxs-lookup"><span data-stu-id="3d876-185">These may include errors or other conditions that do not cause the application to stop, but which may need to be investigated.</span></span> <span data-ttu-id="3d876-186">Zpracovávaný výjimky jsou obvyklé místo pro použití `Warning` úrovně protokolování.</span><span class="sxs-lookup"><span data-stu-id="3d876-186">Handled exceptions are a common place to use the `Warning` log level.</span></span> <span data-ttu-id="3d876-187">Příklad:`FileNotFoundException for file quotes.txt.`</span><span class="sxs-lookup"><span data-stu-id="3d876-187">Example: `FileNotFoundException for file quotes.txt.`</span></span>

* <span data-ttu-id="3d876-188">Chyba = 4</span><span class="sxs-lookup"><span data-stu-id="3d876-188">Error = 4</span></span>

  <span data-ttu-id="3d876-189">Chyby a výjimky, které nelze zpracovat.</span><span class="sxs-lookup"><span data-stu-id="3d876-189">For errors and exceptions that cannot be handled.</span></span> <span data-ttu-id="3d876-190">Tyto zprávy označují selhání v aktuální aktivita nebo operace (například aktuální požadavek HTTP), není chybu celou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="3d876-190">These messages indicate a failure in the current activity or operation (such as the current HTTP request), not an application-wide failure.</span></span> <span data-ttu-id="3d876-191">Příklad zprávy protokolu:`Cannot insert record due to duplicate key violation.`</span><span class="sxs-lookup"><span data-stu-id="3d876-191">Example log message: `Cannot insert record due to duplicate key violation.`</span></span>

* <span data-ttu-id="3d876-192">Kritické = 5</span><span class="sxs-lookup"><span data-stu-id="3d876-192">Critical = 5</span></span>

  <span data-ttu-id="3d876-193">K selhání, které vyžadují okamžitou pozornost.</span><span class="sxs-lookup"><span data-stu-id="3d876-193">For failures that require immediate attention.</span></span> <span data-ttu-id="3d876-194">Příklady: ztrátě dat., nedostatek místa na disku.</span><span class="sxs-lookup"><span data-stu-id="3d876-194">Examples: data loss scenarios, out of disk space.</span></span>

<span data-ttu-id="3d876-195">Úroveň protokolu můžete určit, kolik protokolu výstup zapsán do média konkrétní úložiště a které zobrazí okno.</span><span class="sxs-lookup"><span data-stu-id="3d876-195">You can use the log level to control how much log output is written to a particular storage medium or display window.</span></span> <span data-ttu-id="3d876-196">Například v produkčním prostředí můžete všechny protokoly `Information` úroveň a nižší přejít na úložiště dat svazek a všechny protokoly `Warning` úrovně a vyšší přejděte k úložišti dat hodnotu.</span><span class="sxs-lookup"><span data-stu-id="3d876-196">For example, in production you might want all logs of `Information` level and lower to go to a volume data store, and all logs of `Warning` level and higher to go to a value data store.</span></span> <span data-ttu-id="3d876-197">Během vývoje, může být obvykle odeslat protokoly `Warning` nebo vyšší závažnosti ke konzole.</span><span class="sxs-lookup"><span data-stu-id="3d876-197">During development, you might normally send logs of `Warning` or higher severity to the console.</span></span> <span data-ttu-id="3d876-198">Když potřebujete vyřešit, můžete přidat `Debug` úroveň.</span><span class="sxs-lookup"><span data-stu-id="3d876-198">Then when you need to troubleshoot, you can add `Debug` level.</span></span> <span data-ttu-id="3d876-199">[Filtrování protokolu](#log-filtering) později v tomto článku vysvětluje, jak řídit které protokolu úrovně zpracovává zprostředkovatele.</span><span class="sxs-lookup"><span data-stu-id="3d876-199">The [Log filtering](#log-filtering) section later in this article explains how to control which log levels a provider handles.</span></span>

<span data-ttu-id="3d876-200">Zapíše rozhraní ASP.NET Core `Debug` protokoly pro framework události na úrovni.</span><span class="sxs-lookup"><span data-stu-id="3d876-200">The ASP.NET Core framework writes `Debug` level logs for framework events.</span></span> <span data-ttu-id="3d876-201">Příklady protokolu dříve v tomto článku vyloučené protokoly níže `Information` úroveň, takže žádná `Debug` úrovně protokoly byly vidět.</span><span class="sxs-lookup"><span data-stu-id="3d876-201">The log examples earlier in this article excluded logs below `Information` level, so no `Debug` level logs were shown.</span></span> <span data-ttu-id="3d876-202">Tady je příklad protokoly konzoly, pokud spustíte ukázkovou aplikaci nakonfigurovat tak, aby zobrazit `Debug` a vyšší protokoly pro zprostředkovatele konzoly.</span><span class="sxs-lookup"><span data-stu-id="3d876-202">Here's an example of console logs if you run the sample application configured to show `Debug` and higher logs for the console provider.</span></span>

```console
info: Microsoft.AspNetCore.Hosting.Internal.WebHost[1]
      Request starting HTTP/1.1 GET http://localhost:62555/api/todo/0
dbug: Microsoft.AspNetCore.Routing.Tree.TreeRouter[1]
      Request successfully matched the route with name 'GetTodo' and template 'api/Todo/{id}'.
dbug: Microsoft.AspNetCore.Mvc.Internal.ActionSelector[2]
      Action 'TodoApi.Controllers.TodoController.Update (TodoApi)' with id '089d59b6-92ec-472d-b552-cc613dfd625d' did not match the constraint 'Microsoft.AspNetCore.Mvc.Internal.HttpMethodActionConstraint'
dbug: Microsoft.AspNetCore.Mvc.Internal.ActionSelector[2]
      Action 'TodoApi.Controllers.TodoController.Delete (TodoApi)' with id 'f3476abe-4bd9-4ad3-9261-3ead09607366' did not match the constraint 'Microsoft.AspNetCore.Mvc.Internal.HttpMethodActionConstraint'
dbug: Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker[1]
      Executing action TodoApi.Controllers.TodoController.GetById (TodoApi)
info: Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker[1]
      Executing action method TodoApi.Controllers.TodoController.GetById (TodoApi) with arguments (0) - ModelState is Valid
info: TodoApi.Controllers.TodoController[1002]
      Getting item 0
warn: TodoApi.Controllers.TodoController[4000]
      GetById(0) NOT FOUND
dbug: Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker[2]
      Executed action method TodoApi.Controllers.TodoController.GetById (TodoApi), returned result Microsoft.AspNetCore.Mvc.NotFoundResult.
info: Microsoft.AspNetCore.Mvc.StatusCodeResult[1]
      Executing HttpStatusCodeResult, setting HTTP status code 404
info: Microsoft.AspNetCore.Mvc.Internal.ControllerActionInvoker[2]
      Executed action TodoApi.Controllers.TodoController.GetById (TodoApi) in 0.8788ms
dbug: Microsoft.AspNetCore.Server.Kestrel[9]
      Connection id "0HL6L7NEFF2QD" completed keep alive response.
info: Microsoft.AspNetCore.Hosting.Internal.WebHost[2]
      Request finished in 2.7286ms 404
```

## <a name="log-event-id"></a><span data-ttu-id="3d876-203">ID události protokolu</span><span class="sxs-lookup"><span data-stu-id="3d876-203">Log event ID</span></span>

<span data-ttu-id="3d876-204">Pokaždé, když napíšete protokolu, můžete zadat *ID události*.</span><span class="sxs-lookup"><span data-stu-id="3d876-204">Each time you write a log, you can specify an *event ID*.</span></span> <span data-ttu-id="3d876-205">Ukázková aplikace k tomu pomocí místně definované `LoggingEvents` třídy:</span><span class="sxs-lookup"><span data-stu-id="3d876-205">The sample app does this by using a locally-defined `LoggingEvents` class:</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

[!code-csharp[](index/sample//Core/LoggingEvents.cs?name=snippet_LoggingEvents)]

<span data-ttu-id="3d876-206">ID události je celočíselná hodnota, která můžete přidružit jednu na druhou sadu protokolované události.</span><span class="sxs-lookup"><span data-stu-id="3d876-206">An event ID is an integer value that you can use to associate a set of logged events with one another.</span></span> <span data-ttu-id="3d876-207">Například protokolu pro přidání položky do nákupního košíku může být událost ID 1000 a protokolu pro dokončení nákupu může být událost ID 1001.</span><span class="sxs-lookup"><span data-stu-id="3d876-207">For instance, a log for adding an item to a shopping cart could be event ID 1000 and a log for completing a purchase could be event ID 1001.</span></span>

<span data-ttu-id="3d876-208">Ve výstupu protokolování může uložené v poli ID události nebo součástí textové zprávy, v závislosti na zprostředkovateli.</span><span class="sxs-lookup"><span data-stu-id="3d876-208">In logging output, the event ID may be stored in a field or included in the text message, depending on the provider.</span></span> <span data-ttu-id="3d876-209">Ladění zprostředkovatele nezobrazí ID událostí, ale konzola poskytovatel je zobrazuje v závorkách za kategorií:</span><span class="sxs-lookup"><span data-stu-id="3d876-209">The Debug provider doesn't show event IDs, but the console provider shows them in brackets after the category:</span></span>

```console
info: TodoApi.Controllers.TodoController[1002]
      Getting item invalidid
warn: TodoApi.Controllers.TodoController[4000]
      GetById(invalidid) NOT FOUND
```

## <a name="log-message-template"></a><span data-ttu-id="3d876-210">Šablona zpráv protokolu</span><span class="sxs-lookup"><span data-stu-id="3d876-210">Log message template</span></span>

<span data-ttu-id="3d876-211">Pokaždé, když napíšete zprávu protokolu poskytnete Šablona zprávy.</span><span class="sxs-lookup"><span data-stu-id="3d876-211">Each time you write a log message, you provide a message template.</span></span> <span data-ttu-id="3d876-212">Šablona zprávy může být řetězec, nebo může obsahovat pojmenované zástupné symboly, do které argument hodnoty budou vloženy.</span><span class="sxs-lookup"><span data-stu-id="3d876-212">The message template can be a string or it can contain named placeholders into which argument values are placed.</span></span> <span data-ttu-id="3d876-213">Šablony není řetězec formátu, a zástupné symboly by měla mít název, není číslované.</span><span class="sxs-lookup"><span data-stu-id="3d876-213">The template isn't a format string, and placeholders should be named, not numbered.</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_CallLogMethods&highlight=3,7)]

<span data-ttu-id="3d876-214">Pořadí zástupných symbolů, není jejich názvy, určuje, které parametry slouží k zadání jejich hodnot.</span><span class="sxs-lookup"><span data-stu-id="3d876-214">The order of placeholders, not their names, determines which parameters are used to provide their values.</span></span> <span data-ttu-id="3d876-215">Pokud máte následující kód:</span><span class="sxs-lookup"><span data-stu-id="3d876-215">If you have the following code:</span></span>

```csharp
string p1 = "parm1";
string p2 = "parm2";
_logger.LogInformation("Parameter values: {p2}, {p1}", p1, p2);
```

<span data-ttu-id="3d876-216">Výsledný zprávy protokolu vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="3d876-216">The resulting log message looks like this:</span></span>

```
Parameter values: parm1, parm2
```

<span data-ttu-id="3d876-217">Rozhraní protokolování zpráv formátování tímto způsobem, aby bylo možné pro protokolování zprostředkovatele implementovat [sémantické protokolování, také známé jako strukturovaný protokolování](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).</span><span class="sxs-lookup"><span data-stu-id="3d876-217">The logging framework does message formatting in this way to make it possible for logging providers to implement [semantic logging, also known as structured logging](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).</span></span> <span data-ttu-id="3d876-218">Protože jsou argumenty sami předat protokolování systému, ne jenom šablony formátovaná zpráva zprostředkovatelé protokolování může ukládat hodnoty parametru jako pole kromě Šablona zprávy.</span><span class="sxs-lookup"><span data-stu-id="3d876-218">Because the arguments themselves are passed to the logging system, not just the formatted message template, logging providers can store the parameter values as fields in addition to the message template.</span></span> <span data-ttu-id="3d876-219">Pokud jste odkazovat protokolu výstup Azure Table Storage a volání metody protokolovacího nástroje vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="3d876-219">If you're directing your log output to Azure Table Storage and your logger method call looks like this:</span></span>

```csharp
_logger.LogInformation("Getting item {ID} at {RequestTime}", id, DateTime.Now);
```

<span data-ttu-id="3d876-220">Každá entita Azure Table může mít `ID` a `RequestTime` vlastnosti, které zjednodušuje dotazy na data protokolu.</span><span class="sxs-lookup"><span data-stu-id="3d876-220">Each Azure Table entity can have `ID` and `RequestTime` properties, which simplifies queries on log data.</span></span> <span data-ttu-id="3d876-221">Můžete najít všechny protokoly v rámci konkrétní `RequestTime` rozsah bez nutnosti analyzovat časový limit textové zprávy.</span><span class="sxs-lookup"><span data-stu-id="3d876-221">You can find all logs within a particular `RequestTime` range without the need to parse the time out of the text message.</span></span>

## <a name="logging-exceptions"></a><span data-ttu-id="3d876-222">Protokolování výjimky</span><span class="sxs-lookup"><span data-stu-id="3d876-222">Logging exceptions</span></span>

<span data-ttu-id="3d876-223">Metody protokolovacího nástroje, mají přetížení, které umožňují předat výjimku, jako v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="3d876-223">The logger methods have overloads that let you pass in an exception, as in the following example:</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_LogException&highlight=3)]

<span data-ttu-id="3d876-224">Různé zprostředkovatele zpracovat informace o výjimce různými způsoby.</span><span class="sxs-lookup"><span data-stu-id="3d876-224">Different providers handle the exception information in different ways.</span></span> <span data-ttu-id="3d876-225">Tady je příklad výstupu ladění zprostředkovatele z výše uvedeném kódu.</span><span class="sxs-lookup"><span data-stu-id="3d876-225">Here's an example of Debug provider output from the code shown above.</span></span>

```
TodoApi.Controllers.TodoController:Warning: GetById(036dd898-fb01-47e8-9a65-f92eb73cf924) NOT FOUND

System.Exception: Item not found exception.
 at TodoApi.Controllers.TodoController.GetById(String id) in C:\logging\sample\src\TodoApi\Controllers\TodoController.cs:line 226
```

## <a name="log-filtering"></a><span data-ttu-id="3d876-226">Filtrování protokolu</span><span class="sxs-lookup"><span data-stu-id="3d876-226">Log filtering</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3d876-227">ASP.NET základní 2.x</span><span class="sxs-lookup"><span data-stu-id="3d876-227">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="3d876-228">Můžete zadat úroveň minimální protokolu pro konkrétního zprostředkovatele a kategorie nebo pro všechny poskytovatele nebo všechny kategorie.</span><span class="sxs-lookup"><span data-stu-id="3d876-228">You can specify a minimum log level for a specific provider and category or for all providers or all categories.</span></span> <span data-ttu-id="3d876-229">Žádné protokoly nižší než minimální úroveň nejsou předaný tohoto zprostředkovatele, takže nemusíte získat nezobrazí nebo uložené.</span><span class="sxs-lookup"><span data-stu-id="3d876-229">Any logs below the minimum level aren't passed to that provider, so they don't get displayed or stored.</span></span> 

<span data-ttu-id="3d876-230">Pokud chcete potlačit všechny protokoly, můžete zadat `LogLevel.None` jako úroveň minimální protokolu.</span><span class="sxs-lookup"><span data-stu-id="3d876-230">If you want to suppress all logs, you can specify `LogLevel.None` as the minimum log level.</span></span> <span data-ttu-id="3d876-231">Celočíselnou hodnotu `LogLevel.None` je 6, která je vyšší než `LogLevel.Critical` (5).</span><span class="sxs-lookup"><span data-stu-id="3d876-231">The integer value of `LogLevel.None` is 6, which is higher than `LogLevel.Critical` (5).</span></span>

<span data-ttu-id="3d876-232">**Vytvoření pravidla filtru v konfiguraci**</span><span class="sxs-lookup"><span data-stu-id="3d876-232">**Create filter rules in configuration**</span></span>

<span data-ttu-id="3d876-233">Šablony projektů vytvořit kód, který volá `CreateDefaultBuilder` nastavení protokolování pro zprostředkovatele konzoly a ladění.</span><span class="sxs-lookup"><span data-stu-id="3d876-233">The project templates create code that calls `CreateDefaultBuilder` to set up logging for the Console and Debug providers.</span></span> <span data-ttu-id="3d876-234">`CreateDefaultBuilder` Metoda také nastaví protokolování tak, aby hledat konfiguraci v `Logging` části pomocí kódu takto:</span><span class="sxs-lookup"><span data-stu-id="3d876-234">The `CreateDefaultBuilder` method also sets up logging to look for configuration in a `Logging` section, using code like the following:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_ExpandDefault&highlight=15)]

<span data-ttu-id="3d876-235">Konfigurační data Určuje minimální protokolu úrovně zprostředkovatele a kategorie, jako v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="3d876-235">The configuration data specifies minimum log levels by provider and category, as in the following example:</span></span>

[!code-json[](index/sample2/appsettings.json)]

<span data-ttu-id="3d876-236">Tento formát JSON vytvoří šesti pravidla filtru, jeden pro zprostředkovatele ladění, čtyři pro zprostředkovatele konzoly a ten, který se vztahuje na všechny poskytovatele.</span><span class="sxs-lookup"><span data-stu-id="3d876-236">This JSON creates six filter rules, one for the Debug provider, four for the Console provider, and one that applies to all providers.</span></span> <span data-ttu-id="3d876-237">Zobrazí se později jak právě jeden z těchto pravidel je zvolen pro každého zprostředkovatele při `ILogger` je vytvořen objekt.</span><span class="sxs-lookup"><span data-stu-id="3d876-237">You'll see later how just one of these rules is chosen for each provider when an `ILogger` object is created.</span></span>

<span data-ttu-id="3d876-238">**Pravidla filtru v kódu**</span><span class="sxs-lookup"><span data-stu-id="3d876-238">**Filter rules in code**</span></span>

<span data-ttu-id="3d876-239">V kódu, můžete zaregistrovat pravidla filtru, jak je znázorněno v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="3d876-239">You can register filter rules in code, as shown in the following example:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_FilterInCode&highlight=4-5)]

<span data-ttu-id="3d876-240">Druhý `AddFilter` Určuje zprostředkovatele, který ladění pomocí jeho názvu typu.</span><span class="sxs-lookup"><span data-stu-id="3d876-240">The second `AddFilter` specifies the Debug provider by using its type name.</span></span> <span data-ttu-id="3d876-241">První `AddFilter` platí pro všechny poskytovatele, protože neurčuje typ poskytovatele.</span><span class="sxs-lookup"><span data-stu-id="3d876-241">The first `AddFilter` applies to all providers because it doesn't specify a provider type.</span></span>

<span data-ttu-id="3d876-242">**Jak pravidla filtrování se použijí.**</span><span class="sxs-lookup"><span data-stu-id="3d876-242">**How filtering rules are applied**</span></span>

<span data-ttu-id="3d876-243">Konfigurační data a `AddFilter` uvedeném v předchozích ukázkách kódu vytvořit pravidla uvedené v následující tabulce.</span><span class="sxs-lookup"><span data-stu-id="3d876-243">The configuration data and the `AddFilter` code shown in the preceding examples create the rules shown in the following table.</span></span> <span data-ttu-id="3d876-244">Prvních šest pocházet z příklad konfigurace a poslední dva pocházet z příkladu kódu.</span><span class="sxs-lookup"><span data-stu-id="3d876-244">The first six come from the configuration example and the last two come from the code example.</span></span>

| <span data-ttu-id="3d876-245">Číslo</span><span class="sxs-lookup"><span data-stu-id="3d876-245">Number</span></span> | <span data-ttu-id="3d876-246">Zprostředkovatel</span><span class="sxs-lookup"><span data-stu-id="3d876-246">Provider</span></span>      | <span data-ttu-id="3d876-247">Kategorie, které začínají...</span><span class="sxs-lookup"><span data-stu-id="3d876-247">Categories that begin with ...</span></span>          | <span data-ttu-id="3d876-248">Úroveň minimální protokolu</span><span class="sxs-lookup"><span data-stu-id="3d876-248">Minimum log level</span></span> |
| :----: | ------------- | --------------------------------------- | ----------------- |
| <span data-ttu-id="3d876-249">1</span><span class="sxs-lookup"><span data-stu-id="3d876-249">1</span></span>      | <span data-ttu-id="3d876-250">Ladit</span><span class="sxs-lookup"><span data-stu-id="3d876-250">Debug</span></span>         | <span data-ttu-id="3d876-251">Všechny kategorie</span><span class="sxs-lookup"><span data-stu-id="3d876-251">All categories</span></span>                          | <span data-ttu-id="3d876-252">Informace o</span><span class="sxs-lookup"><span data-stu-id="3d876-252">Information</span></span>       |
| <span data-ttu-id="3d876-253">2</span><span class="sxs-lookup"><span data-stu-id="3d876-253">2</span></span>      | <span data-ttu-id="3d876-254">Konzola</span><span class="sxs-lookup"><span data-stu-id="3d876-254">Console</span></span>       | <span data-ttu-id="3d876-255">Microsoft.AspNetCore.Mvc.Razor.Internal</span><span class="sxs-lookup"><span data-stu-id="3d876-255">Microsoft.AspNetCore.Mvc.Razor.Internal</span></span> | <span data-ttu-id="3d876-256">Upozornění</span><span class="sxs-lookup"><span data-stu-id="3d876-256">Warning</span></span>           |
| <span data-ttu-id="3d876-257">3</span><span class="sxs-lookup"><span data-stu-id="3d876-257">3</span></span>      | <span data-ttu-id="3d876-258">Konzola</span><span class="sxs-lookup"><span data-stu-id="3d876-258">Console</span></span>       | <span data-ttu-id="3d876-259">Microsoft.AspNetCore.Mvc.Razor.Razor</span><span class="sxs-lookup"><span data-stu-id="3d876-259">Microsoft.AspNetCore.Mvc.Razor.Razor</span></span>    | <span data-ttu-id="3d876-260">Ladit</span><span class="sxs-lookup"><span data-stu-id="3d876-260">Debug</span></span>             |
| <span data-ttu-id="3d876-261">4</span><span class="sxs-lookup"><span data-stu-id="3d876-261">4</span></span>      | <span data-ttu-id="3d876-262">Konzola</span><span class="sxs-lookup"><span data-stu-id="3d876-262">Console</span></span>       | <span data-ttu-id="3d876-263">Microsoft.AspNetCore.Mvc.Razor</span><span class="sxs-lookup"><span data-stu-id="3d876-263">Microsoft.AspNetCore.Mvc.Razor</span></span>          | <span data-ttu-id="3d876-264">Chyba</span><span class="sxs-lookup"><span data-stu-id="3d876-264">Error</span></span>             |
| <span data-ttu-id="3d876-265">5</span><span class="sxs-lookup"><span data-stu-id="3d876-265">5</span></span>      | <span data-ttu-id="3d876-266">Konzola</span><span class="sxs-lookup"><span data-stu-id="3d876-266">Console</span></span>       | <span data-ttu-id="3d876-267">Všechny kategorie</span><span class="sxs-lookup"><span data-stu-id="3d876-267">All categories</span></span>                          | <span data-ttu-id="3d876-268">Informace o</span><span class="sxs-lookup"><span data-stu-id="3d876-268">Information</span></span>       |
| <span data-ttu-id="3d876-269">6</span><span class="sxs-lookup"><span data-stu-id="3d876-269">6</span></span>      | <span data-ttu-id="3d876-270">Všichni poskytovatelé</span><span class="sxs-lookup"><span data-stu-id="3d876-270">All providers</span></span> | <span data-ttu-id="3d876-271">Všechny kategorie</span><span class="sxs-lookup"><span data-stu-id="3d876-271">All categories</span></span>                          | <span data-ttu-id="3d876-272">Ladit</span><span class="sxs-lookup"><span data-stu-id="3d876-272">Debug</span></span>             |
| <span data-ttu-id="3d876-273">7</span><span class="sxs-lookup"><span data-stu-id="3d876-273">7</span></span>      | <span data-ttu-id="3d876-274">Všichni poskytovatelé</span><span class="sxs-lookup"><span data-stu-id="3d876-274">All providers</span></span> | <span data-ttu-id="3d876-275">Systém</span><span class="sxs-lookup"><span data-stu-id="3d876-275">System</span></span>                                  | <span data-ttu-id="3d876-276">Ladit</span><span class="sxs-lookup"><span data-stu-id="3d876-276">Debug</span></span>             |
| <span data-ttu-id="3d876-277">8</span><span class="sxs-lookup"><span data-stu-id="3d876-277">8</span></span>      | <span data-ttu-id="3d876-278">Ladit</span><span class="sxs-lookup"><span data-stu-id="3d876-278">Debug</span></span>         | <span data-ttu-id="3d876-279">Microsoft</span><span class="sxs-lookup"><span data-stu-id="3d876-279">Microsoft</span></span>                               | <span data-ttu-id="3d876-280">trasování</span><span class="sxs-lookup"><span data-stu-id="3d876-280">Trace</span></span>             |

<span data-ttu-id="3d876-281">Při vytváření `ILogger` objekt zápis protokolů, `ILoggerFactory` objekt vybere jedno pravidlo na zprostředkovatele pro použití tohoto protokolovacího nástroje.</span><span class="sxs-lookup"><span data-stu-id="3d876-281">When you create an `ILogger` object to write logs with, the `ILoggerFactory` object selects a single rule per provider to apply to that logger.</span></span> <span data-ttu-id="3d876-282">Všechny zprávy, které jsou napsané v tomto `ILogger` objekt jsou filtrovány podle vybraná pravidla.</span><span class="sxs-lookup"><span data-stu-id="3d876-282">All messages written by that `ILogger` object are filtered based on the selected rules.</span></span> <span data-ttu-id="3d876-283">Většina konkrétní pravidlo možné pro každou kategorii dvojice a zprostředkovatele se vybere z dostupná pravidla.</span><span class="sxs-lookup"><span data-stu-id="3d876-283">The most specific rule possible for each provider and category pair is selected from the available rules.</span></span>

<span data-ttu-id="3d876-284">Následující algoritmus se používá pro každého zprostředkovatele při `ILogger` se vytvoří pro danou kategorii:</span><span class="sxs-lookup"><span data-stu-id="3d876-284">The following algorithm is used for each provider when an `ILogger` is created for a given category:</span></span>

* <span data-ttu-id="3d876-285">Vyberte všechna pravidla, které odpovídají zprostředkovatel nebo jeho alias.</span><span class="sxs-lookup"><span data-stu-id="3d876-285">Select all rules that match the provider or its alias.</span></span> <span data-ttu-id="3d876-286">Pokud nejsou nalezeny, vyberte všechna pravidla s poskytovatele prázdný.</span><span class="sxs-lookup"><span data-stu-id="3d876-286">If none are found, select all rules with an empty provider.</span></span>
* <span data-ttu-id="3d876-287">Od výsledku v předchozím kroku vyberte pravidla s nejdéle odpovídající kategorii předponu.</span><span class="sxs-lookup"><span data-stu-id="3d876-287">From the result of the preceding step, select rules with longest matching category prefix.</span></span> <span data-ttu-id="3d876-288">Pokud nejsou nalezeny, vyberte všechna pravidla, které nechcete zadat kategorii.</span><span class="sxs-lookup"><span data-stu-id="3d876-288">If none are found, select all rules that don't specify a category.</span></span>
* <span data-ttu-id="3d876-289">Pokud je vybraných víc pravidel trvat **poslední** jeden.</span><span class="sxs-lookup"><span data-stu-id="3d876-289">If multiple rules are selected take the **last** one.</span></span>
* <span data-ttu-id="3d876-290">Pokud je vybrána žádná pravidla, použijte `MinimumLevel`.</span><span class="sxs-lookup"><span data-stu-id="3d876-290">If no rules are selected, use `MinimumLevel`.</span></span>
 
<span data-ttu-id="3d876-291">Předpokládejme například, máte předchozí seznam pravidel a vytvoříte `ILogger` objektu pro kategorii "Microsoft.AspNetCore.Mvc.Razor.RazorViewEngine":</span><span class="sxs-lookup"><span data-stu-id="3d876-291">For example, suppose you have the preceding list of rules and you create an `ILogger` object for category "Microsoft.AspNetCore.Mvc.Razor.RazorViewEngine":</span></span>

* <span data-ttu-id="3d876-292">Ladění zprostředkovatele platí pravidla 1, 6 a 8.</span><span class="sxs-lookup"><span data-stu-id="3d876-292">For the Debug provider, rules 1, 6, and 8 apply.</span></span> <span data-ttu-id="3d876-293">Pravidlo 8 je nejvíce konkrétní tak, aby se jeden vybrané.</span><span class="sxs-lookup"><span data-stu-id="3d876-293">Rule 8 is most specific, so that's the one selected.</span></span>
* <span data-ttu-id="3d876-294">Pro zprostředkovatele konzoly platí pravidla 3, 4, 5 a 6.</span><span class="sxs-lookup"><span data-stu-id="3d876-294">For the Console provider, rules 3, 4, 5, and 6 apply.</span></span> <span data-ttu-id="3d876-295">Pravidlo 3 je nejvíce.</span><span class="sxs-lookup"><span data-stu-id="3d876-295">Rule 3 is most specific.</span></span>

<span data-ttu-id="3d876-296">Při vytváření protokoly s `ILogger` pro kategorii "Microsoft.AspNetCore.Mvc.Razor.RazorViewEngine", protokoly z `Trace` úrovni a vyšší přejde na ladění zprostředkovatele a protokoly `Debug` úrovni a vyšší přejde k poskytovateli konzoly.</span><span class="sxs-lookup"><span data-stu-id="3d876-296">When you create logs with an `ILogger` for category "Microsoft.AspNetCore.Mvc.Razor.RazorViewEngine", logs of `Trace` level and above will go to the Debug provider, and logs of `Debug` level and above will go to the Console provider.</span></span>

<span data-ttu-id="3d876-297">**Aliasy zprostředkovatele**</span><span class="sxs-lookup"><span data-stu-id="3d876-297">**Provider aliases**</span></span>

<span data-ttu-id="3d876-298">Název typu můžete zadat poskytovatele v konfiguraci, ale každý poskytovatel definuje kratší *alias* , je jednodušší použít.</span><span class="sxs-lookup"><span data-stu-id="3d876-298">You can use the type name to specify a provider in configuration, but each provider defines a shorter *alias* that is easier to use.</span></span> <span data-ttu-id="3d876-299">Pro předdefinované zprostředkovatele použijte následující aliasy:</span><span class="sxs-lookup"><span data-stu-id="3d876-299">For the built-in providers, use the following aliases:</span></span>

- <span data-ttu-id="3d876-300">Konzola</span><span class="sxs-lookup"><span data-stu-id="3d876-300">Console</span></span>
- <span data-ttu-id="3d876-301">Ladit</span><span class="sxs-lookup"><span data-stu-id="3d876-301">Debug</span></span>
- <span data-ttu-id="3d876-302">Protokol událostí</span><span class="sxs-lookup"><span data-stu-id="3d876-302">EventLog</span></span>
- <span data-ttu-id="3d876-303">AzureAppServices</span><span class="sxs-lookup"><span data-stu-id="3d876-303">AzureAppServices</span></span>
- <span data-ttu-id="3d876-304">TraceSource</span><span class="sxs-lookup"><span data-stu-id="3d876-304">TraceSource</span></span>
- <span data-ttu-id="3d876-305">EventSource</span><span class="sxs-lookup"><span data-stu-id="3d876-305">EventSource</span></span>

<span data-ttu-id="3d876-306">**Výchozí minimální úroveň**</span><span class="sxs-lookup"><span data-stu-id="3d876-306">**Default minimum level**</span></span>

<span data-ttu-id="3d876-307">Není k dispozici minimální nastavení úrovně, který se uplatní pouze v případě, že žádná pravidla z konfigurace nebo kód platí pro daného zprostředkovatele a kategorie.</span><span class="sxs-lookup"><span data-stu-id="3d876-307">There is a minimum level setting that takes effect only if no rules from configuration or code apply for a given provider and category.</span></span> <span data-ttu-id="3d876-308">Následující příklad ukazuje, jak nastavit minimální úroveň:</span><span class="sxs-lookup"><span data-stu-id="3d876-308">The following example shows how to set the minimum level:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_MinLevel&highlight=3)]

<span data-ttu-id="3d876-309">Pokud není explicitně nastavit minimální úroveň, výchozí hodnota je `Information`, to znamená, že `Trace` a `Debug` protokoly jsou ignorovány.</span><span class="sxs-lookup"><span data-stu-id="3d876-309">If you don't explicitly set the minimum level, the default value is `Information`, which means that `Trace` and `Debug` logs are ignored.</span></span>

<span data-ttu-id="3d876-310">**Funkce filtru**</span><span class="sxs-lookup"><span data-stu-id="3d876-310">**Filter functions**</span></span>

<span data-ttu-id="3d876-311">Můžete napsat kód ve funkci filtru pro použití pravidel filtrování.</span><span class="sxs-lookup"><span data-stu-id="3d876-311">You can write code in a filter function to apply filtering rules.</span></span> <span data-ttu-id="3d876-312">Pro všechny zprostředkovatele a kategorie, které nemají přiřazenou konfigurace nebo kód pravidla je volána funkce filtru.</span><span class="sxs-lookup"><span data-stu-id="3d876-312">A filter function is invoked for all providers and categories that do not have rules assigned to them by configuration or code.</span></span> <span data-ttu-id="3d876-313">Kód ve funkci má přístup k typ zprostředkovatele, kategorie a úroveň protokolu se rozhodnout, zda mají být protokolovány zprávu.</span><span class="sxs-lookup"><span data-stu-id="3d876-313">Code in the function has access to the provider type, category, and log level to decide whether or not a message should be logged.</span></span> <span data-ttu-id="3d876-314">Příklad:</span><span class="sxs-lookup"><span data-stu-id="3d876-314">For example:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_FilterFunction&highlight=5-13)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3d876-315">ASP.NET základní 1.x</span><span class="sxs-lookup"><span data-stu-id="3d876-315">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="3d876-316">Někteří poskytovatelé protokolování umožňují určit, kdy by měla být protokoly na médium úložiště nebo ignorovat na základě úroveň protokolu a kategorie.</span><span class="sxs-lookup"><span data-stu-id="3d876-316">Some logging providers let you specify when logs should be written to a storage medium or ignored based on log level and category.</span></span>

<span data-ttu-id="3d876-317">`AddConsole` a `AddDebug` metody rozšíření poskytují přetížení, které umožňují předat kritéria filtrování.</span><span class="sxs-lookup"><span data-stu-id="3d876-317">The `AddConsole` and `AddDebug` extension methods provide overloads that let you pass in filtering criteria.</span></span> <span data-ttu-id="3d876-318">Následující vzorový kód způsobí, že konzola poskytovatel ignorovat protokoly níže `Warning` úroveň, při ladění zprostředkovatele ignoruje protokoly, které vytvoří rozhraní.</span><span class="sxs-lookup"><span data-stu-id="3d876-318">The following sample code causes the console provider to ignore logs below `Warning` level, while the Debug provider ignores logs that the framework creates.</span></span>

[!code-csharp[](index/sample/Startup.cs?name=snippet_AddConsoleAndDebugWithFilter&highlight=6-7)]

<span data-ttu-id="3d876-319">`AddEventLog` Metoda má přetížení, které přijímá `EventLogSettings` instanci, která může obsahovat filtrování funkce v jeho `Filter` vlastnost.</span><span class="sxs-lookup"><span data-stu-id="3d876-319">The `AddEventLog` method has an overload that takes an `EventLogSettings` instance, which may contain a filtering function in its `Filter` property.</span></span> <span data-ttu-id="3d876-320">Zprostředkovatel TraceSource neposkytuje žádné z těchto přetížení vzhledem k tomu, že jsou na základě jeho úroveň protokolování a dalších parametrů `SourceSwitch` a `TraceListener` používá.</span><span class="sxs-lookup"><span data-stu-id="3d876-320">The TraceSource provider does not provide any of those overloads, since its logging level and other parameters are based on the `SourceSwitch` and `TraceListener` it uses.</span></span>

<span data-ttu-id="3d876-321">Můžete nastavit pravidla filtrování pro všechny poskytovatele, které jsou registrovány `ILoggerFactory` instance pomocí `WithFilter` metoda rozšíření.</span><span class="sxs-lookup"><span data-stu-id="3d876-321">You can set filtering rules for all providers that are registered with an `ILoggerFactory` instance by using the `WithFilter` extension method.</span></span> <span data-ttu-id="3d876-322">Následující příklad omezuje protokoly framework (kategorie začíná "Microsoft" nebo "Systém") a upozornění při upozornění v protokolu aplikace na úrovni ladění.</span><span class="sxs-lookup"><span data-stu-id="3d876-322">The example below limits framework logs (category begins with "Microsoft" or "System") to warnings while letting the app log at debug level.</span></span>

[!code-csharp[](index/sample/Startup.cs?name=snippet_FactoryFilter&highlight=6-11)]

<span data-ttu-id="3d876-323">Pokud chcete zabránit zápisu pro danou kategorii všechny protokoly pomocí filtrování, můžete zadat `LogLevel.None` jako úroveň minimální protokolu této kategorie.</span><span class="sxs-lookup"><span data-stu-id="3d876-323">If you want to use filtering to prevent all logs from being written for a particular category, you can specify `LogLevel.None` as the minimum log level for that category.</span></span> <span data-ttu-id="3d876-324">Celočíselnou hodnotu `LogLevel.None` je 6, která je vyšší než `LogLevel.Critical` (5).</span><span class="sxs-lookup"><span data-stu-id="3d876-324">The integer value of `LogLevel.None` is 6, which is higher than `LogLevel.Critical` (5).</span></span>

<span data-ttu-id="3d876-325">`WithFilter` Rozšíření metoda je poskytována [Microsoft.Extensions.Logging.Filter](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Filter) balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="3d876-325">The `WithFilter` extension method is provided by the [Microsoft.Extensions.Logging.Filter](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Filter) NuGet package.</span></span> <span data-ttu-id="3d876-326">Metoda vrátí novou `ILoggerFactory` instance, která bude filtrovat zprávy protokolu předaný všechny protokoly poskytovatele registrované s ním.</span><span class="sxs-lookup"><span data-stu-id="3d876-326">The method returns a new `ILoggerFactory` instance that will filter the log messages passed to all logger providers registered with it.</span></span> <span data-ttu-id="3d876-327">Nemá vliv na žádné jiné `ILoggerFactory` instance, včetně původní `ILoggerFactory` instance.</span><span class="sxs-lookup"><span data-stu-id="3d876-327">It does not affect any other `ILoggerFactory` instances, including the original `ILoggerFactory` instance.</span></span>

---

## <a name="log-scopes"></a><span data-ttu-id="3d876-328">Obory protokolu</span><span class="sxs-lookup"><span data-stu-id="3d876-328">Log scopes</span></span>

<span data-ttu-id="3d876-329">Můžete seskupit sadu logické operace v rámci *oboru* Chcete-li přiřadit každý protokol, který je vytvořen jako součást této sady stejná data.</span><span class="sxs-lookup"><span data-stu-id="3d876-329">You can group a set of logical operations within a *scope* in order to attach the same data to each log that is created as part of that set.</span></span> <span data-ttu-id="3d876-330">Například můžete každý protokol vytvořené jako součást zpracování transakci zahrnují ID transakce.</span><span class="sxs-lookup"><span data-stu-id="3d876-330">For example, you might want every log created as part of processing a transaction to include the transaction ID.</span></span>

<span data-ttu-id="3d876-331">Obor je `IDisposable` typ, který je vrácený `ILogger.BeginScope<TState>` metoda a bude trvat, dokud je zrušen.</span><span class="sxs-lookup"><span data-stu-id="3d876-331">A scope is an `IDisposable` type that is returned by the `ILogger.BeginScope<TState>` method and lasts until it is disposed.</span></span> <span data-ttu-id="3d876-332">Použít obor podle zabalení vaše protokoly volání metod `using` blokovat, jak je vidět tady:</span><span class="sxs-lookup"><span data-stu-id="3d876-332">You use a scope by wrapping your logger calls in a `using` block, as shown here:</span></span>

[!code-csharp[](index/sample//Controllers/TodoController.cs?name=snippet_Scopes&highlight=4-5,13)]

<span data-ttu-id="3d876-333">Následující kód umožňuje obory pro zprostředkovatele konzoly:</span><span class="sxs-lookup"><span data-stu-id="3d876-333">The following code enables scopes for the console provider:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3d876-334">ASP.NET základní 2.x</span><span class="sxs-lookup"><span data-stu-id="3d876-334">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="3d876-335">V *Program.cs*:</span><span class="sxs-lookup"><span data-stu-id="3d876-335">In *Program.cs*:</span></span>

[!code-csharp[](index/sample2/Program.cs?name=snippet_Scopes&highlight=4)]

> [!NOTE]
> <span data-ttu-id="3d876-336">Konfigurace `IncludeScopes` možnost protokolovacího nástroje Konzola je potřeba povolit protokolování obor.</span><span class="sxs-lookup"><span data-stu-id="3d876-336">Configuring the `IncludeScopes` console logger option is required to enable scope-based logging.</span></span> <span data-ttu-id="3d876-337">Konfigurace `IncludeScopes` pomocí *appsettings* konfigurační soubory bude k dispozici ve verzi ASP.NET Core 2.1.</span><span class="sxs-lookup"><span data-stu-id="3d876-337">Configuration of `IncludeScopes` using *appsettings* configuration files will be available with the release of ASP.NET Core 2.1.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3d876-338">ASP.NET základní 1.x</span><span class="sxs-lookup"><span data-stu-id="3d876-338">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="3d876-339">V *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="3d876-339">In *Startup.cs*:</span></span>

[!code-csharp[](index/sample/Startup.cs?name=snippet_Scopes&highlight=6)]

---

<span data-ttu-id="3d876-340">Každé zprávě protokolu obsahuje informace o oboru:</span><span class="sxs-lookup"><span data-stu-id="3d876-340">Each log message includes the scoped information:</span></span>

```
info: TodoApi.Controllers.TodoController[1002]
      => RequestId:0HKV9C49II9CK RequestPath:/api/todo/0 => TodoApi.Controllers.TodoController.GetById (TodoApi) => Message attached to logs created in the using block
      Getting item 0
warn: TodoApi.Controllers.TodoController[4000]
      => RequestId:0HKV9C49II9CK RequestPath:/api/todo/0 => TodoApi.Controllers.TodoController.GetById (TodoApi) => Message attached to logs created in the using block
      GetById(0) NOT FOUND
```

## <a name="built-in-logging-providers"></a><span data-ttu-id="3d876-341">Zprostředkovatelé integrované protokolování</span><span class="sxs-lookup"><span data-stu-id="3d876-341">Built-in logging providers</span></span>

<span data-ttu-id="3d876-342">ASP.NET Core dodává tyto zprostředkovatele:</span><span class="sxs-lookup"><span data-stu-id="3d876-342">ASP.NET Core ships the following providers:</span></span>

* [<span data-ttu-id="3d876-343">Console</span><span class="sxs-lookup"><span data-stu-id="3d876-343">Console</span></span>](#console)
* [<span data-ttu-id="3d876-344">Ladění</span><span class="sxs-lookup"><span data-stu-id="3d876-344">Debug</span></span>](#debug)
* [<span data-ttu-id="3d876-345">EventSource</span><span class="sxs-lookup"><span data-stu-id="3d876-345">EventSource</span></span>](#eventsource)
* [<span data-ttu-id="3d876-346">EventLog</span><span class="sxs-lookup"><span data-stu-id="3d876-346">EventLog</span></span>](#eventlog)
* [<span data-ttu-id="3d876-347">TraceSource</span><span class="sxs-lookup"><span data-stu-id="3d876-347">TraceSource</span></span>](#tracesource)
* [<span data-ttu-id="3d876-348">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3d876-348">Azure App Service</span></span>](#appservice)

<a id="console"></a>
### <a name="the-console-provider"></a><span data-ttu-id="3d876-349">Zprostředkovatel konzoly</span><span class="sxs-lookup"><span data-stu-id="3d876-349">The console provider</span></span>

<span data-ttu-id="3d876-350">[Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console) balíček zprostředkovatele odesílá výstup protokolu ke konzole.</span><span class="sxs-lookup"><span data-stu-id="3d876-350">The [Microsoft.Extensions.Logging.Console](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Console) provider package sends log output to the console.</span></span> 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3d876-351">ASP.NET základní 2.x</span><span class="sxs-lookup"><span data-stu-id="3d876-351">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
logging.AddConsole()
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3d876-352">ASP.NET základní 1.x</span><span class="sxs-lookup"><span data-stu-id="3d876-352">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
loggerFactory.AddConsole()
```

<span data-ttu-id="3d876-353">[Přetížení AddConsole](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.consoleloggerextensions) umožňují předáte v úroveň minimální protokolu, funkce filtru a logická hodnota, která označuje, zda obory.</span><span class="sxs-lookup"><span data-stu-id="3d876-353">[AddConsole overloads](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.consoleloggerextensions) let you pass in an a minimum log level, a filter function, and a boolean that indicates whether scopes are supported.</span></span> <span data-ttu-id="3d876-354">Další možností je předat `IConfiguration` objektu, který můžete určit podporu obory a úrovně protokolování.</span><span class="sxs-lookup"><span data-stu-id="3d876-354">Another option is to pass in an `IConfiguration` object, which can specify scopes support and logging levels.</span></span> 

<span data-ttu-id="3d876-355">Pokud uvažujete o poskytovateli konzoly pro použití v produkčním prostředí, mějte na paměti, že má významný dopad na výkon.</span><span class="sxs-lookup"><span data-stu-id="3d876-355">If you are considering the console provider for use in production, be aware that it has a significant impact on performance.</span></span>

<span data-ttu-id="3d876-356">Když vytvoříte nový projekt v sadě Visual Studio `AddConsole` metoda vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="3d876-356">When you create a new project in Visual Studio, the `AddConsole` method looks like this:</span></span>

```csharp
loggerFactory.AddConsole(Configuration.GetSection("Logging"));
```

<span data-ttu-id="3d876-357">Tento kód odkazuje `Logging` části *appSettings.JSON určený* souboru:</span><span class="sxs-lookup"><span data-stu-id="3d876-357">This code refers to the `Logging` section of the *appSettings.json* file:</span></span>

[!code-json[](index/sample//appsettings.json)]

<span data-ttu-id="3d876-358">Nastavení při povolení aplikace zobrazí protokoly framework limit upozornění k protokolování na úrovni ladění, jak je popsáno v [filtrování protokolu](#log-filtering) části.</span><span class="sxs-lookup"><span data-stu-id="3d876-358">The settings shown limit framework logs to warnings while allowing the app to log at debug level, as explained in the [Log filtering](#log-filtering) section.</span></span> <span data-ttu-id="3d876-359">Další informace najdete v tématu [konfigurace](xref:fundamentals/configuration/index).</span><span class="sxs-lookup"><span data-stu-id="3d876-359">For more information, see [Configuration](xref:fundamentals/configuration/index).</span></span>

---

<a id="debug"></a>
### <a name="the-debug-provider"></a><span data-ttu-id="3d876-360">Ladění zprostředkovatele</span><span class="sxs-lookup"><span data-stu-id="3d876-360">The Debug provider</span></span>

<span data-ttu-id="3d876-361">[Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug) balíček zprostředkovatele zapíše výstup protokolu pomocí [System.Diagnostics.Debug](https://docs.microsoft.com/dotnet/core/api/system.diagnostics.debug#System_Diagnostics_Debug) – třída (`Debug.WriteLine` volání metod).</span><span class="sxs-lookup"><span data-stu-id="3d876-361">The [Microsoft.Extensions.Logging.Debug](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Debug) provider package writes log output by using the [System.Diagnostics.Debug](https://docs.microsoft.com/dotnet/core/api/system.diagnostics.debug#System_Diagnostics_Debug) class (`Debug.WriteLine` method calls).</span></span>

<span data-ttu-id="3d876-362">V systému Linux, tohoto zprostředkovatele zapisuje protokoly do */var/log/message*.</span><span class="sxs-lookup"><span data-stu-id="3d876-362">On Linux, this provider writes logs to */var/log/message*.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3d876-363">ASP.NET základní 2.x</span><span class="sxs-lookup"><span data-stu-id="3d876-363">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
logging.AddDebug()
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3d876-364">ASP.NET základní 1.x</span><span class="sxs-lookup"><span data-stu-id="3d876-364">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
loggerFactory.AddDebug()
```

<span data-ttu-id="3d876-365">[Přetížení AddDebug](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.debugloggerfactoryextensions) umožňují předáte v úroveň minimální protokolu nebo funkce filtru.</span><span class="sxs-lookup"><span data-stu-id="3d876-365">[AddDebug overloads](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.debugloggerfactoryextensions) let you pass in a minimum log level or a filter function.</span></span>

---

<a id="eventsource"></a>
### <a name="the-eventsource-provider"></a><span data-ttu-id="3d876-366">EventSource zprostředkovatele</span><span class="sxs-lookup"><span data-stu-id="3d876-366">The EventSource provider</span></span>

<span data-ttu-id="3d876-367">Pro aplikace, které cílí ASP.NET Core 1.1.0 nebo vyšší, [Microsoft.Extensions.Logging.EventSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventSource) balíček zprostředkovatele můžete implementovat trasování událostí.</span><span class="sxs-lookup"><span data-stu-id="3d876-367">For apps that target ASP.NET Core 1.1.0 or higher, the [Microsoft.Extensions.Logging.EventSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventSource) provider package can implement event tracing.</span></span> <span data-ttu-id="3d876-368">V systému Windows, používá [ETW](https://msdn.microsoft.com/library/windows/desktop/bb968803).</span><span class="sxs-lookup"><span data-stu-id="3d876-368">On Windows, it uses [ETW](https://msdn.microsoft.com/library/windows/desktop/bb968803).</span></span> <span data-ttu-id="3d876-369">Zprostředkovatel je platformy, ale nejsou žádná událost shromažďování a zobrazení nástroje pro Linux nebo systému macOS ještě.</span><span class="sxs-lookup"><span data-stu-id="3d876-369">The provider is cross-platform, but there are no event collection and display tools yet for Linux or macOS.</span></span> 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3d876-370">ASP.NET základní 2.x</span><span class="sxs-lookup"><span data-stu-id="3d876-370">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
logging.AddEventSourceLogger()
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3d876-371">ASP.NET základní 1.x</span><span class="sxs-lookup"><span data-stu-id="3d876-371">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
loggerFactory.AddEventSourceLogger()
```

---

<span data-ttu-id="3d876-372">Dobrým způsobem, jak shromáždit a zobrazit protokoly se má používat [nástroje PerfView nástroj](https://www.microsoft.com/download/details.aspx?id=28567).</span><span class="sxs-lookup"><span data-stu-id="3d876-372">A good way to collect and view logs is to use the [PerfView utility](https://www.microsoft.com/download/details.aspx?id=28567).</span></span> <span data-ttu-id="3d876-373">Existují další nástroje pro prohlížení protokolů trasování událostí pro Windows, ale nástroje PerfView přináší nejlepší výsledky pro práci s události ETW vygenerované pomocí technologie ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3d876-373">There are other tools for viewing ETW logs, but PerfView provides the best experience for working with the ETW events emitted by ASP.NET.</span></span> 

<span data-ttu-id="3d876-374">Konfigurace nástroje PerfView pro shromažďování události zapsané podle tohoto zprostředkovatele, přidejte řetězec `*Microsoft-Extensions-Logging` k **další poskytovatele** seznamu.</span><span class="sxs-lookup"><span data-stu-id="3d876-374">To configure PerfView for collecting events logged by this provider, add the string `*Microsoft-Extensions-Logging` to the **Additional Providers** list.</span></span> <span data-ttu-id="3d876-375">(Nezapomeňte si projít hvězdičky na začátku řetězce.)</span><span class="sxs-lookup"><span data-stu-id="3d876-375">(Don't miss the asterisk at the start of the string.)</span></span>

![Další poskytovatele nástroje Perfview](index/_static/perfview-additional-providers.png)

<span data-ttu-id="3d876-377">Zachycení událostí na Nano Server vyžaduje některé další nastavení:</span><span class="sxs-lookup"><span data-stu-id="3d876-377">Capturing events on Nano Server requires some additional setup:</span></span>

* <span data-ttu-id="3d876-378">Připojení k serveru Nano vzdálenou komunikaci prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3d876-378">Connect PowerShell remoting to the Nano Server:</span></span>

  ```powershell
  Enter-PSSession [name]
  ```

* <span data-ttu-id="3d876-379">Vytvoření relace trasování událostí pro Windows:</span><span class="sxs-lookup"><span data-stu-id="3d876-379">Create an ETW session:</span></span>

  ```powershell
  New-EtwTraceSession -Name "MyAppTrace" -LocalFilePath C:\trace.etl
  ```

* <span data-ttu-id="3d876-380">Přidat zprostředkovatele trasování událostí pro Windows pro [CLR](https://docs.microsoft.com/dotnet/framework/performance/clr-etw-providers), ASP.NET Core a dalších podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="3d876-380">Add ETW providers for [CLR](https://docs.microsoft.com/dotnet/framework/performance/clr-etw-providers), ASP.NET Core, and others as needed.</span></span> <span data-ttu-id="3d876-381">Zprostředkovatel ASP.NET Core GUID je `3ac73b97-af73-50e9-0822-5da4367920d0`.</span><span class="sxs-lookup"><span data-stu-id="3d876-381">The ASP.NET Core provider GUID is `3ac73b97-af73-50e9-0822-5da4367920d0`.</span></span> 

  ```powershell
  Add-EtwTraceProvider -Guid "{e13c0d23-ccbc-4e12-931b-d9cc2eee27e4}" -SessionName MyAppTrace
  Add-EtwTraceProvider -Guid "{3ac73b97-af73-50e9-0822-5da4367920d0}" -SessionName MyAppTrace
  ```

* <span data-ttu-id="3d876-382">Spuštění tohoto webu a provést libovolné akce chcete informace o trasování pro.</span><span class="sxs-lookup"><span data-stu-id="3d876-382">Run the site and do whatever actions you want tracing information for.</span></span>

* <span data-ttu-id="3d876-383">Ukončit relaci trasování, až budete hotoví:</span><span class="sxs-lookup"><span data-stu-id="3d876-383">Stop the tracing session when you're finished:</span></span>

  ```powershell
  Stop-EtwTraceSession -Name "MyAppTrace"
  ```

<span data-ttu-id="3d876-384">Výsledná *C:\trace.etl* soubor může být analyzována pomocí nástroje PerfView jako v jiných edicích systému Windows.</span><span class="sxs-lookup"><span data-stu-id="3d876-384">The resulting *C:\trace.etl* file can be analyzed with PerfView as on other editions of Windows.</span></span>

<a id="eventlog"></a>
### <a name="the-windows-eventlog-provider"></a><span data-ttu-id="3d876-385">Zprostředkovatel protokolu událostí systému Windows</span><span class="sxs-lookup"><span data-stu-id="3d876-385">The Windows EventLog provider</span></span>

<span data-ttu-id="3d876-386">[Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog) balíček zprostředkovatele odesílá výstup protokolu do protokolu událostí systému Windows.</span><span class="sxs-lookup"><span data-stu-id="3d876-386">The [Microsoft.Extensions.Logging.EventLog](https://www.nuget.org/packages/Microsoft.Extensions.Logging.EventLog) provider package sends log output to the Windows Event Log.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3d876-387">ASP.NET základní 2.x</span><span class="sxs-lookup"><span data-stu-id="3d876-387">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
logging.AddEventLog()
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3d876-388">ASP.NET základní 1.x</span><span class="sxs-lookup"><span data-stu-id="3d876-388">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
loggerFactory.AddEventLog()
```

<span data-ttu-id="3d876-389">[Přetížení AddEventLog](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.eventloggerfactoryextensions) umožňují předáte v `EventLogSettings` nebo úroveň minimální protokolu.</span><span class="sxs-lookup"><span data-stu-id="3d876-389">[AddEventLog overloads](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.eventloggerfactoryextensions) let you pass in `EventLogSettings` or a minimum log level.</span></span>

---

<a id="tracesource"></a>
### <a name="the-tracesource-provider"></a><span data-ttu-id="3d876-390">TraceSource zprostředkovatele</span><span class="sxs-lookup"><span data-stu-id="3d876-390">The TraceSource provider</span></span>

<span data-ttu-id="3d876-391">[Microsoft.Extensions.Logging.TraceSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.TraceSource) používá balíček zprostředkovatele [System.Diagnostics.TraceSource](https://docs.microsoft.com/dotnet/api/system.diagnostics.tracesource) knihovny a zprostředkovatele.</span><span class="sxs-lookup"><span data-stu-id="3d876-391">The [Microsoft.Extensions.Logging.TraceSource](https://www.nuget.org/packages/Microsoft.Extensions.Logging.TraceSource) provider package uses the [System.Diagnostics.TraceSource](https://docs.microsoft.com/dotnet/api/system.diagnostics.tracesource) libraries and providers.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3d876-392">ASP.NET základní 2.x</span><span class="sxs-lookup"><span data-stu-id="3d876-392">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
logging.AddTraceSource(sourceSwitchName);
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3d876-393">ASP.NET základní 1.x</span><span class="sxs-lookup"><span data-stu-id="3d876-393">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
loggerFactory.AddTraceSource(sourceSwitchName);
```

---

<span data-ttu-id="3d876-394">[Přetížení AddTraceSource](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.tracesourcefactoryextensions) umožňují předáte v přepínač zdroje a naslouchací proces trasování.</span><span class="sxs-lookup"><span data-stu-id="3d876-394">[AddTraceSource overloads](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.tracesourcefactoryextensions) let you pass in a source switch and a trace listener.</span></span>

<span data-ttu-id="3d876-395">Pro tohoto zprostředkovatele použijte aplikace má ke spuštění na rozhraní .NET Framework (nikoli .NET Core).</span><span class="sxs-lookup"><span data-stu-id="3d876-395">To use this provider, an application has to run on the .NET Framework (rather than .NET Core).</span></span> <span data-ttu-id="3d876-396">Umožňuje zprostředkovatele směrování zpráv do různých [naslouchací procesy](https://docs.microsoft.com/dotnet/framework/debug-trace-profile/trace-listeners), například [TextWriterTraceListener](https://docs.microsoft.com/dotnet/api/system.diagnostics.textwritertracelistenerr) použít v ukázkové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="3d876-396">The provider lets you route messages to a variety of [listeners](https://docs.microsoft.com/dotnet/framework/debug-trace-profile/trace-listeners), such as the [TextWriterTraceListener](https://docs.microsoft.com/dotnet/api/system.diagnostics.textwritertracelistenerr) used in the sample application.</span></span>

<span data-ttu-id="3d876-397">Následující příklad konfiguruje `TraceSource` zprostředkovatele, který protokoluje `Warning` a vyšší zprávy v okně konzoly.</span><span class="sxs-lookup"><span data-stu-id="3d876-397">The following example configures a `TraceSource` provider that logs `Warning` and higher messages to the console window.</span></span>

[!code-csharp[](index/sample/Startup.cs?name=snippet_TraceSource&highlight=9-12)]

<a id="appservice"></a>
### <a name="the-azure-app-service-provider"></a><span data-ttu-id="3d876-398">Zprostředkovatel služby Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3d876-398">The Azure App Service provider</span></span>

<span data-ttu-id="3d876-399">[Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices) balíček zprostředkovatele zapisuje protokoly do textových souborů v systému souborů aplikace služby Azure App Service a na [úložiště objektů blob](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/#what-is-blob-storage) v účtu Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3d876-399">The [Microsoft.Extensions.Logging.AzureAppServices](https://www.nuget.org/packages/Microsoft.Extensions.Logging.AzureAppServices) provider package writes logs to text files in an Azure App Service app's file system and to [blob storage](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/#what-is-blob-storage) in an Azure Storage account.</span></span> <span data-ttu-id="3d876-400">Zprostředkovatel je k dispozici pouze pro aplikace, které cílí ASP.NET Core 1.1.0 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="3d876-400">The provider is available only for apps that target ASP.NET Core 1.1.0 or higher.</span></span> 

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="3d876-401">ASP.NET základní 2.x</span><span class="sxs-lookup"><span data-stu-id="3d876-401">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="3d876-402">Pokud cílení na .NET Core, není nutné instalovat balíček zprostředkovatele nebo explicitně volání `AddAzureWebAppDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="3d876-402">If targeting .NET Core, you don't have to install the provider package or explicitly call `AddAzureWebAppDiagnostics`.</span></span> <span data-ttu-id="3d876-403">Zprostředkovatel je automaticky dostupný pro vaši aplikaci při nasazení aplikace do služby Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="3d876-403">The provider is automatically available to your app when you deploy the app to Azure App Service.</span></span>

<span data-ttu-id="3d876-404">Pokud cílení na rozhraní .NET Framework, do projektu přidejte balíček zprostředkovatele a vyvolání `AddAzureWebAppDiagnostics`:</span><span class="sxs-lookup"><span data-stu-id="3d876-404">If targeting .NET Framework, add the provider package to your project and invoke `AddAzureWebAppDiagnostics`:</span></span>

```csharp
logging.AddAzureWebAppDiagnostics();
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="3d876-405">ASP.NET základní 1.x</span><span class="sxs-lookup"><span data-stu-id="3d876-405">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
loggerFactory.AddAzureWebAppDiagnostics();
```

<span data-ttu-id="3d876-406">`AddAzureWebAppDiagnostics` Přetížení vám umožní předat v [AzureAppServicesDiagnosticsSettings](https://github.com/aspnet/Logging/blob/c7d0b1b88668ff4ef8a86ea7d2ebb5ca7f88d3e0/src/Microsoft.Extensions.Logging.AzureAppServices/AzureAppServicesDiagnosticsSettings.cs) se kterým můžete přepsat výchozí nastavení, jako je například protokolování výstupu šablony, název objektu blob a omezení velikosti souboru.</span><span class="sxs-lookup"><span data-stu-id="3d876-406">An `AddAzureWebAppDiagnostics` overload lets you pass in [AzureAppServicesDiagnosticsSettings](https://github.com/aspnet/Logging/blob/c7d0b1b88668ff4ef8a86ea7d2ebb5ca7f88d3e0/src/Microsoft.Extensions.Logging.AzureAppServices/AzureAppServicesDiagnosticsSettings.cs) with which you can override default settings such as the logging output template, blob name, and file size limit.</span></span> <span data-ttu-id="3d876-407">(*Výstup šablony* je šablona zprávy, který se použije pro všechny protokoly nad ten, který je zadat při volání `ILogger` metoda.)</span><span class="sxs-lookup"><span data-stu-id="3d876-407">(*Output template* is a message template that's applied to all logs on top of the one that you provide when you call an `ILogger` method.)</span></span>

---

<span data-ttu-id="3d876-408">Když nasazujete do aplikace služby App Service, vaše aplikace respektuje nastavení v [diagnostické protokoly](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/#enablediag) části **služby App Service** stránce portálu Azure.</span><span class="sxs-lookup"><span data-stu-id="3d876-408">When you deploy to an App Service app, your application honors the settings in the [Diagnostic Logs](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/#enablediag) section of the **App Service** page of the Azure portal.</span></span> <span data-ttu-id="3d876-409">Při změně těchto nastavení, změny se projeví okamžitě bez nutnosti restartovat aplikaci nebo znovu nasadit kódu do ní.</span><span class="sxs-lookup"><span data-stu-id="3d876-409">When you change those settings, the changes take effect immediately without requiring that you restart the app or redeploy code to it.</span></span> 

![Nastavení protokolování Azure](index/_static/azure-logging-settings.png)

<span data-ttu-id="3d876-411">Výchozí umístění pro soubory protokolu je v *D:\\domácí\\LogFiles\\aplikace* složku a výchozí název souboru je *diagnostiky yyyymmdd.txt*.</span><span class="sxs-lookup"><span data-stu-id="3d876-411">The default location for log files is in the *D:\\home\\LogFiles\\Application* folder, and the default file name is *diagnostics-yyyymmdd.txt*.</span></span> <span data-ttu-id="3d876-412">Výchozí limit velikosti souboru je 10 MB a výchozí maximální počet souborů, které uchovávají se 2.</span><span class="sxs-lookup"><span data-stu-id="3d876-412">The default file size limit is 10 MB, and the default maximum number of files retained is 2.</span></span> <span data-ttu-id="3d876-413">Výchozí název objektu blob je *{app-name}{timestamp}/yyyy/mm/dd/hh/{guid}-applicationLog.txt*.</span><span class="sxs-lookup"><span data-stu-id="3d876-413">The default blob name is *{app-name}{timestamp}/yyyy/mm/dd/hh/{guid}-applicationLog.txt*.</span></span> <span data-ttu-id="3d876-414">Další informace o výchozí chování najdete v tématu [AzureAppServicesDiagnosticsSettings](https://github.com/aspnet/Logging/blob/c7d0b1b88668ff4ef8a86ea7d2ebb5ca7f88d3e0/src/Microsoft.Extensions.Logging.AzureAppServices/AzureAppServicesDiagnosticsSettings.cs).</span><span class="sxs-lookup"><span data-stu-id="3d876-414">For more information about default behavior, see [AzureAppServicesDiagnosticsSettings](https://github.com/aspnet/Logging/blob/c7d0b1b88668ff4ef8a86ea7d2ebb5ca7f88d3e0/src/Microsoft.Extensions.Logging.AzureAppServices/AzureAppServicesDiagnosticsSettings.cs).</span></span>

<span data-ttu-id="3d876-415">Zprostředkovatel funguje pouze při spuštění projektu v prostředí Azure.</span><span class="sxs-lookup"><span data-stu-id="3d876-415">The provider only works when your project runs in the Azure environment.</span></span> <span data-ttu-id="3d876-416">Nemá žádný vliv, pokud spouštíte místně &mdash; zapsat do místních souborů nebo vývoj pro místní úložiště pro objekty BLOB.</span><span class="sxs-lookup"><span data-stu-id="3d876-416">It has no effect when you run locally &mdash; it does not write to local files or local development storage for blobs.</span></span>

## <a name="third-party-logging-providers"></a><span data-ttu-id="3d876-417">Zprostředkovatelé třetí strany protokolování</span><span class="sxs-lookup"><span data-stu-id="3d876-417">Third-party logging providers</span></span>

<span data-ttu-id="3d876-418">Zde jsou některé rozhraní protokolování třetích stran, které pracují s ASP.NET Core:</span><span class="sxs-lookup"><span data-stu-id="3d876-418">Here are some third-party logging frameworks that work with ASP.NET Core:</span></span>

* <span data-ttu-id="3d876-419">[elmah.IO](https://github.com/elmahio/Elmah.Io.Extensions.Logging) -zprostředkovatele pro službu Elmah.Io</span><span class="sxs-lookup"><span data-stu-id="3d876-419">[elmah.io](https://github.com/elmahio/Elmah.Io.Extensions.Logging) - provider for the Elmah.Io service</span></span>

* <span data-ttu-id="3d876-420">[JSNLog](http://jsnlog.com) -protokoly výjimek jazyka JavaScript a dalších událostí na straně klienta pomocí protokolu na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="3d876-420">[JSNLog](http://jsnlog.com) - logs JavaScript exceptions and other client-side events in your server-side log.</span></span>

* <span data-ttu-id="3d876-421">[Loggr](https://github.com/imobile3/Loggr.Extensions.Logging) -zprostředkovatele pro službu Loggr</span><span class="sxs-lookup"><span data-stu-id="3d876-421">[Loggr](https://github.com/imobile3/Loggr.Extensions.Logging) - provider for the Loggr service</span></span>

* <span data-ttu-id="3d876-422">[NLog](https://github.com/NLog/NLog.Extensions.Logging) -zprostředkovatele pro knihovnu NLog</span><span class="sxs-lookup"><span data-stu-id="3d876-422">[NLog](https://github.com/NLog/NLog.Extensions.Logging) - provider for the NLog library</span></span>

* <span data-ttu-id="3d876-423">[Serilog](https://github.com/serilog/serilog-extensions-logging) -zprostředkovatele pro knihovnu Serilog</span><span class="sxs-lookup"><span data-stu-id="3d876-423">[Serilog](https://github.com/serilog/serilog-extensions-logging) - provider for the Serilog library</span></span>

<span data-ttu-id="3d876-424">Můžete provést některé architektury třetích stran [sémantické protokolování, také známé jako strukturovaný protokolování](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).</span><span class="sxs-lookup"><span data-stu-id="3d876-424">Some third-party frameworks can do [semantic logging, also known as structured logging](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).</span></span>

<span data-ttu-id="3d876-425">Pomocí rozhraní třetích stran je podobná pomocí jedné z předdefinované zprostředkovatele: Přidejte balíček NuGet do projektu a volání metody rozšíření na `ILoggerFactory`.</span><span class="sxs-lookup"><span data-stu-id="3d876-425">Using a third-party framework is similar to using one of the built-in providers: add a NuGet package to your project and call an extension method on `ILoggerFactory`.</span></span> <span data-ttu-id="3d876-426">Další informace najdete v dokumentaci k každý framework.</span><span class="sxs-lookup"><span data-stu-id="3d876-426">For more information, see each framework's documentation.</span></span>

<span data-ttu-id="3d876-427">Vaše vlastní zprostředkovatele taky můžete vytvořit pro podporu vlastního protokolování požadavky nebo jiných rozhraní protokolování.</span><span class="sxs-lookup"><span data-stu-id="3d876-427">You can create your own custom providers as well, to support other logging frameworks or your own logging requirements.</span></span>

## <a name="azure-log-streaming"></a><span data-ttu-id="3d876-428">Streamování protokolů Azure</span><span class="sxs-lookup"><span data-stu-id="3d876-428">Azure log streaming</span></span>

<span data-ttu-id="3d876-429">Vysílání datového proudu protokolů Azure umožňuje zobrazit aktivitu protokolu v reálném čase z:</span><span class="sxs-lookup"><span data-stu-id="3d876-429">Azure log streaming enables you to view log activity in real time from:</span></span> 

* <span data-ttu-id="3d876-430">Aplikační server</span><span class="sxs-lookup"><span data-stu-id="3d876-430">The application server</span></span> 
* <span data-ttu-id="3d876-431">Webový server</span><span class="sxs-lookup"><span data-stu-id="3d876-431">The web server</span></span>
* <span data-ttu-id="3d876-432">Trasování neúspěšných žádostí</span><span class="sxs-lookup"><span data-stu-id="3d876-432">Failed request tracing</span></span> 

<span data-ttu-id="3d876-433">Postup konfigurace streamování protokolů Azure:</span><span class="sxs-lookup"><span data-stu-id="3d876-433">To configure Azure log streaming:</span></span> 

* <span data-ttu-id="3d876-434">Přejděte na **protokolů diagnostiky** stránky ze stránky portálu vaší aplikace</span><span class="sxs-lookup"><span data-stu-id="3d876-434">Navigate to the **Diagnostics Logs** page from your application's portal page</span></span>
* <span data-ttu-id="3d876-435">Nastavit **protokolování aplikací (systém souborů)** na on.</span><span class="sxs-lookup"><span data-stu-id="3d876-435">Set **Application Logging (Filesystem)** to on.</span></span> 

![Stránka Azure portálu diagnostických protokolů](index/_static/azure-diagnostic-logs.png)

<span data-ttu-id="3d876-437">Přejděte na **vysílání datového proudu protokolu** stránky zobrazení zpráv aplikace.</span><span class="sxs-lookup"><span data-stu-id="3d876-437">Navigate to the **Log Streaming** page to view application messages.</span></span> <span data-ttu-id="3d876-438">Jsou zaznamenány aplikací pomocí `ILogger` rozhraní.</span><span class="sxs-lookup"><span data-stu-id="3d876-438">They are logged by application through the `ILogger` interface.</span></span> 

![Vysílání datového proudu protokolu aplikace portálu Azure](index/_static/azure-log-streaming.png)


## <a name="see-also"></a><span data-ttu-id="3d876-440">Viz také</span><span class="sxs-lookup"><span data-stu-id="3d876-440">See also</span></span>

[<span data-ttu-id="3d876-441">Vysoce výkonné protokolování s LoggerMessage</span><span class="sxs-lookup"><span data-stu-id="3d876-441">High-performance logging with LoggerMessage</span></span>](xref:fundamentals/logging/loggermessage)