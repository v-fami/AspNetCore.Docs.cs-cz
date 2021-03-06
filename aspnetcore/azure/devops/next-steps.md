---
title: Další kroky – DevOps s využitím ASP.NET Core a Azure
author: CamSoper
description: Další postupy výuky pro vývoj a provoz s ASP.NET Core a Azure.
ms.author: casoper
ms.custom: mvc, seodec18
ms.date: 10/24/2018
uid: azure/devops/next-steps
ms.openlocfilehash: a775dc42551a43bcce72b5f9ca364ed00b1dc4e6
ms.sourcegitcommit: 9a129f5f3e31cc449742b164d5004894bfca90aa
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78659472"
---
# <a name="next-steps"></a>Další kroky

V tomto průvodci vytvořit kanál DevOps pro ukázkové aplikace ASP.NET Core. Blahopřejeme! Doufáme, že se vám líbilo učení k publikování webových aplikací ASP.NET Core do služby Azure App Service a automatizovat průběžné integrace změny.

Kromě hostování webů a DevOps Azure nabízí širokou škálu služeb Platform-as-a-Service (PaaS) je užitečný pro vývojáře ASP.NET Core. Tato část poskytuje stručný přehled o některé z nejčastěji používaných služeb.

## <a name="storage-and-databases"></a>Úložiště a databází

[Redis Cache](/azure/redis-cache/) je k dispozici ukládání dat do mezipaměti s vysokou propustností a nízkou latencí jako služba. Je možné pro ukládání výstupu stránek, snížení požadavků na databázi a poskytování stavu relace ASP.NET Core do několika instancí aplikace.

[Azure Storage](/azure/storage/) je rozsáhle škálovatelné cloudové úložiště Azure. Vývojáři mohou využít výhod [Queue Storage](/azure/storage/queues/storage-queues-introduction) pro spolehlivé služby Řízení front zpráv a [Table Storage](/azure/storage/tables/table-storage-overview) je úložiště NoSQL klíč-hodnota navržené pro rychlý vývoj pomocí rozsáhlých, částečně strukturovaných datových sad.

[Azure SQL Database](/azure/sql-database/) poskytuje známé funkce relační databáze jako služba využívající modul Microsoft SQL Server.

[Cosmos DB](/azure/cosmos-db/) globálně distribuovaná databázová služba NoSQL pro více modelů. Několik rozhraní API jsou dostupná, včetně rozhraní SQL API (dříve se označovaly jako DocumentDB) a Cassandra, MongoDB.

## <a name="identity"></a>Identita

[Azure Active Directory](/azure/active-directory/) a [Azure Active Directory B2C](/azure/active-directory-b2c/) jsou obě služby identity. Azure Active Directory je určená pro podnikové scénáře a umožňuje spolupráci Azure AD B2B (business-to-business), zatímco Azure Active Directory B2C je zamýšlené firmy zákazníka scénářů, včetně přihlášení sociálních sítí.

## <a name="mobile"></a>Mobilní

[Notification Hubs](/azure/notification-hubs/) je Škálovatelný modul nabízených oznámení pro více platforem, který umožňuje rychle odesílat miliony zpráv aplikacím běžícím na různých typech zařízení.

## <a name="web-infrastructure"></a>Infrastruktura webové

[Azure Container Service](/azure/aks/) spravuje hostované prostředí Kubernetes, které umožňuje rychlé a snadné nasazení a správu kontejnerových aplikací bez znalosti orchestrace kontejnerů.

[Azure Search](/azure/search/) slouží k vytvoření podnikového řešení pro vyhledávání v rámci soukromého obsahu heterogenní.

[Service Fabric](/azure/service-fabric/) je platforma distribuovaných systémů usnadňující balení, nasazování a spravování škálovatelných a spolehlivých mikroslužeb a kontejnerů.
