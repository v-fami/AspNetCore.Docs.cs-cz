---
uid: signalr/overview/security/persistent-connection-authorization
title: "Ověřování a autorizace pro trvalé připojení SignalR | Microsoft Docs"
author: pfletcher
description: "Toto téma popisuje, jak vynutit autorizaci u na trvalé připojení. Obecné informace o integraci do aplikace pomocí SignalR zabezpečení..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: e264677b-9c01-47ec-94f9-3cd8f08f94af
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/security/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 9c6fff86ae6b1b65e6ba9922b6b8448643ef1f15
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/10/2017
---
<a name="authentication-and-authorization-for-signalr-persistent-connections"></a><span data-ttu-id="df8f8-104">Ověřování a autorizace pro trvalé připojení SignalR</span><span class="sxs-lookup"><span data-stu-id="df8f8-104">Authentication and Authorization for SignalR Persistent Connections</span></span>
====================
<span data-ttu-id="df8f8-105">podle [Patrik Fletcher](https://github.com/pfletcher), [tní FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="df8f8-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="df8f8-106">Toto téma popisuje, jak vynutit autorizaci u na trvalé připojení.</span><span class="sxs-lookup"><span data-stu-id="df8f8-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="df8f8-107">Obecné informace o integraci zabezpečení do aplikace SignalR najdete v tématu [Úvod k zabezpečení](introduction-to-security.md).</span><span class="sxs-lookup"><span data-stu-id="df8f8-107">For general information about integrating security into a SignalR application, see [Introduction to Security](introduction-to-security.md).</span></span> 
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="df8f8-108">Verze softwaru použitým v tomto tématu</span><span class="sxs-lookup"><span data-stu-id="df8f8-108">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="df8f8-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="df8f8-109">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="df8f8-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="df8f8-110">.NET 4.5</span></span>
> - <span data-ttu-id="df8f8-111">SignalR verze 2</span><span class="sxs-lookup"><span data-stu-id="df8f8-111">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="df8f8-112">Předchozí verze tohoto tématu</span><span class="sxs-lookup"><span data-stu-id="df8f8-112">Previous versions of this topic</span></span>
> 
> <span data-ttu-id="df8f8-113">Informace o předchozích verzích SignalR najdete v tématu [starší verze funkce SignalR](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="df8f8-113">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="df8f8-114">Dotazy a připomínky</span><span class="sxs-lookup"><span data-stu-id="df8f8-114">Questions and comments</span></span>
> 
> <span data-ttu-id="df8f8-115">Prosím sdělit svůj názor na tom, jak líbilo tohoto kurzu a co jsme může zlepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="df8f8-115">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="df8f8-116">Pokud máte otázky, které přímo nesouvisejí s kurz, můžete je do příspěvku [fórum pro ASP.NET SignalR](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="df8f8-116">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="enforce-authorization"></a><span data-ttu-id="df8f8-117">Vynutit autorizaci</span><span class="sxs-lookup"><span data-stu-id="df8f8-117">Enforce authorization</span></span>

<span data-ttu-id="df8f8-118">K vynucení pravidel autorizace při použití [připojení PersistentConnection](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) je nutné přepsat `AuthorizeRequest` metoda.</span><span class="sxs-lookup"><span data-stu-id="df8f8-118">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/en-us/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="df8f8-119">Nelze použít `Authorize` atribut s trvalým připojením.</span><span class="sxs-lookup"><span data-stu-id="df8f8-119">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="df8f8-120">`AuthorizeRequest` Metoda je volána rámcem SignalR před každým požadavkem k ověření, že uživatel má oprávnění provést požadovanou akci.</span><span class="sxs-lookup"><span data-stu-id="df8f8-120">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="df8f8-121">`AuthorizeRequest` Metoda není volána z klienta; místo toho ověření uživatele prostřednictvím mechanismu standardní ověřování vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="df8f8-121">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="df8f8-122">Následující příklad ukazuje, jak omezit požadavky na ověření uživatelé.</span><span class="sxs-lookup"><span data-stu-id="df8f8-122">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="df8f8-123">Můžete přidat všechny přizpůsobené autorizace logiku v metodě AuthorizeRequest; například kontrola, zda uživatel patří do určité role.</span><span class="sxs-lookup"><span data-stu-id="df8f8-123">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>