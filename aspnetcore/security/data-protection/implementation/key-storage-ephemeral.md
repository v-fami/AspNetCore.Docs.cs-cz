---
title: Zprostředkovatelé dočasné ochrany dat v ASP.NET Core
author: rick-anderson
description: Přečtěte si podrobnosti o implementaci ASP.NET Core zprostředkovatelů ochrany před dočasnými daty.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/implementation/key-storage-ephemeral
ms.openlocfilehash: e4b0014ab3bdbf90b91383e8a33102f94faa8153
ms.sourcegitcommit: 9a129f5f3e31cc449742b164d5004894bfca90aa
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78664736"
---
# <a name="ephemeral-data-protection-providers-in-aspnet-core"></a>Zprostředkovatelé dočasné ochrany dat v ASP.NET Core

<a name="data-protection-implementation-key-storage-ephemeral"></a>

Existují situace, kdy aplikace potřebuje throwaway `IDataProtectionProvider`. Vývojář může například experimentovat pouze v jednorázových konzolových aplikacích, nebo je samotná aplikace přechodná (je to skriptový projekt nebo test jednotky). Pro podporu těchto scénářů obsahuje balíček [Microsoft. AspNetCore. DataProtection](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection/) typ `EphemeralDataProtectionProvider`. Tento typ poskytuje základní implementaci `IDataProtectionProvider`, jejichž úložiště klíčů je uchováváno pouze v paměti a není zapsáno do žádného záložního úložiště.

Každá instance `EphemeralDataProtectionProvider` používá vlastní jedinečný hlavní klíč. Proto pokud `IDataProtector` rootem v `EphemeralDataProtectionProvider` vygeneruje chráněnou datovou část, může být tato datová část chráněná jenom ekvivalentním `IDataProtector` (pro stejný řetěz [účelu](xref:security/data-protection/consumer-apis/purpose-strings#data-protection-consumer-apis-purposes) ), která se zadává na stejné `EphemeralDataProtectionProvider` instanci.

Následující příklad ukazuje vytvoření instance `EphemeralDataProtectionProvider` a její použití k ochraně a neochraně dat.

```csharp
using System;
using Microsoft.AspNetCore.DataProtection;

public class Program
{
    public static void Main(string[] args)
    {
        const string purpose = "Ephemeral.App.v1";

        // create an ephemeral provider and demonstrate that it can round-trip a payload
        var provider = new EphemeralDataProtectionProvider();
        var protector = provider.CreateProtector(purpose);
        Console.Write("Enter input: ");
        string input = Console.ReadLine();

        // protect the payload
        string protectedPayload = protector.Protect(input);
        Console.WriteLine($"Protect returned: {protectedPayload}");

        // unprotect the payload
        string unprotectedPayload = protector.Unprotect(protectedPayload);
        Console.WriteLine($"Unprotect returned: {unprotectedPayload}");

        // if I create a new ephemeral provider, it won't be able to unprotect existing
        // payloads, even if I specify the same purpose
        provider = new EphemeralDataProtectionProvider();
        protector = provider.CreateProtector(purpose);
        unprotectedPayload = protector.Unprotect(protectedPayload); // THROWS
    }
}

/*
* SAMPLE OUTPUT
*
* Enter input: Hello!
* Protect returned: CfDJ8AAAAAAAAAAAAAAAAAAAAA...uGoxWLjGKtm1SkNACQ
* Unprotect returned: Hello!
* << throws CryptographicException >>
*/
```
