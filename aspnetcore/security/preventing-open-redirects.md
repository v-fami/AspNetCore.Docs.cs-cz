---
title: Zabránit útokům v otevřeném přesměrování v ASP.NET Core
author: ardalis
description: Ukazuje, jak zabránit otevírání útoků přesměrování proti ASP.NET Core aplikaci.
ms.author: riande
ms.date: 07/07/2017
uid: security/preventing-open-redirects
ms.openlocfilehash: 9d8cac8708fe9aeadba5af1287362a20df7f6bfe
ms.sourcegitcommit: 9a129f5f3e31cc449742b164d5004894bfca90aa
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78660522"
---
# <a name="prevent-open-redirect-attacks-in-aspnet-core"></a>Zabránit útokům v otevřeném přesměrování v ASP.NET Core

Webová aplikace, která přesměrovává na adresu URL zadanou prostřednictvím žádosti, jako je například dotaz nebo data formuláře, může být úmyslně poškozena pro přesměrování uživatelů na externí škodlivou adresu URL. Tato manipulace se nazývá útok typu otevřené přesměrování.

Vždy, když vaše logika aplikace přesměrovává na zadanou adresu URL, je nutné ověřit, že adresa URL pro přesměrování nebyla úmyslně poškozena. ASP.NET Core má integrovanou funkcionalitu, která vám může pomáhat chránit aplikace před otevřeným přesměrováním (označuje se také jako otevřené přesměrování).

## <a name="what-is-an-open-redirect-attack"></a>Co je otevřený útok na přesměrování?

Webové aplikace často přesměrují uživatele na přihlašovací stránku, když přistupují k prostředkům, které vyžadují ověření. Přesměrování obvykle obsahuje parametr `returnUrl` QueryString, aby se uživatel mohl vrátit na původně požadovanou adresu URL po úspěšném přihlášení. Po ověření se uživatel přesměruje na adresu URL, kterou si původně požadoval.

Vzhledem k tomu, že cílová adresa URL je zadána v řetězci QueryString žádosti, může uživatel se zlými úmysly manipulovat s řetězcem dotazu. Neoprávněný řetězec QueryString může webovému serveru přesměrovat uživatele na externí, škodlivý web. Tato technika se nazývá otevřené útoky přesměrování (nebo přesměrování).

### <a name="an-example-attack"></a>Ukázkový útok

Uživatel se zlými úmysly může vyvíjet útok s cílem umožnit uživateli se zlými úmysly přístup k přihlašovacím údajům uživatele nebo citlivým informacím. Uživatel, který se zlými úmysly zahájí, uživatele přesvědčit, aby po kliknutí na odkaz na přihlašovací stránku vaší lokality s hodnotou `returnUrl` QueryString přidané do adresy URL. Zvažte například aplikaci na `contoso.com`, která obsahuje přihlašovací stránku na `http://contoso.com/Account/LogOn?returnUrl=/Home/About`. Útok se řídí těmito kroky:

1. Uživatel klikne na škodlivý odkaz `http://contoso.com/Account/LogOn?returnUrl=http://contoso1.com/Account/LogOn` (druhá adresa URL je contoso**1**. com ", nikoli" contoso.com ").
2. Uživatel se úspěšně přihlásil.
3. Uživatel se přesměruje (lokalitou) na `http://contoso1.com/Account/LogOn` (škodlivá lokalita, která vypadá přesně stejně jako skutečná lokalita).
4. Uživatel se znovu přihlásí (uvede přihlašovací údaje pro škodlivý web) a bude přesměrován zpět na skutečný Web.

Uživatel se nejspíš domnívá, že se první pokus o přihlášení nezdařil a že jejich druhý pokus je úspěšný. Uživatel pravděpodobně stále neví, že jejich přihlašovací údaje jsou ohroženy.

![Otevřít proces útoku přesměrování](preventing-open-redirects/_static/open-redirection-attack-process.png)

Kromě přihlašovacích stránek poskytují některé lokality stránky přesměrování nebo koncové body. Představte si, že vaše aplikace má stránku s otevřeným přesměrování `/Home/Redirect`. Útočník by mohl vytvořit například odkaz v e-mailu, který přejde na `[yoursite]/Home/Redirect?url=http://phishingsite.com/Home/Login`. Typický uživatel se podívá na adresu URL a zjistí, že začíná názvem vaší lokality. Důvěřujete to tím, že kliknete na odkaz. Otevřené přesměrování by pak poslalo uživateli na web útoku phishing, který vypadá stejně jako váš a uživatel se pravděpodobně přihlásí k tomu, co se domníváte, že se jedná o Web.

## <a name="protecting-against-open-redirect-attacks"></a>Ochrana před útoky typu otevřené přesměrování

Při vývoji webových aplikací zachází všechna uživatelsky zadaná data jako nedůvěryhodná. Pokud má vaše aplikace funkcionalitu, která přesměruje uživatele na základě obsahu adresy URL, zajistěte, aby se tyto přesměrování prováděly pouze místně v rámci aplikace (nebo na známou adresu URL, nikoli na adresu URL, která může být zadána v řetězci QueryString).

### <a name="localredirect"></a>LocalRedirect

Použijte pomocnou metodu `LocalRedirect` ze základní `Controller` třídy:

```csharp
public IActionResult SomeAction(string redirectUrl)
{
    return LocalRedirect(redirectUrl);
}
```

`LocalRedirect` vyvolá výjimku, pokud je zadána adresa URL, která není místní. V opačném případě se chová stejně jako metoda `Redirect`.

### <a name="islocalurl"></a>IsLocalUrl

Před přesměrováním otestujte adresy URL pomocí metody [IsLocalUrl](/dotnet/api/Microsoft.AspNetCore.Mvc.IUrlHelper.islocalurl#Microsoft_AspNetCore_Mvc_IUrlHelper_IsLocalUrl_System_String_) :

Následující příklad ukazuje, jak ověřit, zda je adresa URL místní před přesměrováním.

```csharp
private IActionResult RedirectToLocal(string returnUrl)
{
    if (Url.IsLocalUrl(returnUrl))
    {
        return Redirect(returnUrl);
    }
    else
    {
        return RedirectToAction(nameof(HomeController.Index), "Home");
    }
}
```

Metoda `IsLocalUrl` chrání uživatele před neúmyslným přesměrováním na škodlivý web. V případě, že jste očekávali místní adresu URL, můžete protokolovat podrobnosti adresy URL, které byly poskytnuty při zadání jiné než místní adresy URL. Protokolování adres URL pro přesměrování může pomáhat při diagnostice útoků přesměrování.
