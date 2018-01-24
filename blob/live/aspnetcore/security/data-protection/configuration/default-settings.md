---
title: "Správa klíčů ochrany dat a doba platnosti v ASP.NET Core"
author: rick-anderson
description: "Další informace o ochranu dat správy klíčů a doba platnosti v ASP.NET Core."
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/configuration/default-settings
ms.openlocfilehash: 0993c68e37944a3aad863b98f92fe0140cfb746d
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/19/2018
---
# <a name="data-protection-key-management-and-lifetime-in-aspnet-core"></a><span data-ttu-id="60703-103">Správa klíčů ochrany dat a doba platnosti v ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="60703-103">Data Protection key management and lifetime in ASP.NET Core</span></span>

<span data-ttu-id="60703-104">Podle [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="60703-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

## <a name="key-management"></a><span data-ttu-id="60703-105">Správa klíčů</span><span class="sxs-lookup"><span data-stu-id="60703-105">Key management</span></span>

<span data-ttu-id="60703-106">Aplikace se pokusí zjistit jeho provozní prostředí a zpracování konfigurace klíče svoje vlastní.</span><span class="sxs-lookup"><span data-stu-id="60703-106">The app attempts to detect its operational environment and handle key configuration on its own.</span></span>

1. <span data-ttu-id="60703-107">Pokud je aplikace hostovaná v [Azure Apps](https://azure.microsoft.com/services/app-service/), klíče jsou nastavené jako trvalé k *%HOME%\ASP.NET\DataProtection-Keys* složky.</span><span class="sxs-lookup"><span data-stu-id="60703-107">If the app is hosted in [Azure Apps](https://azure.microsoft.com/services/app-service/), keys are persisted to the *%HOME%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="60703-108">Tato složka je zálohovaný díky síťového úložiště a se synchronizují napříč všechny počítače, které hostují aplikaci.</span><span class="sxs-lookup"><span data-stu-id="60703-108">This folder is backed by network storage and is synchronized across all machines hosting the app.</span></span>
   * <span data-ttu-id="60703-109">Klíče nejsou chráněné v klidovém stavu.</span><span class="sxs-lookup"><span data-stu-id="60703-109">Keys aren't protected at rest.</span></span>
   * <span data-ttu-id="60703-110">*DataProtection klíče* složky poskytuje prstenec klíč na všechny instance aplikace v jednom nasazovací slot.</span><span class="sxs-lookup"><span data-stu-id="60703-110">The *DataProtection-Keys* folder supplies the key ring to all instances of an app in a single deployment slot.</span></span>
   * <span data-ttu-id="60703-111">Samostatné nasazovací sloty, jako je například pracovní a provozní, Nesdílejte prstenec klíč.</span><span class="sxs-lookup"><span data-stu-id="60703-111">Separate deployment slots, such as Staging and Production, don't share a key ring.</span></span> <span data-ttu-id="60703-112">Při výměně mezi sloty nasazení, například odkládací pracovní do produkčního prostředí nebo použití A / B testování, všech aplikací pomocí funkce Ochrana dat nebude moci dešifrovat uložená data pomocí klíče prstenec uvnitř předchozí pozici.</span><span class="sxs-lookup"><span data-stu-id="60703-112">When you swap between deployment slots, for example swapping Staging to Production or using A/B testing, any app using Data Protection won't be able to decrypt stored data using the key ring inside the previous slot.</span></span> <span data-ttu-id="60703-113">To vede k uživatelé protokolována mimo aplikaci, která používá standardní ověřování souborů cookie ASP.NET Core, protože využívá ochranu dat k ochraně jeho soubory cookie.</span><span class="sxs-lookup"><span data-stu-id="60703-113">This leads to users being logged out of an app that uses the standard ASP.NET Core cookie authentication, as it uses Data Protection to protect its cookies.</span></span> <span data-ttu-id="60703-114">Vyžadujete, aby okruhy klíč nezávislé na pozici,-li použít zprostředkovatel vnější prstenec klíč, například Azure Blob Storage, Azure Key Vault, úložiště SQL nebo Redis cache.</span><span class="sxs-lookup"><span data-stu-id="60703-114">If you desire slot-independent key rings, use an external key ring provider, such as Azure Blob Storage, Azure Key Vault, a SQL store, or Redis cache.</span></span>

1. <span data-ttu-id="60703-115">Pokud profil uživatele je k dispozici, klíče, jsou nastavené jako trvalé k *%LOCALAPPDATA%\ASP.NET\DataProtection-Keys* složky.</span><span class="sxs-lookup"><span data-stu-id="60703-115">If the user profile is available, keys are persisted to the *%LOCALAPPDATA%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="60703-116">Pokud operační systém Windows, klíče jsou zašifrovaná přinejmenším pomocí rozhraní DPAPI.</span><span class="sxs-lookup"><span data-stu-id="60703-116">If the operating system is Windows, the keys are encrypted at rest using DPAPI.</span></span>

1. <span data-ttu-id="60703-117">Pokud je aplikace hostované ve službě IIS, jsou trvalé klíče registru HKLM klíč speciální registru, který je ACLed pouze pro účet pracovního procesu.</span><span class="sxs-lookup"><span data-stu-id="60703-117">If the app is hosted in IIS, keys are persisted to the HKLM registry in a special registry key that is ACLed only to the worker process account.</span></span> <span data-ttu-id="60703-118">Klíče jsou zašifrovaná přinejmenším pomocí rozhraní DPAPI.</span><span class="sxs-lookup"><span data-stu-id="60703-118">Keys are encrypted at rest using DPAPI.</span></span>

1. <span data-ttu-id="60703-119">Pokud žádná z těchto podmínek shodují, klíče nejsou trvalé mimo aktuální proces.</span><span class="sxs-lookup"><span data-stu-id="60703-119">If none of these conditions match, keys aren't persisted outside of the current process.</span></span> <span data-ttu-id="60703-120">Když se proces ukončí, všechny vygenerované klíče jsou ztraceny.</span><span class="sxs-lookup"><span data-stu-id="60703-120">When the process shuts down, all generated keys are lost.</span></span>

<span data-ttu-id="60703-121">Vývojář je vždy plně pod kontrolou a můžete přepsat, jak a kde jsou uložené klíče.</span><span class="sxs-lookup"><span data-stu-id="60703-121">The developer is always in full control and can override how and where keys are stored.</span></span> <span data-ttu-id="60703-122">První tři výše uvedených možností by měl poskytovat dobrý výchozí hodnoty pro většinu aplikací podobná jak ASP.NET  **\<machineKey >** automatické generování rutiny fungovaly v minulosti.</span><span class="sxs-lookup"><span data-stu-id="60703-122">The first three options above should provide good defaults for most apps similar to how the ASP.NET **\<machineKey>** auto-generation routines worked in the past.</span></span> <span data-ttu-id="60703-123">Možnost konečné, záložní je jenom scénáře, který vyžaduje vývojáři zadejte [konfigurace](xref:security/data-protection/configuration/overview) předem, pokud chtějí klíče trvalost, ale tento záložní dochází pouze ve výjimečných případech.</span><span class="sxs-lookup"><span data-stu-id="60703-123">The final, fallback option is the only scenario that requires the developer to specify [configuration](xref:security/data-protection/configuration/overview) upfront if they want key persistence, but this fallback only occurs in rare situations.</span></span>

<span data-ttu-id="60703-124">Při hostování v kontejner Docker, klíče by měl natrvalo ve složce, kterou je svazek Docker (sdíleného svazku nebo svazku připojené hostitele, který potrvají nad rámec kontejneru životnost) nebo do externího poskytovatele, jako například [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) nebo [Redis](https://redis.io/).</span><span class="sxs-lookup"><span data-stu-id="60703-124">When hosting in a Docker container, keys should be persisted in a folder that's a Docker volume (a shared volume or a host-mounted volume that persists beyond the container's lifetime) or in an external provider, such as [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) or [Redis](https://redis.io/).</span></span> <span data-ttu-id="60703-125">Externího poskytovatele je užitečný ve scénářích, webové farmy také pokud aplikace nemá přístup k sdílené síťové svazek (viz [PersistKeysToFileSystem](xref:security/data-protection/configuration/overview#persistkeystofilesystem) informace).</span><span class="sxs-lookup"><span data-stu-id="60703-125">An external provider is also useful in web farm scenarios if apps can't access a shared network volume (see [PersistKeysToFileSystem](xref:security/data-protection/configuration/overview#persistkeystofilesystem) for more information).</span></span>

> [!WARNING]
> <span data-ttu-id="60703-126">Pokud vývojář přepsání pravidel uvedených výše a bodů systému ochrany dat na konkrétní úložiště klíčů, je zakázané automatické šifrování klíče v klidovém stavu.</span><span class="sxs-lookup"><span data-stu-id="60703-126">If the developer overrides the rules outlined above and points the Data Protection system at a specific key repository, automatic encryption of keys at rest is disabled.</span></span> <span data-ttu-id="60703-127">Může být znovu zapnout ochranu v rest [konfigurace](xref:security/data-protection/configuration/overview).</span><span class="sxs-lookup"><span data-stu-id="60703-127">At-rest protection can be re-enabled via [configuration](xref:security/data-protection/configuration/overview).</span></span>

## <a name="key-lifetime"></a><span data-ttu-id="60703-128">Doba platnosti klíče</span><span class="sxs-lookup"><span data-stu-id="60703-128">Key lifetime</span></span>

<span data-ttu-id="60703-129">Klíče měly životnost-90denní ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="60703-129">Keys have a 90-day lifetime by default.</span></span> <span data-ttu-id="60703-130">Když vyprší platnost klíče, aplikace se automaticky vygeneruje nový klíč a nastaví nového klíče jako aktivní klíč.</span><span class="sxs-lookup"><span data-stu-id="60703-130">When a key expires, the app automatically generates a new key and sets the new key as the active key.</span></span> <span data-ttu-id="60703-131">Tak dlouho, dokud vyřazeno klíče zůstávají v systému, aplikace mohly dešifrovat všechna data chráněná s nimi.</span><span class="sxs-lookup"><span data-stu-id="60703-131">As long as retired keys remain on the system, your app can decrypt any data protected with them.</span></span> <span data-ttu-id="60703-132">V tématu [Správa klíčů](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling) Další informace.</span><span class="sxs-lookup"><span data-stu-id="60703-132">See [key management](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling) for more information.</span></span>

## <a name="default-algorithms"></a><span data-ttu-id="60703-133">Výchozí algoritmy</span><span class="sxs-lookup"><span data-stu-id="60703-133">Default algorithms</span></span>

<span data-ttu-id="60703-134">Použitý algoritmus ochrany výchozí datové části pro utajení a HMACSHA256 je AES-256-CBC pro pravosti.</span><span class="sxs-lookup"><span data-stu-id="60703-134">The default payload protection algorithm used is AES-256-CBC for confidentiality and HMACSHA256 for authenticity.</span></span> <span data-ttu-id="60703-135">Hlavní klíč 512 bitů, změnit každých 90 dní, slouží k dvě dílčí klíče používané pro tyto algoritmy na základě za datové odvozena.</span><span class="sxs-lookup"><span data-stu-id="60703-135">A 512-bit master key, changed every 90 days, is used to derive the two sub-keys used for these algorithms on a per-payload basis.</span></span> <span data-ttu-id="60703-136">V tématu [podklíčů odvození](xref:security/data-protection/implementation/subkeyderivation#additional-authenticated-data-and-subkey-derivation) Další informace.</span><span class="sxs-lookup"><span data-stu-id="60703-136">See [subkey derivation](xref:security/data-protection/implementation/subkeyderivation#additional-authenticated-data-and-subkey-derivation) for more information.</span></span>

## <a name="see-also"></a><span data-ttu-id="60703-137">Viz také</span><span class="sxs-lookup"><span data-stu-id="60703-137">See also</span></span>

* [<span data-ttu-id="60703-138">Rozšiřitelnost správy klíčů</span><span class="sxs-lookup"><span data-stu-id="60703-138">Key management extensibility</span></span>](xref:security/data-protection/extensibility/key-management)