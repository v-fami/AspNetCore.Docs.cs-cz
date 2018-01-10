---
title: "Povolení generování kód QR pro aplikace v ASP.NET Core"
author: rick-anderson
description: "Povolení generování kód QR pro aplikace v ASP.NET Core"
keywords: "Jádro ASP.NET, MVC, generování kód QR, authenticator, 2FA"
ms.author: riande
manager: wpickett
ms.date: 09/24/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/authentication/identity-enable-qrcodes
ms.openlocfilehash: a3029e68164dd91d1bc43704c5e96bd591bcae05
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/10/2017
---
# <a name="enabling-qr-code-generation-for-authenticator-apps-in-aspnet-core"></a><span data-ttu-id="afe04-104">Povolení generování kód QR pro aplikace v ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="afe04-104">Enabling QR Code generation for authenticator apps in ASP.NET Core</span></span>

<span data-ttu-id="afe04-105">Poznámka: Toto téma se vztahuje na ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="afe04-105">Note: This topic applies to ASP.NET Core 2.x</span></span>

<span data-ttu-id="afe04-106">ASP.NET Core se dodává s podporou pro ověřovací aplikací pro jednotlivé ověřování.</span><span class="sxs-lookup"><span data-stu-id="afe04-106">ASP.NET Core ships with support for authenticator applications for individual authentication.</span></span> <span data-ttu-id="afe04-107">Dva faktor ověřování (2FA), použití založené na čase jednorázové heslo algoritmus (TOTP), jsou tyto aplikace doporučenému přístupu pro 2FA odvětví.</span><span class="sxs-lookup"><span data-stu-id="afe04-107">Two factor authentication (2FA) authenticator apps, using a Time-based One-time Password Algorithm (TOTP), are the industry recommended approach for 2FA.</span></span> <span data-ttu-id="afe04-108">2FA pomocí TOTP je upřednostňovaný k 2FA serveru SMS.</span><span class="sxs-lookup"><span data-stu-id="afe04-108">2FA using TOTP is preferred to SMS 2FA.</span></span> <span data-ttu-id="afe04-109">Ověřovací aplikaci poskytuje 6 až 8 číslice kódu, které uživatelé musí zadat po potvrzení uživatelského jména a hesla.</span><span class="sxs-lookup"><span data-stu-id="afe04-109">An authenticator app provides a 6 to 8 digit code which users must enter after confirming their username and password.</span></span> <span data-ttu-id="afe04-110">Ověřovací aplikaci je obvykle nainstalován na Smartphone.</span><span class="sxs-lookup"><span data-stu-id="afe04-110">Typically an authenticator app is installed on a smart phone.</span></span>

<span data-ttu-id="afe04-111">Šablony webové aplikace ASP.NET Core podporovat ověřovací data, ale neposkytuje podporu pro generování QRCode.</span><span class="sxs-lookup"><span data-stu-id="afe04-111">The ASP.NET Core web app templates support authenticators, but do not provide support for QRCode generation.</span></span> <span data-ttu-id="afe04-112">Generátory QRCode usnadňují nastavení 2FA.</span><span class="sxs-lookup"><span data-stu-id="afe04-112">QRCode generators ease the setup of 2FA.</span></span> <span data-ttu-id="afe04-113">Tento dokument vás provede přidáním [kód QR](https://wikipedia.org/wiki/QR_code) generování na stránku konfigurace 2FA.</span><span class="sxs-lookup"><span data-stu-id="afe04-113">This document will guide you through adding [QR Code](https://wikipedia.org/wiki/QR_code) generation to the 2FA configuration page.</span></span>

## <a name="adding-qr-codes-to-the-2fa-configuration-page"></a><span data-ttu-id="afe04-114">Přidání kódy QR na stránku konfigurace 2FA</span><span class="sxs-lookup"><span data-stu-id="afe04-114">Adding QR Codes to the 2FA configuration page</span></span>

<span data-ttu-id="afe04-115">Tyto pokyny používají *qrcode.js* z https://davidshimjs.github.io/qrcodejs/ úložiště.</span><span class="sxs-lookup"><span data-stu-id="afe04-115">These instructions use *qrcode.js* from the https://davidshimjs.github.io/qrcodejs/ repo.</span></span>

* <span data-ttu-id="afe04-116">Stažení [knihovna javascript qrcode.js](https://davidshimjs.github.io/qrcodejs/) k `wwwroot\lib` složku ve vašem projektu.</span><span class="sxs-lookup"><span data-stu-id="afe04-116">Download the [qrcode.js javascript library](https://davidshimjs.github.io/qrcodejs/) to the `wwwroot\lib` folder in your project.</span></span>

* <span data-ttu-id="afe04-117">V *Pages\Account\Manage\EnableAuthenticator.cshtml* (stránky Razor) nebo *Views\Manage\EnableAuthenticator.cshtml* (MVC), vyhledejte `Scripts` na konci souboru:</span><span class="sxs-lookup"><span data-stu-id="afe04-117">In *Pages\Account\Manage\EnableAuthenticator.cshtml* (Razor Pages) or *Views\Manage\EnableAuthenticator.cshtml* (MVC), locate the `Scripts` section at the end of the file:</span></span>

```cshtml
@section Scripts {
    @await Html.PartialAsync("_ValidationScriptsPartial")
}
```

* <span data-ttu-id="afe04-118">Aktualizace `Scripts` části se přidat odkaz na `qrcodejs` knihovny, které jste přidali a volání generovat kód QR.</span><span class="sxs-lookup"><span data-stu-id="afe04-118">Update the `Scripts` section to add a reference to the `qrcodejs` library you added and a call to generate the QR Code.</span></span> <span data-ttu-id="afe04-119">By měla vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="afe04-119">It should look as follows:</span></span>

```cshtml
@section Scripts {
    @await Html.PartialAsync("_ValidationScriptsPartial")

    <script type="text/javascript" src="~/lib/qrcode.js"></script>
    <script type="text/javascript">
        new QRCode(document.getElementById("qrCode"),
            {
                text: "@Html.Raw(Model.AuthenticatorUri)",
                width: 150,
                height: 150
            });
    </script>
}
```

* <span data-ttu-id="afe04-120">Odstraňte odstavce, který odkazy na tyto pokyny.</span><span class="sxs-lookup"><span data-stu-id="afe04-120">Delete the paragraph which links you to these instructions.</span></span>

<span data-ttu-id="afe04-121">Spuštění aplikace a zkontrolujte, zda jste naskenujte kód QR a ověřit kód, který prokáže ověřovacích.</span><span class="sxs-lookup"><span data-stu-id="afe04-121">Run your app and ensure that you can scan the QR code and validate the code the authenticator proves.</span></span>

## <a name="change-the-site-name-in-the-qr-code"></a><span data-ttu-id="afe04-122">Změňte název webu v kód QR</span><span class="sxs-lookup"><span data-stu-id="afe04-122">Change the site name in the QR Code</span></span>

<span data-ttu-id="afe04-123">Název webu v kód QR je převzat ze název projektu, který si zvolíte při počátečním vytvoření projektu.</span><span class="sxs-lookup"><span data-stu-id="afe04-123">The site name in the QR Code is taken from the project name you choose when initially creating your project.</span></span> <span data-ttu-id="afe04-124">Můžete ji změnit tak, že vyhledá `GenerateQrCodeUri(string email, string unformattedKey)` metoda v *Pages\Account\Manage\EnableAuthenticator.cshtml.cs* souboru (stránky Razor) nebo *Controllers\ManageController.cs* (MVC) souboru.</span><span class="sxs-lookup"><span data-stu-id="afe04-124">You can change it by looking for the `GenerateQrCodeUri(string email, string unformattedKey)` method in the *Pages\Account\Manage\EnableAuthenticator.cshtml.cs* (Razor Pages) file or the *Controllers\ManageController.cs* (MVC) file.</span></span> 

<span data-ttu-id="afe04-125">Ve výchozím kódu ze šablony vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="afe04-125">The default code from the template looks as follows:</span></span>

```c#
private string GenerateQrCodeUri(string email, string unformattedKey)
{
    return string.Format(
        AuthenicatorUriFormat,
        _urlEncoder.Encode("Razor Pages"),
        _urlEncoder.Encode(email),
        unformattedKey);
}
```

<span data-ttu-id="afe04-126">Druhý parametr ve volání `string.Format` je název lokality, provedených od název řešení.</span><span class="sxs-lookup"><span data-stu-id="afe04-126">The second parameter in the call to `string.Format` is your site name, taken from your solution name.</span></span> <span data-ttu-id="afe04-127">Lze změnit na jakoukoli hodnotu, ale musí být vždycky kódovaná adresou URL.</span><span class="sxs-lookup"><span data-stu-id="afe04-127">It can be changed to any value, but it must always be URL encoded.</span></span>

## <a name="using-a-different-qr-code-library"></a><span data-ttu-id="afe04-128">Pomocí různých kód QR knihovny</span><span class="sxs-lookup"><span data-stu-id="afe04-128">Using a different QR Code library</span></span>

<span data-ttu-id="afe04-129">Kód QR knihovny můžete nahradit své upřednostňované knihovny.</span><span class="sxs-lookup"><span data-stu-id="afe04-129">You can replace the QR Code library with your preferred library.</span></span> <span data-ttu-id="afe04-130">Obsahuje kód HTML `qrCode` obsahuje element, do kterého můžete umístit kód QR podle jakýmkoli své knihovny.</span><span class="sxs-lookup"><span data-stu-id="afe04-130">The HTML contains a `qrCode` element into which you can place a QR Code by whatever mechanism your library provides.</span></span>

<span data-ttu-id="afe04-131">Je k dispozici v správně formátovaného adresa URL pro kód QR:</span><span class="sxs-lookup"><span data-stu-id="afe04-131">The correctly formatted URL for the QR Code is available in the:</span></span>

* <span data-ttu-id="afe04-132">`AuthenticatorUri`Vlastnost modelu.</span><span class="sxs-lookup"><span data-stu-id="afe04-132">`AuthenticatorUri` property of the model.</span></span>
* <span data-ttu-id="afe04-133">`data-url`Vlastnost `qrCodeData` elementu.</span><span class="sxs-lookup"><span data-stu-id="afe04-133">`data-url` property in the `qrCodeData` element.</span></span> 

<span data-ttu-id="afe04-134">Použití `@Html.Raw` pro přístup k vlastnosti modelu v zobrazení (jinak bude double kódovaný ampersandy v adrese url a budou se ignorovat parametr label kód QR).</span><span class="sxs-lookup"><span data-stu-id="afe04-134">Use `@Html.Raw` to access the model property in a view (otherwise the ampersands in the url will be double encoded and the label parameter of the QR Code will be ignored).</span></span>

## <a name="totp-client-and-server-time-skew"></a><span data-ttu-id="afe04-135">TOTP klientských a serverových čas zkosení</span><span class="sxs-lookup"><span data-stu-id="afe04-135">TOTP client and server time skew</span></span>

<span data-ttu-id="afe04-136">Ověření TOTP závisí na serveru a ověřovací zařízení má přesnému času.</span><span class="sxs-lookup"><span data-stu-id="afe04-136">TOTP authentication depends on both the server and authenticator device having an accurate time.</span></span> <span data-ttu-id="afe04-137">Tokeny pouze trvat 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="afe04-137">Tokens only last for 30 seconds.</span></span> <span data-ttu-id="afe04-138">Pokud se nedaří přihlášení 2FA TOTP, zkontrolujte, jestli čas serveru přesné a pokud možno synchronizovány s služby přesné NTP.</span><span class="sxs-lookup"><span data-stu-id="afe04-138">If TOTP 2FA logins are failing, check that the server time is accurate, and preferably synchronized to an accurate NTP service.</span></span>