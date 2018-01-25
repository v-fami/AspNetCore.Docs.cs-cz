---
title: Browser Link v ASP.NET Core
author: ncarandini
description: "Vysvětluje, jak Browser Link je funkce sady Visual Studio, který odkazuje vývojového prostředí s jeden nebo více webových prohlížečů."
ms.author: riande
manager: wpickett
ms.date: 09/22/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: client-side/using-browserlink
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d5db65c268923e96c45b034639437fc3496ccac1
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/19/2018
---
# <a name="browser-link-in-aspnet-core"></a><span data-ttu-id="064cb-103">Browser Link v ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="064cb-103">Browser Link in ASP.NET Core</span></span> 

<span data-ttu-id="064cb-104">Podle [Nicolò Carandini](https://github.com/ncarandini), [Karel Wasson](https://github.com/MikeWasson), a [tní Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="064cb-104">By [Nicolò Carandini](https://github.com/ncarandini), [Mike Wasson](https://github.com/MikeWasson), and [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="064cb-105">Browser Link je funkce v sadě Visual Studio, který vytváří komunikační kanál mezi vývojového prostředí a jeden nebo více webových prohlížečů.</span><span class="sxs-lookup"><span data-stu-id="064cb-105">Browser Link is a feature in Visual Studio that creates a communication channel between the development environment and one or more web browsers.</span></span> <span data-ttu-id="064cb-106">Můžete použít Browser Link aktualizujte svoji webovou aplikaci v několika prohlížeče najednou, což je užitečné pro testování různých prohlížečích.</span><span class="sxs-lookup"><span data-stu-id="064cb-106">You can use Browser Link to refresh your web application in several browsers at once, which is useful for cross-browser testing.</span></span>

## <a name="browser-link-setup"></a><span data-ttu-id="064cb-107">Instalační program odkaz prohlížeče</span><span class="sxs-lookup"><span data-stu-id="064cb-107">Browser Link setup</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="064cb-108">ASP.NET základní 2.x</span><span class="sxs-lookup"><span data-stu-id="064cb-108">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="064cb-109">ASP.NET Core 2.x **webové aplikace**, **prázdný**, a **webového rozhraní API** šablony projektů, použití [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) Meta balíček, který obsahuje odkaz na balíček pro [Microsoft.VisualStudio.Web.BrowserLink](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.BrowserLink/).</span><span class="sxs-lookup"><span data-stu-id="064cb-109">The ASP.NET Core 2.x **Web Application**, **Empty**, and **Web API** template projects use the [Microsoft.AspNetCore.All](https://www.nuget.org/packages/Microsoft.AspNetCore.All/) meta-package, which contains a package reference for [Microsoft.VisualStudio.Web.BrowserLink](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.BrowserLink/).</span></span> <span data-ttu-id="064cb-110">Proto pomocí `Microsoft.AspNetCore.All` metabalíček vyžadována žádná další akce, chcete-li k dispozici pro použití odkazů prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="064cb-110">Therefore, using the `Microsoft.AspNetCore.All` meta-package requires no further action to make Browser Link available for use.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="064cb-111">ASP.NET základní 1.x</span><span class="sxs-lookup"><span data-stu-id="064cb-111">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="064cb-112">ASP.NET Core 1.x **webové aplikace** šablona projektu obsahuje odkaz na balíček pro [Microsoft.VisualStudio.Web.BrowserLink](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.BrowserLink/) balíčku.</span><span class="sxs-lookup"><span data-stu-id="064cb-112">The ASP.NET Core 1.x **Web Application** project template has a package reference for the [Microsoft.VisualStudio.Web.BrowserLink](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.BrowserLink/) package.</span></span> <span data-ttu-id="064cb-113">**Prázdný** nebo **webového rozhraní API** šablony projektů vyžadují, abyste přidat odkaz na balíček `Microsoft.VisualStudio.Web.BrowserLink`.</span><span class="sxs-lookup"><span data-stu-id="064cb-113">The **Empty** or **Web API** template projects require you to add a package reference to `Microsoft.VisualStudio.Web.BrowserLink`.</span></span>

<span data-ttu-id="064cb-114">Vzhledem k tomu, že toto je funkce sady Visual Studio, nejjednodušší způsob přidání balíčku, který má **prázdný** nebo **webového rozhraní API** projektu šablony je otevřít **Konzola správce balíčků** (**Zobrazení** > **ostatní okna** > **Konzola správce balíčků**) a spusťte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="064cb-114">Since this is a Visual Studio feature, the easiest way to add the package to an **Empty** or **Web API** template project is to open the **Package Manager Console** (**View** > **Other Windows** > **Package Manager Console**) and run the following command:</span></span>

```console
install-package Microsoft.VisualStudio.Web.BrowserLink
```

<span data-ttu-id="064cb-115">Alternativně můžete použít **Správce balíčků NuGet**.</span><span class="sxs-lookup"><span data-stu-id="064cb-115">Alternatively, you can use **NuGet Package Manager**.</span></span> <span data-ttu-id="064cb-116">Klikněte pravým tlačítkem myši na název projektu v **Průzkumníku řešení** a zvolte **spravovat balíčky NuGet**:</span><span class="sxs-lookup"><span data-stu-id="064cb-116">Right-click the project name in **Solution Explorer** and choose **Manage NuGet Packages**:</span></span>

![Správce balíčků NuGet otevřít](using-browserlink/_static/open-nuget-package-manager.png)

<span data-ttu-id="064cb-118">Najít a nainstalovat balíček:</span><span class="sxs-lookup"><span data-stu-id="064cb-118">Find and install the package:</span></span>

![Přidejte balíček s Správce balíčků NuGet](using-browserlink/_static/add-package-with-nuget-package-manager.png)

---

### <a name="configuration"></a><span data-ttu-id="064cb-120">Konfigurace</span><span class="sxs-lookup"><span data-stu-id="064cb-120">Configuration</span></span>

<span data-ttu-id="064cb-121">V `Configure` metodu *Startup.cs* souboru:</span><span class="sxs-lookup"><span data-stu-id="064cb-121">In the `Configure` method of the *Startup.cs* file:</span></span>

```csharp
app.UseBrowserLink();
```

<span data-ttu-id="064cb-122">Obvykle je kód uvnitř `if` blok, který umožňuje pouze Browser Link ve vývojovém prostředí, jak je vidět tady:</span><span class="sxs-lookup"><span data-stu-id="064cb-122">Usually the code is inside an `if` block that only enables Browser Link in the Development environment, as shown here:</span></span>

```csharp
if (env.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
    app.UseBrowserLink();
}
```

<span data-ttu-id="064cb-123">Další informace najdete v tématu [práce s několika prostředí](xref:fundamentals/environments).</span><span class="sxs-lookup"><span data-stu-id="064cb-123">For more information, see [Working with Multiple Environments](xref:fundamentals/environments).</span></span>

## <a name="how-to-use-browser-link"></a><span data-ttu-id="064cb-124">Postup použití Browser Link</span><span class="sxs-lookup"><span data-stu-id="064cb-124">How to use Browser Link</span></span>

<span data-ttu-id="064cb-125">Když máte projekt ASP.NET Core otevřete, Visual Studio zobrazí ovládacím prvkem panel nástrojů Browser Link vedle **cíl ladění** prvku panel nástrojů:</span><span class="sxs-lookup"><span data-stu-id="064cb-125">When you have an ASP.NET Core project open, Visual Studio shows the Browser Link toolbar control next to the **Debug Target** toolbar control:</span></span>

![Prohlížeč odkaz rozevírací nabídky](using-browserlink/_static/browserLink-dropdown-menu.png)

<span data-ttu-id="064cb-127">Z ovládacího prvku panel nástrojů Browser Link můžete:</span><span class="sxs-lookup"><span data-stu-id="064cb-127">From the Browser Link toolbar control, you can:</span></span>

* <span data-ttu-id="064cb-128">Aktualizace webové aplikace v prohlížečích několik najednou.</span><span class="sxs-lookup"><span data-stu-id="064cb-128">Refresh the web application in several browsers at once.</span></span>
* <span data-ttu-id="064cb-129">Otevřete **řídicím odkazů prohlížeče**.</span><span class="sxs-lookup"><span data-stu-id="064cb-129">Open the **Browser Link Dashboard**.</span></span>
* <span data-ttu-id="064cb-130">Povolit nebo zakázat **Browser Link**.</span><span class="sxs-lookup"><span data-stu-id="064cb-130">Enable or disable **Browser Link**.</span></span> <span data-ttu-id="064cb-131">Poznámka: Ve výchozím nastavení v aplikaci Visual Studio 2017 (15.3) vypnutá odkazů prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="064cb-131">Note: Browser Link is disabled by default in Visual Studio 2017 (15.3).</span></span>
* <span data-ttu-id="064cb-132">Povolit nebo zakázat [Automatická synchronizace šablon stylů CSS](#enable-or-disable-css-auto-sync).</span><span class="sxs-lookup"><span data-stu-id="064cb-132">Enable or disable [CSS Auto-Sync](#enable-or-disable-css-auto-sync).</span></span>

> [!NOTE]
> <span data-ttu-id="064cb-133">Některé sady Visual Studio moduly plug-in, zejména *webové rozšíření Pack 2015* a *2017 Pack rozšíření webové*, nabízí rozšířené funkce pro Browser Link, ale některé další funkce nefungují s prostředím ASP. Projekty Asp.net Core.</span><span class="sxs-lookup"><span data-stu-id="064cb-133">Some Visual Studio plug-ins, most notably *Web Extension Pack 2015* and *Web Extension Pack 2017*, offer extended functionality for Browser Link, but some of the additional features don't work with ASP.NET Core projects.</span></span>

## <a name="refresh-the-web-application-in-several-browsers-at-once"></a><span data-ttu-id="064cb-134">Aktualizace webové aplikace v prohlížečích několik najednou</span><span class="sxs-lookup"><span data-stu-id="064cb-134">Refresh the web application in several browsers at once</span></span>

<span data-ttu-id="064cb-135">Zvolte jeden webový prohlížeč, aby spuštění při spuštění projektu, použijte rozevírací nabídky v **cíl ladění** prvku panel nástrojů:</span><span class="sxs-lookup"><span data-stu-id="064cb-135">To choose a single web browser to launch when starting the project, use the drop-down menu in the **Debug Target** toolbar control:</span></span>

![F5 rozevírací nabídky](using-browserlink/_static/debug-target-dropdown-menu.png)

<span data-ttu-id="064cb-137">Otevřete více prohlížečů najednou, zvolte **procházet s...**  ze stejné rozevíracího seznamu.</span><span class="sxs-lookup"><span data-stu-id="064cb-137">To open multiple browsers at once, choose **Browse with...** from the same drop-down.</span></span> <span data-ttu-id="064cb-138">Podržte stisknutou klávesu CTRL k výběru prohlížeče, který chcete a pak klikněte na **Procházet**:</span><span class="sxs-lookup"><span data-stu-id="064cb-138">Hold down the CTRL key to select the browsers you want, and then click **Browse**:</span></span>

![Otevřete najednou mnoha prohlížečů](using-browserlink/_static/open-many-browsers-at-once.png)

<span data-ttu-id="064cb-140">Zde je snímek obrazovky zobrazující Visual Studio s zobrazení indexu otevřete a otevřete prohlížečů:</span><span class="sxs-lookup"><span data-stu-id="064cb-140">Here's a screenshot showing Visual Studio with the Index view open and two open browsers:</span></span>

![Synchronizovat s příklad prohlížečů](using-browserlink/_static/sync-with-two-browsers-example.png)

<span data-ttu-id="064cb-142">Najeďte myší na ovládací prvek Browser Link panelu nástrojů zobrazíte prohlížečů, které jsou připojené do projektu:</span><span class="sxs-lookup"><span data-stu-id="064cb-142">Hover over the Browser Link toolbar control to see the browsers that are connected to the project:</span></span>

![Najeďte tipu](using-browserlink/_static/hoover-tip.png)

<span data-ttu-id="064cb-144">Změnit zobrazení indexu a všechny připojené prohlížeče aktualizují po kliknutí na tlačítko Aktualizovat Browser Link:</span><span class="sxs-lookup"><span data-stu-id="064cb-144">Change the Index view, and all connected browsers are updated when you click the Browser Link refresh button:</span></span>

![browsers-sync-to-changes](using-browserlink/_static/browsers-sync-to-changes.png)

<span data-ttu-id="064cb-146">Browser Link funguje taky s prohlížeče, které spusťte mimo aplikaci Visual Studio a přejděte na adresu URL aplikace.</span><span class="sxs-lookup"><span data-stu-id="064cb-146">Browser Link also works with browsers that you launch from outside Visual Studio and navigate to the application URL.</span></span>

### <a name="the-browser-link-dashboard"></a><span data-ttu-id="064cb-147">Řídicím panelu odkazů prohlížeče</span><span class="sxs-lookup"><span data-stu-id="064cb-147">The Browser Link Dashboard</span></span>

<span data-ttu-id="064cb-148">Z rozevírací nabídky ke správě připojení pomocí prohlížeče otevřete Browser Link otevřete řídicím panelu odkazů prohlížeče:</span><span class="sxs-lookup"><span data-stu-id="064cb-148">Open the Browser Link Dashboard from the Browser Link drop down menu to manage the connection with open browsers:</span></span>

![open-browserslink-dashboard](using-browserlink/_static/open-browserlink-dashboard.png)

<span data-ttu-id="064cb-150">Pokud je připojený žádný prohlížeč, můžete spustit relaci – ladění výběrem *zobrazit v prohlížeči* odkaz:</span><span class="sxs-lookup"><span data-stu-id="064cb-150">If no browser is connected, you can start a non-debugging session by selecting the *View in Browser* link:</span></span>

![browserlink-dashboard-no-connections](using-browserlink/_static/browserlink-dashboard-no-connections.png)

<span data-ttu-id="064cb-152">Jinak hodnota cesta ke stránce, který se zobrazuje každým prohlížečem, který zobrazuje připojené prohlížeče:</span><span class="sxs-lookup"><span data-stu-id="064cb-152">Otherwise, the connected browsers are shown with the path to the page that each browser is showing:</span></span>

![browserlink-dashboard-two-connections](using-browserlink/_static/browserlink-dashboard-two-connections.png)

<span data-ttu-id="064cb-154">Pokud chcete, můžete kliknutím na název uvedené prohlížeče aktualizujte tohoto jednoho prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="064cb-154">If you like, you can click on a listed browser name to refresh that single browser.</span></span>

### <a name="enable-or-disable-browser-link"></a><span data-ttu-id="064cb-155">Povolit nebo zakázat Browser Link</span><span class="sxs-lookup"><span data-stu-id="064cb-155">Enable or disable Browser Link</span></span>

<span data-ttu-id="064cb-156">Pokud znovu povolíte Browser Link po jejím zakázáním, je nutné aktualizovat prohlížeče se je znovu připojit.</span><span class="sxs-lookup"><span data-stu-id="064cb-156">When you re-enable Browser Link after disabling it, you must refresh the browsers to reconnect them.</span></span>

### <a name="enable-or-disable-css-auto-sync"></a><span data-ttu-id="064cb-157">Povolit nebo zakázat automatickou synchronizaci šablon stylů CSS</span><span class="sxs-lookup"><span data-stu-id="064cb-157">Enable or disable CSS Auto-Sync</span></span>

<span data-ttu-id="064cb-158">Pokud je povolena automatická synchronizace šablon stylů CSS, připojené prohlížeče se automaticky aktualizují při provést změnu souborů CSS.</span><span class="sxs-lookup"><span data-stu-id="064cb-158">When CSS Auto-Sync is enabled, connected browsers are automatically refreshed when you make any change to CSS files.</span></span>

## <a name="how-does-it-work"></a><span data-ttu-id="064cb-159">Jak to funguje?</span><span class="sxs-lookup"><span data-stu-id="064cb-159">How does it work?</span></span>

<span data-ttu-id="064cb-160">Browser Link používá k vytvoření komunikační kanál mezi Visual Studio a prohlížeči SignalR.</span><span class="sxs-lookup"><span data-stu-id="064cb-160">Browser Link uses SignalR to create a communication channel between Visual Studio and the browser.</span></span> <span data-ttu-id="064cb-161">Pokud je povoleno Browser Link, Visual Studio funguje jako server SignalR, více klientů (prohlížeče) mohou připojit.</span><span class="sxs-lookup"><span data-stu-id="064cb-161">When Browser Link is enabled, Visual Studio acts as a SignalR server that multiple clients (browsers) can connect to.</span></span> <span data-ttu-id="064cb-162">Browser Link také zaregistruje komponentu middleware v kanálu požadavku ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="064cb-162">Browser Link also registers a middleware component in the ASP.NET request pipeline.</span></span> <span data-ttu-id="064cb-163">Tato součást Vloží speciální `<script>` odkazy na každý požadavek na stránku ze serveru.</span><span class="sxs-lookup"><span data-stu-id="064cb-163">This component injects special `<script>` references into every page request from the server.</span></span> <span data-ttu-id="064cb-164">Zobrazí odkazům na skript tak, že vyberete **zobrazit zdroj** v prohlížeči a posouvání na konec `<body>` označení obsahu:</span><span class="sxs-lookup"><span data-stu-id="064cb-164">You can see the script references by selecting **View source** in the browser and scrolling to the end of the `<body>` tag content:</span></span>

```javascript
    <!-- Visual Studio Browser Link -->
    <script type="application/json" id="__browserLink_initializationData">
        {"requestId":"a717d5a07c1741949a7cefd6fa2bad08","requestMappingFromServer":false}
    </script>
    <script type="text/javascript" src="http://localhost:54139/b6e36e429d034f578ebccd6a79bf19bf/browserLink" async="async"></script>
    <!-- End Browser Link -->
</body>
```

<span data-ttu-id="064cb-165">Zdrojové soubory vašeho se nemění.</span><span class="sxs-lookup"><span data-stu-id="064cb-165">Your source files aren't modified.</span></span> <span data-ttu-id="064cb-166">Komponenta middlewaru vloží odkazům na skript dynamicky.</span><span class="sxs-lookup"><span data-stu-id="064cb-166">The middleware component injects the script references dynamically.</span></span> 

<span data-ttu-id="064cb-167">Protože kód prohlížeče na straně je všechny JavaScript, funguje u všech prohlížečů, které podporuje SignalR bez nutnosti modul plug-in prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="064cb-167">Because the browser-side code is all JavaScript, it works on all browsers that SignalR supports without requiring a browser plug-in.</span></span>