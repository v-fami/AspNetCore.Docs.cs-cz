---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: "Prevence útoků otevřete přesměrování (C#) | Microsoft Docs"
author: jongalloway
description: "Tento kurz popisuje, jak lze zabránit útokům otevřete přesměrování v aplikacích ASP.NET MVC. Tento kurz popisuje změny, které byly provedeny..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: 97e0aacbf21914bf95f01019cf4dcc9e7ca1c4be
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/10/2017
---
<a name="preventing-open-redirection-attacks-c"></a><span data-ttu-id="f1a17-104">Prevence útoků otevřete přesměrování (C#)</span><span class="sxs-lookup"><span data-stu-id="f1a17-104">Preventing Open Redirection Attacks (C#)</span></span>
====================
<span data-ttu-id="f1a17-105">podle [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="f1a17-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="f1a17-106">Tento kurz popisuje, jak lze zabránit útokům otevřete přesměrování v aplikacích ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="f1a17-106">This tutorial explains how you can prevent open redirection attacks in your ASP.NET MVC applications.</span></span> <span data-ttu-id="f1a17-107">Tento kurz popisuje změny, které byly provedeny v AccountController v architektuře ASP.NET MVC 3 a ukazuje, jak můžete tyto změny použít na vaše stávající technologie ASP.NET MVC 1.0 a 2 aplikace.</span><span class="sxs-lookup"><span data-stu-id="f1a17-107">This tutorial discusses the changes that have been made in the AccountController in ASP.NET MVC 3 and demonstrates how you can apply these changes in your existing ASP.NET MVC 1.0 and 2 applications.</span></span>


## <a name="what-is-an-open-redirection-attack"></a><span data-ttu-id="f1a17-108">Co je útok otevřete přesměrování?</span><span class="sxs-lookup"><span data-stu-id="f1a17-108">What is an Open Redirection Attack?</span></span>

<span data-ttu-id="f1a17-109">Webové aplikace, který přesměruje na adresu URL, která je zadána prostřednictvím požadavku například řetězci dotazu nebo formuláře dat může potenciálně manipulováno k přesměrování uživatelů na externí, škodlivý URL.</span><span class="sxs-lookup"><span data-stu-id="f1a17-109">Any web application that redirects to a URL that is specified via the request such as the querystring or form data can potentially be tampered with to redirect users to an external, malicious URL.</span></span> <span data-ttu-id="f1a17-110">Tato manipulaci se nazývá útok otevřete přesměrování.</span><span class="sxs-lookup"><span data-stu-id="f1a17-110">This tampering is called an open redirection attack.</span></span>

<span data-ttu-id="f1a17-111">Vždy, když vaše aplikace logiky přesměruje na zadané adrese URL, je nutné ověřit, že adresu URL pro přesměrování nikdo neoprávněně nemanipuloval.</span><span class="sxs-lookup"><span data-stu-id="f1a17-111">Whenever your application logic redirects to a specified URL, you must verify that the redirection URL hasn't been tampered with.</span></span> <span data-ttu-id="f1a17-112">Přihlášení, které se používá ve výchozím AccountController pro ASP.NET MVC 1.0 a ASP.NET MVC 2 je zranitelný vůči útokům přesměrování otevřete.</span><span class="sxs-lookup"><span data-stu-id="f1a17-112">The login used in the default AccountController for both ASP.NET MVC 1.0 and ASP.NET MVC 2 is vulnerable to open redirection attacks.</span></span> <span data-ttu-id="f1a17-113">Naštěstí je snadné k aktualizaci existující aplikace oprav z verze Preview ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="f1a17-113">Fortunately, it is easy to update your existing applications to use the corrections from the ASP.NET MVC 3 Preview.</span></span>

<span data-ttu-id="f1a17-114">Zjistit chybu podíváme, jak funguje přesměrování přihlášení v projektu webové aplikace ASP.NET MVC 2 výchozí.</span><span class="sxs-lookup"><span data-stu-id="f1a17-114">To understand the vulnerability, let's look at how the login redirection works in a default ASP.NET MVC 2 Web Application project.</span></span> <span data-ttu-id="f1a17-115">V této aplikaci pokusu navštívit akce kontroleru, který má atribut [autorizovat] přesměruje neoprávnění uživatelé /Account/LogOn zobrazení.</span><span class="sxs-lookup"><span data-stu-id="f1a17-115">In this application, attempting to visit a controller action that has the [Authorize] attribute will redirect unauthorized users to the /Account/LogOn view.</span></span> <span data-ttu-id="f1a17-116">Tato přesměrování, které /Account/LogOn bude obsahovat parametr řetězce dotazu returnUrl tak, aby uživatel se může vracet na původně požadovanou URL adresu po jejich úspěšně přihlášeni.</span><span class="sxs-lookup"><span data-stu-id="f1a17-116">This redirect to /Account/LogOn will include a returnUrl querystring parameter so that the user can be returned to the originally requested URL after they have successfully logged in.</span></span>

<span data-ttu-id="f1a17-117">Na tomto snímku obrazovky uvidíme, že pokus o přístup k zobrazení /Account/ChangePassword, když není přihlášen výsledkem přesměrování na /Account/LogOn? ReturnUrl = % 2fAccount % 2fChangePassword % 2f.</span><span class="sxs-lookup"><span data-stu-id="f1a17-117">In the screenshot below, we can see that an attempt to access the /Account/ChangePassword view when not logged in results in a redirect to /Account/LogOn?ReturnUrl=%2fAccount%2fChangePassword%2f.</span></span>

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

<span data-ttu-id="f1a17-118">**Obrázek 01**: přihlašovací stránku s otevřete přesměrování</span><span class="sxs-lookup"><span data-stu-id="f1a17-118">**Figure 01**: Login page with an open redirection</span></span>

<span data-ttu-id="f1a17-119">Vzhledem k tomu, že parametr řetězce dotazu ReturnUrl není ověřená, útočník ho upravit, abyste vložit libovolnou adresu URL do parametru k provedení útoku otevřete přesměrování.</span><span class="sxs-lookup"><span data-stu-id="f1a17-119">Since the ReturnUrl querystring parameter is not validated, an attacker can modify it to inject any URL address into the parameter to conduct an open redirection attack.</span></span> <span data-ttu-id="f1a17-120">Ukazuje to jsme můžete změnit parametr ReturnUrl na [http://bing.com](http://bing.com), takže výsledný přihlašovací adresa URL bude/Account/přihlášení? ReturnUrl = http://www.bing.com/.</span><span class="sxs-lookup"><span data-stu-id="f1a17-120">To demonstrate this, we can modify the ReturnUrl parameter to [http://bing.com](http://bing.com), so the resulting login URL will be /Account/LogOn?ReturnUrl=http://www.bing.com/.</span></span> <span data-ttu-id="f1a17-121">Po úspěšně přihlašování k webu, jsme se přesměrují na [http://bing.com](http://bing.com). Vzhledem k tomu, že toto přesměrování není ověřen, může místo toho přejděte na škodlivé weby, které se pokouší přesvědčit uživatele, aby.</span><span class="sxs-lookup"><span data-stu-id="f1a17-121">Upon successfully logging in to the site, we are redirected to [http://bing.com](http://bing.com). Since this redirection is not validated, it could instead point to a malicious site that attempts to trick the user.</span></span>

### <a name="a-more-complex-open-redirection-attack"></a><span data-ttu-id="f1a17-122">Složitější otevřete útoku přesměrování</span><span class="sxs-lookup"><span data-stu-id="f1a17-122">A more complex Open Redirection Attack</span></span>

<span data-ttu-id="f1a17-123">Otevřete přesměrování útoky jsou obzvláště nebezpečné, protože útočník ví, že Pokoušíme se přihlaste se k určitému webu, který je zranitelný nám [útoky phishing](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1a17-123">Open redirection attacks are especially dangerous because an attacker knows that we're trying to log into a specific website, which makes us vulnerable to a [phishing attack](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx).</span></span> <span data-ttu-id="f1a17-124">Například útočník může odeslat škodlivý e-mailů webu uživatelům ve snaze zaznamenat jejich hesla.</span><span class="sxs-lookup"><span data-stu-id="f1a17-124">For example, an attacker could send malicious e-mails to website users in an attempt to capture their passwords.</span></span> <span data-ttu-id="f1a17-125">Podíváme, jak to bude fungovat na webu NerdDinner.</span><span class="sxs-lookup"><span data-stu-id="f1a17-125">Let's look at how this would work on the NerdDinner site.</span></span> <span data-ttu-id="f1a17-126">(Všimněte si, že byl aktualizován živý web NerdDinner chránit před útoky otevřete přesměrování.)</span><span class="sxs-lookup"><span data-stu-id="f1a17-126">(Note that the live NerdDinner site has been updated to protect against open redirection attacks.)</span></span>

<span data-ttu-id="f1a17-127">Nejprve útočník odešle nám odkaz na přihlašovací stránku na NerdDinner, která zahrnuje přesměrování, které jejich padělané stránky:</span><span class="sxs-lookup"><span data-stu-id="f1a17-127">First, an attacker sends us a link to the login page on NerdDinner that includes a redirect to their forged page:</span></span>

[<span data-ttu-id="f1a17-128">http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn</span><span class="sxs-lookup"><span data-stu-id="f1a17-128">http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn</span></span>](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

<span data-ttu-id="f1a17-129">Všimněte si, že návratová adresa URL odkazuje na nerddiner.com, které chybí "n" z večeři aplikace word.</span><span class="sxs-lookup"><span data-stu-id="f1a17-129">Note that the return URL points to nerddiner.com, which is missing an "n" from the word dinner.</span></span> <span data-ttu-id="f1a17-130">V tomto příkladu je to doméně, která určuje, že útočník.</span><span class="sxs-lookup"><span data-stu-id="f1a17-130">In this example, this is a domain that the attacker controls.</span></span> <span data-ttu-id="f1a17-131">Když jsme získat přístup na výše uvedený odkaz, jsme se prováděné na oprávněné NerdDinner.com přihlašovací stránku.</span><span class="sxs-lookup"><span data-stu-id="f1a17-131">When we access the above link, we're taken to the legitimate NerdDinner.com login page.</span></span>

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

<span data-ttu-id="f1a17-132">**Obrázek 02**: NerdDinner přihlašovací stránku s otevřete přesměrování</span><span class="sxs-lookup"><span data-stu-id="f1a17-132">**Figure 02**: NerdDinner login page with an open redirection</span></span>

<span data-ttu-id="f1a17-133">Když jsme správně přihlásit, akce ASP.NET MVC AccountController přihlášení nám přesměruje na adresu URL zadanou v parametru řetězce dotazu returnUrl.</span><span class="sxs-lookup"><span data-stu-id="f1a17-133">When we correctly log in, the ASP.NET MVC AccountController's LogOn action redirects us to the URL specified in the returnUrl querystring parameter.</span></span> <span data-ttu-id="f1a17-134">V takovém případě je adresu URL, kterou má zadán útočník, který je [http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="f1a17-134">In this case, it's the URL that the attacker has entered, which is [http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn).</span></span> <span data-ttu-id="f1a17-135">Pokud jsme velmi watchful, že je velmi pravděpodobné, že nebude, zjistíme zvlášť, protože útočník byl pečlivě zkontrolujte, zda jejich padělané stránka vypadá úplně stejně jako legitimní přihlašovací stránku.</span><span class="sxs-lookup"><span data-stu-id="f1a17-135">Unless we're extremely watchful, it's very likely we won't notice this, especially because the attacker has been careful to make sure that their forged page looks exactly like the legitimate login page.</span></span> <span data-ttu-id="f1a17-136">Tento přihlašovací stránku obsahuje, chyba zprávu požadavku, nemůžeme přihlásit znovu.</span><span class="sxs-lookup"><span data-stu-id="f1a17-136">This login page includes an error message requesting that we login again.</span></span> <span data-ttu-id="f1a17-137">Clumsy nás, jsme musí zadali heslo.</span><span class="sxs-lookup"><span data-stu-id="f1a17-137">Clumsy us, we must have mistyped our password.</span></span>

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

<span data-ttu-id="f1a17-138">**Obrázek 03**: Forged NerdDinner přihlašovací obrazovku</span><span class="sxs-lookup"><span data-stu-id="f1a17-138">**Figure 03**: Forged NerdDinner Login screen</span></span>

<span data-ttu-id="f1a17-139">Když jsme znovu naše uživatelské jméno a heslo, padělané přihlašovací stránky uloží informace a odešle nám zpět na web legitimní NerdDinner.com.</span><span class="sxs-lookup"><span data-stu-id="f1a17-139">When we retype our user name and password, the forged login page saves the information and sends us back to the legitimate NerdDinner.com site.</span></span> <span data-ttu-id="f1a17-140">V tomto okamžiku NerdDinner.com lokality již ověřen nám, takže přímo na této stránce můžete přesměrovat padělané přihlašovací stránku.</span><span class="sxs-lookup"><span data-stu-id="f1a17-140">At this point, the NerdDinner.com site has already authenticated us, so the forged login page can redirect directly to that page.</span></span> <span data-ttu-id="f1a17-141">Konečným výsledkem je, že útočník má naše uživatelské jméno a heslo a jsme neberou v úvahu, že jsme jste zadali na ně.</span><span class="sxs-lookup"><span data-stu-id="f1a17-141">The end result is that the attacker has our user name and password, and we are unaware that we've provided it to them.</span></span>

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a><span data-ttu-id="f1a17-142">Prohlížení kód citlivé na přihlášení akce AccountController</span><span class="sxs-lookup"><span data-stu-id="f1a17-142">Looking at the vulnerable code in the AccountController LogOn Action</span></span>

<span data-ttu-id="f1a17-143">Kód pro přihlášení akce v aplikaci ASP.NET MVC 2 je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="f1a17-143">The code for the LogOn action in an ASP.NET MVC 2 application is shown below.</span></span> <span data-ttu-id="f1a17-144">Všimněte si, že po úspěšném přihlášení kontroleru vrátí přesměrování returnUrl.</span><span class="sxs-lookup"><span data-stu-id="f1a17-144">Note that upon a successful login, the controller returns a redirect to the returnUrl.</span></span> <span data-ttu-id="f1a17-145">Uvidíte, že žádné ověření se provádí před returnUrl parametr.</span><span class="sxs-lookup"><span data-stu-id="f1a17-145">You can see that no validation is being performed against the returnUrl parameter.</span></span>

<span data-ttu-id="f1a17-146">**Výpis 1 – akce ASP.NET MVC 2 přihlášení v`AccountController.cs`**</span><span class="sxs-lookup"><span data-stu-id="f1a17-146">**Listing 1 – ASP.NET MVC 2 LogOn action in `AccountController.cs`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

<span data-ttu-id="f1a17-147">Nyní Podíváme se na změny akce ASP.NET MVC 3 přihlášení.</span><span class="sxs-lookup"><span data-stu-id="f1a17-147">Now let's look at the changes to the ASP.NET MVC 3 LogOn action.</span></span> <span data-ttu-id="f1a17-148">Tento kód byl změněn na ověření parametru returnUrl voláním nové metody v System.Web.Mvc.Url pomocná třída s názvem `IsLocalUrl()`.</span><span class="sxs-lookup"><span data-stu-id="f1a17-148">This code has been changed to validate the returnUrl parameter by calling a new method in the System.Web.Mvc.Url helper class named `IsLocalUrl()`.</span></span>

<span data-ttu-id="f1a17-149">**Výpis 2 – akce ASP.NET MVC 3 přihlášení v`AccountController.cs`**</span><span class="sxs-lookup"><span data-stu-id="f1a17-149">**Listing 2 – ASP.NET MVC 3 LogOn action in `AccountController.cs`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

<span data-ttu-id="f1a17-150">To se změnil na ověření parametr návratové adresy URL voláním nové metody v System.Web.Mvc.Url pomocná třída, `IsLocalUrl()`.</span><span class="sxs-lookup"><span data-stu-id="f1a17-150">This has been changed to validate the return URL parameter by calling a new method in the System.Web.Mvc.Url helper class, `IsLocalUrl()`.</span></span>

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a><span data-ttu-id="f1a17-151">Ochrana rozhraní ASP.NET MVC 1,0 a MVC 2 aplikace</span><span class="sxs-lookup"><span data-stu-id="f1a17-151">Protecting Your ASP.NET MVC 1.0 and MVC 2 Applications</span></span>

<span data-ttu-id="f1a17-152">Přidáním pomocnou metodu IsLocalUrl() a aktualizaci akce přihlášení k ověření parametru returnUrl jsme můžete využít výhod ASP.NET MVC 3 změny v našem existující ASP.NET MVC 1.0 a 2 aplikace.</span><span class="sxs-lookup"><span data-stu-id="f1a17-152">We can take advantage of the ASP.NET MVC 3 changes in our existing ASP.NET MVC 1.0 and 2 applications by adding the IsLocalUrl() helper method and updating the LogOn action to validate the returnUrl parameter.</span></span>

<span data-ttu-id="f1a17-153">Metoda UrlHelper IsLocalUrl() ve skutečnosti jenom volání do metody v System.Web.WebPages jako toto ověření používá i rozhraní ASP.NET Web Pages.</span><span class="sxs-lookup"><span data-stu-id="f1a17-153">The UrlHelper IsLocalUrl() method actually just calling into a method in System.Web.WebPages, as this validation is also used by ASP.NET Web Pages applications.</span></span>

<span data-ttu-id="f1a17-154">**Výpis 3 – metoda IsLocalUrl() z ASP.NET MVC 3 UrlHelper`class`**</span><span class="sxs-lookup"><span data-stu-id="f1a17-154">**Listing 3 – The IsLocalUrl() method from the ASP.NET MVC 3 UrlHelper `class`**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

<span data-ttu-id="f1a17-155">Metoda IsUrlLocalToHost obsahuje logiku samotné ověření, jak je znázorněno v výpis 4.</span><span class="sxs-lookup"><span data-stu-id="f1a17-155">The IsUrlLocalToHost method contains the actual validation logic, as shown in Listing 4.</span></span>

<span data-ttu-id="f1a17-156">**Výpis 4 – metoda IsUrlLocalToHost() z System.Web.WebPages RequestExtensions – třída**</span><span class="sxs-lookup"><span data-stu-id="f1a17-156">**Listing 4 – IsUrlLocalToHost() method from the System.Web.WebPages RequestExtensions class**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

<span data-ttu-id="f1a17-157">V našich ASP.NET MVC 1.0 nebo 2 aplikace přidáme IsLocalUrl() metoda do AccountController, ale jste doporučujeme, aby ho přidat do samostatné pomocná třída Pokud je to možné.</span><span class="sxs-lookup"><span data-stu-id="f1a17-157">In our ASP.NET MVC 1.0 or 2 application, we'll add a IsLocalUrl() method to the AccountController, but you're encouraged to add it to a separate helper class if possible.</span></span> <span data-ttu-id="f1a17-158">Jsme tak, že bude pracovat uvnitř AccountController budou dva malé změny ve verzi ASP.NET MVC 3 IsLocalUrl().</span><span class="sxs-lookup"><span data-stu-id="f1a17-158">We will make two small changes to the ASP.NET MVC 3 version of IsLocalUrl() so that it will work inside the AccountController.</span></span> <span data-ttu-id="f1a17-159">Nejprve Změníme jeho z veřejné metody privátní metodu, vzhledem k tomu, že jsou přístupné veřejné metody v řadiče jako akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="f1a17-159">First, we'll change it from a public method to a private method, since public methods in controllers can be accessed as controller actions.</span></span> <span data-ttu-id="f1a17-160">Za druhé upravíme volání, která kontroluje hostitele adresy URL pro hostitele aplikací.</span><span class="sxs-lookup"><span data-stu-id="f1a17-160">Second, we'll modify the call that checks the URL host against the application host.</span></span> <span data-ttu-id="f1a17-161">Aby se volání využívá místní kontext požadavku pole Třída UrlHelper.</span><span class="sxs-lookup"><span data-stu-id="f1a17-161">That call makes use of a local RequestContext field in the UrlHelper class.</span></span> <span data-ttu-id="f1a17-162">Nepoužívejte. RequestContext.HttpContext.Request.Url.Host, použijeme to. Request.Url.Host.</span><span class="sxs-lookup"><span data-stu-id="f1a17-162">Instead of using this.RequestContext.HttpContext.Request.Url.Host, we will use this.Request.Url.Host.</span></span> <span data-ttu-id="f1a17-163">Následující kód ukazuje změny metoda IsLocalUrl() pro použití s třídou řadiče v ASP.NET MVC 1.0 a 2 aplikace.</span><span class="sxs-lookup"><span data-stu-id="f1a17-163">The following code shows the modified IsLocalUrl() method for use with a controller class in ASP.NET MVC 1.0 and 2 applications.</span></span>

<span data-ttu-id="f1a17-164">**Výpis 5 – IsLocalUrl() metoda, která je upravit pro použití s třídu MVC jsou řadič MVC**</span><span class="sxs-lookup"><span data-stu-id="f1a17-164">**Listing 5 – IsLocalUrl() method, which is modified for use with an MVC Controller class**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

<span data-ttu-id="f1a17-165">Teď, když metoda IsLocalUrl() je na místě, jsme ji volat z našich akce přihlášení k ověření parametru returnUrl, jak je znázorněno v následujícím kódu.</span><span class="sxs-lookup"><span data-stu-id="f1a17-165">Now that the IsLocalUrl() method is in place, we can call it from our LogOn action to validate the returnUrl parameter, as shown in the following code.</span></span>

<span data-ttu-id="f1a17-166">**Výpis 6 – aktualizované přihlášení metodu, která ověří parametr returnUrl**</span><span class="sxs-lookup"><span data-stu-id="f1a17-166">**Listing 6 – Updated LogOn method which validates the returnUrl parameter**</span></span>

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

<span data-ttu-id="f1a17-167">Nyní jsme můžete otestovat útoku otevřete přesměrování probíhá pokus o přihlášení pomocí externí návratovou adresu URL.</span><span class="sxs-lookup"><span data-stu-id="f1a17-167">Now we can test an open redirection attack by attempting to log in using an external return URL.</span></span> <span data-ttu-id="f1a17-168">Umožňuje používat/Account/přihlášení? ReturnUrl = http://www.bing.com/ znovu.</span><span class="sxs-lookup"><span data-stu-id="f1a17-168">Let's use /Account/LogOn?ReturnUrl=http://www.bing.com/ again.</span></span>

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

<span data-ttu-id="f1a17-169">**Obrázek 04**: testování aktualizované akce přihlášení</span><span class="sxs-lookup"><span data-stu-id="f1a17-169">**Figure 04**: Testing the updated LogOn Action</span></span>

<span data-ttu-id="f1a17-170">Po úspěšném přihlášení se jsme se přesměrují do akce Kontroleru domovské nebo indexu, nikoli na externí adresu URL.</span><span class="sxs-lookup"><span data-stu-id="f1a17-170">After successfully logging in, we are redirected to the Home/Index Controller action rather than the external URL.</span></span>

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

<span data-ttu-id="f1a17-171">**Obrázek 05**: Otevřete přesměrování útoku potlačována</span><span class="sxs-lookup"><span data-stu-id="f1a17-171">**Figure 05**: Open Redirection attack defeated</span></span>

## <a name="summary"></a><span data-ttu-id="f1a17-172">Souhrn</span><span class="sxs-lookup"><span data-stu-id="f1a17-172">Summary</span></span>

<span data-ttu-id="f1a17-173">Otevřete přesměrování útoky může dojít, když přesměrování adresy URL jsou předány jako parametry v adrese URL pro aplikaci.</span><span class="sxs-lookup"><span data-stu-id="f1a17-173">Open redirection attacks can occur when redirection URLs are passed as parameters in the URL for an application.</span></span> <span data-ttu-id="f1a17-174">Otevřete ASP.NET MVC 3, šablona obsahuje kód pro ochranu proti útokům přesměrování.</span><span class="sxs-lookup"><span data-stu-id="f1a17-174">The ASP.NET MVC 3 template includes code to protect against open redirection attacks.</span></span> <span data-ttu-id="f1a17-175">Můžete přidat tento kód se některé změny ASP.NET MVC 1.0 a 2 aplikace.</span><span class="sxs-lookup"><span data-stu-id="f1a17-175">You can add this code with some modification to ASP.NET MVC 1.0 and 2 applications.</span></span> <span data-ttu-id="f1a17-176">Chránit před útoky otevřete přesměrování při přihlašování do ASP.NET 1.0 a 2 aplikací, přidejte metodu IsLocalUrl() a ověření parametru returnUrl v akci pro přihlášení.</span><span class="sxs-lookup"><span data-stu-id="f1a17-176">To protect against open redirection attacks when logging into ASP.NET 1.0 and 2 applications, add a IsLocalUrl() method and validate the returnUrl parameter in the LogOn action.</span></span>