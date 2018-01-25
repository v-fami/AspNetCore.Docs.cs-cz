---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
title: "Data dělení strategie (vytváření reálných cloudových aplikací s Azure) | Microsoft Docs"
author: MikeWasson
description: "Cloudové aplikace skutečné World sestavení s Azure elektronická kniha je založena na prezentace vyvinuté Scott Guthrie. Vysvětluje 13 vzory a postupy, které můžete mu..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: 513837a7-cfea-4568-a4e9-1f5901245d24
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-partitioning-strategies
msc.type: authoredcontent
ms.openlocfilehash: 8eddb7af2d9032153b30ab54d5e882f0b46cd4ce
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/10/2017
---
<a name="data-partitioning-strategies-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="d30f5-104">Data dělení strategie (vytváření reálných cloudových aplikací s Azure)</span><span class="sxs-lookup"><span data-stu-id="d30f5-104">Data Partitioning Strategies (Building Real-World Cloud Apps with Azure)</span></span>
====================
<span data-ttu-id="d30f5-105">podle [Karel Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [tní Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="d30f5-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="d30f5-106">[Stažení opravit projektu](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stáhnout elektronická kniha](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="d30f5-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="d30f5-107">**Vytváření reálného světa cloudových aplikací s Azure** elektronická kniha je založena na prezentaci vyvinuté Scott Guthrie.</span><span class="sxs-lookup"><span data-stu-id="d30f5-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="d30f5-108">Vysvětluje 13 vzory a postupy, které vám mohou pomoci být úspěšná, vývoj webových aplikací pro cloud.</span><span class="sxs-lookup"><span data-stu-id="d30f5-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="d30f5-109">Informace o řadě najdete v tématu [první kapitoly](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d30f5-109">For information about the series, see [the first chapter](introduction.md).</span></span>


<span data-ttu-id="d30f5-110">Dříve jsme viděli, jak je snadné škálování se webová úroveň cloudové aplikace, přidávání a odebírání webových serverů.</span><span class="sxs-lookup"><span data-stu-id="d30f5-110">Earlier we saw how easy it is to scale the web tier of a cloud application, by adding and removing web servers.</span></span> <span data-ttu-id="d30f5-111">Ale pokud budou se všechny stiskne stejné úložiště dat, kritické aplikace místo přesune z front-endu na back-end a datovou vrstvou je nejtěžší škálování.</span><span class="sxs-lookup"><span data-stu-id="d30f5-111">But if they're all hitting the same data store, your application's bottleneck moves from the front-end to the back-end, and the data tier is the hardest to scale.</span></span> <span data-ttu-id="d30f5-112">V této kapitole podíváme na způsob provádění datové vrstvy škálovatelné dělení dat do několika relačních databází, nebo kombinací relační databáze úložiště s jinými možnostmi datového úložiště.</span><span class="sxs-lookup"><span data-stu-id="d30f5-112">In this chapter we look at how you can make your data tier scalable by partitioning data into multiple relational databases, or by combining relational database storage with other data storage options.</span></span>

<span data-ttu-id="d30f5-113">Nastavení schéma rozdělení oddílů je nejvhodnější done až přední ze stejného důvodu již bylo zmíněno dříve: je velmi obtížné změnit strategie úložiště dat po aplikaci v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="d30f5-113">Setting up a partitioning scheme is best done up front for the same reason mentioned earlier: it's very difficult to change your data storage strategy after an app is in production.</span></span> <span data-ttu-id="d30f5-114">Pokud si myslíte, pevné předem o různý přístup, nemusíte mít "Twitter chvíli" Pokud vaše aplikace dojde k chybě nebo přestane fungovat po dlouhou dobu, během reorganizovat data a data přístupového kódu vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="d30f5-114">If you think hard up front about different approaches, you can avoid having a "Twitter moment" when your app crashes or goes down for a long time while you reorganize your app's data and data access code.</span></span>

## <a name="the-three-vs-of-data-storage"></a><span data-ttu-id="d30f5-115">Tři Vs úložiště dat</span><span class="sxs-lookup"><span data-stu-id="d30f5-115">The three Vs of data storage</span></span>

<span data-ttu-id="d30f5-116">Aby bylo možné zjistit, zda je nutné strategie dělení a co by měl být, vezměte v úvahu tři otázky týkající se vašich dat:</span><span class="sxs-lookup"><span data-stu-id="d30f5-116">In order to determine whether you need a partitioning strategy and what it should be, consider three questions about your data:</span></span>

- <span data-ttu-id="d30f5-117">Nakonec svazek – kolik dat bude můžete uložit?</span><span class="sxs-lookup"><span data-stu-id="d30f5-117">Volume – How much data will you ultimately store?</span></span> <span data-ttu-id="d30f5-118">Několik gigabajtů?</span><span class="sxs-lookup"><span data-stu-id="d30f5-118">A couple gigabytes?</span></span> <span data-ttu-id="d30f5-119">Několik set gigabajtů?</span><span class="sxs-lookup"><span data-stu-id="d30f5-119">A couple hundred gigabytes?</span></span> <span data-ttu-id="d30f5-120">Terabajtů?</span><span class="sxs-lookup"><span data-stu-id="d30f5-120">Terabytes?</span></span> <span data-ttu-id="d30f5-121">Petabajty?</span><span class="sxs-lookup"><span data-stu-id="d30f5-121">Petabytes?</span></span>
- <span data-ttu-id="d30f5-122">Rychlosti – co je rychlost, jakou se zvýší data?</span><span class="sxs-lookup"><span data-stu-id="d30f5-122">Velocity – What is the rate at which your data will grow?</span></span> <span data-ttu-id="d30f5-123">Je interní aplikace, která není generování velké množství dat?</span><span class="sxs-lookup"><span data-stu-id="d30f5-123">Is it an internal app that isn't generating a lot of data?</span></span> <span data-ttu-id="d30f5-124">Externí aplikaci, která zákazníků se nahrávání, bitové kopie a videa do?</span><span class="sxs-lookup"><span data-stu-id="d30f5-124">An external app that customers will be uploading images and videos into?</span></span>
- <span data-ttu-id="d30f5-125">Různé – co typ dat bude ukládat?</span><span class="sxs-lookup"><span data-stu-id="d30f5-125">Variety – What type of data will you store?</span></span> <span data-ttu-id="d30f5-126">Relační, obrázky, páry klíč hodnota, sociálních grafy?</span><span class="sxs-lookup"><span data-stu-id="d30f5-126">Relational, images, key-value pairs, social graphs?</span></span>

<span data-ttu-id="d30f5-127">Pokud si myslíte, že budete mít mnoho svazku, rychlosti nebo různých, budete muset pečlivě zvažte, jaký druh schéma rozdělení oddílů bude nejlépe povolení škálování efektivně a efektivně roste a zajistit nespouští do kritické body, které v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="d30f5-127">If you think you're going to have a lot of volume, velocity, or variety, you have to carefully consider what kind of partitioning scheme will best enable your app to scale efficiently and effectively as it grows, and to ensure you don't run into any bottlenecks.</span></span>

<span data-ttu-id="d30f5-128">V podstatě existují tři přístupy k vytváření oddílů:</span><span class="sxs-lookup"><span data-stu-id="d30f5-128">There are basically three approaches to partitioning:</span></span>

- <span data-ttu-id="d30f5-129">Vertikální dělení</span><span class="sxs-lookup"><span data-stu-id="d30f5-129">Vertical partitioning</span></span>
- <span data-ttu-id="d30f5-130">vodorovné rozdělení do oddílů</span><span class="sxs-lookup"><span data-stu-id="d30f5-130">Horizontal partitioning</span></span>
- <span data-ttu-id="d30f5-131">Hybridní dělení</span><span class="sxs-lookup"><span data-stu-id="d30f5-131">Hybrid partitioning</span></span>

## <a name="vertical-partitioning"></a><span data-ttu-id="d30f5-132">Vertikální dělení</span><span class="sxs-lookup"><span data-stu-id="d30f5-132">Vertical partitioning</span></span>

<span data-ttu-id="d30f5-133">Svislé rozporcování je jako rozdělení tabulky podle sloupců: jednu sadu sloupců přejde do jednoho datového úložiště, a jinou sadu sloupců přejde do jiné datové úložiště.</span><span class="sxs-lookup"><span data-stu-id="d30f5-133">Vertical portioning is like splitting up a table by columns: one set of columns goes into one data store, and another set of columns goes into a different data store.</span></span>

<span data-ttu-id="d30f5-134">Předpokládejme například, že Moje aplikace ukládá data o uživatelům, včetně bitové kopie:</span><span class="sxs-lookup"><span data-stu-id="d30f5-134">For example, suppose my app stores data about people, including images:</span></span>

![Datová tabulka](data-partitioning-strategies/_static/image1.png)

<span data-ttu-id="d30f5-136">Pokud představují tato data jako tabulku a podívejte se na různé typy dat, můžete zobrazit mít tři sloupce na levé straně řetězec data, která může být efektivně uložená relační databázi, zatímco dva sloupce na pravé straně jsou v podstatě bajtová pole tohoto jazyka c Domů z bitové kopie souborů.</span><span class="sxs-lookup"><span data-stu-id="d30f5-136">When you represent this data as a table and look at the different varieties of data, you can see that the three columns on the left have string data that can be efficiently stored by a relational database, while the two columns on the right are essentially byte arrays that come from image files.</span></span> <span data-ttu-id="d30f5-137">Je možné do úložiště bitové kopie souboru dat v relační databázi, a velké množství uživatelů provést, protože nemusíte chtít uložit data do systému souborů.</span><span class="sxs-lookup"><span data-stu-id="d30f5-137">It's possible to storage image file data in a relational database, and a lot of people do that because they don't want to save the data to the file system.</span></span> <span data-ttu-id="d30f5-138">Nemusejí mít umožňující ukládání požadované objemů dat systému souborů nebo nemusí chtějí spravovat samostatný zálohování a obnovení systému.</span><span class="sxs-lookup"><span data-stu-id="d30f5-138">They might not have a file system capable of storing the required volumes of data or they might not want to manage a separate back-up and restore system.</span></span> <span data-ttu-id="d30f5-139">Tento postup funguje i pro místní databáze a pro malé množství dat v databázích cloudu.</span><span class="sxs-lookup"><span data-stu-id="d30f5-139">This approach works well for on-premises databases and for small amounts of data in cloud databases.</span></span> <span data-ttu-id="d30f5-140">V místním prostředí může být snazší právě umožníte postará o všechno, co správce databáze.</span><span class="sxs-lookup"><span data-stu-id="d30f5-140">In the on-premises environment, it might be easier to just let the DBA take care of everything.</span></span>

<span data-ttu-id="d30f5-141">Ale v databázi cloudové úložiště je poměrně drahé a k velkému počtu bitové kopie může zkontrolujte velikost databáze růst mimo hranice, na kterých se mohou pracovat efektivně.</span><span class="sxs-lookup"><span data-stu-id="d30f5-141">But in a cloud database, storage is relatively expensive, and a high volume of images could make the size of the database grow beyond the limits at which it can operate efficiently.</span></span> <span data-ttu-id="d30f5-142">Tyto problémy můžete vyřešit tak, že dělení dat ve svislém směru, což znamená, že si vyberete nejvhodnější úložiště dat pro každý sloupec v tabulce dat.</span><span class="sxs-lookup"><span data-stu-id="d30f5-142">You can address these problems by partitioning the data vertically, which means you choose the most appropriate data store for each column in your table of data.</span></span> <span data-ttu-id="d30f5-143">Co může být nejvhodnější v tomto příkladu je uvést dat řetězců v relační databázi a obrázků v úložišti objektů Blob.</span><span class="sxs-lookup"><span data-stu-id="d30f5-143">What might work best for this example is to put the string data in a relational database and the images in Blob storage.</span></span>

![Datová tabulka svisle na oddíly](data-partitioning-strategies/_static/image2.png)

<span data-ttu-id="d30f5-145">Ukládání bitových kopií v úložišti objektů Blob místo databáze je praktičtější v cloudu než v místním prostředí, protože nemusíte si dělat starosti o nastavení souborových serverů nebo Správa zálohování a obnovení data uložená mimo relační databáze: všechny který zpracovává pro vás automaticky službu úložiště objektů Blob.</span><span class="sxs-lookup"><span data-stu-id="d30f5-145">Storing images in Blob storage instead of a database is more practical in the cloud than in an on-premises environment because you don't have to worry about setting up file servers or managing back-up and restore of data stored outside of the relational database: all that is handled for you automatically by the Blob storage service.</span></span>

<span data-ttu-id="d30f5-146">Jedná se o rozdělení postup implementovali jsme v aplikaci opravit a podíváme kód pro tento v [kapitoly úložiště objektů Blob](unstructured-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="d30f5-146">This is the partitioning approach we implemented in the Fix It app, and we'll look at the code for that in the [Blob storage chapter](unstructured-blob-storage.md).</span></span> <span data-ttu-id="d30f5-147">Bez této schéma rozdělení oddílů a za předpokladu, že obrázku průměrnou velikost 3 MB aplikace opravit pouze budou moct pro ukládání o 40 000 úloh před stiskne maximální velikost 150 gigabajtů.</span><span class="sxs-lookup"><span data-stu-id="d30f5-147">Without this partitioning scheme, and assuming an average image size of 3 megabytes, the Fix It app would only be able to store about 40,000 tasks before hitting the maximum database size of 150 gigabytes.</span></span> <span data-ttu-id="d30f5-148">Po odebrání bitové kopie, můžete ukládat databázi 10 třikrát tolik úlohy; můžete přejít déle, než bude nutné myslíte o implementaci vodorovné schéma rozdělení oddílů.</span><span class="sxs-lookup"><span data-stu-id="d30f5-148">After removing the images, the database can store 10 times as many tasks; you can go much longer before you have to think about implementing a horizontal partitioning scheme.</span></span> <span data-ttu-id="d30f5-149">A jako aplikace škáluje, vaše výdaje zvýší pomalejší, protože hromadným požadavky na ukládání budou do velmi nenákladné úložiště objektů Blob.</span><span class="sxs-lookup"><span data-stu-id="d30f5-149">And as the app scales, your expenses grow more slowly because the bulk of your storage needs are going into very inexpensive Blob storage.</span></span>

## <a name="horizontal-partitioning-sharding"></a><span data-ttu-id="d30f5-150">Vodorovné rozdělení do oddílů (horizontálního dělení)</span><span class="sxs-lookup"><span data-stu-id="d30f5-150">Horizontal partitioning (sharding)</span></span>

<span data-ttu-id="d30f5-151">Vodorovné rozporcování je jako rozdělení tabulky po řádcích: jednu sadu řádků přejde do jednoho datového úložiště, a jinou sadu řádků, přejde do jiné datové úložiště.</span><span class="sxs-lookup"><span data-stu-id="d30f5-151">Horizontal portioning is like splitting up a table by rows: one set of rows goes into one data store, and another set of rows goes into a different data store.</span></span>

<span data-ttu-id="d30f5-152">Zadány stejnou sadu dat, bude další možnost pro uložení různých rozsahů názvů zákazníků v různých databází.</span><span class="sxs-lookup"><span data-stu-id="d30f5-152">Given the same set of data, another option would be to store different ranges of customer names in different databases.</span></span>

![Datová tabulka vodorovně na oddíly](data-partitioning-strategies/_static/image3.png)

<span data-ttu-id="d30f5-154">Chcete velmi opatrně vašeho schématu horizontálního dělení a ujistěte se, že data jsou rovnoměrně rozloženy aby se zabránilo aktivní body.</span><span class="sxs-lookup"><span data-stu-id="d30f5-154">You want to be very careful about your sharding scheme to make sure that data is evenly distributed in order to avoid hot spots.</span></span> <span data-ttu-id="d30f5-155">Tento jednoduchý příklad použití první písmeno příjmení nesplňuje tento požadavek, protože velké množství uživatelů příjmení, které začínají určitým běžné písmena.</span><span class="sxs-lookup"><span data-stu-id="d30f5-155">This simple example using the first letter of the last name doesn't meet that requirement, because a lot of people have last names that start with certain common letters.</span></span> <span data-ttu-id="d30f5-156">Omezení velikosti tabulky by setkají dříve, než by se dalo očekávat vzhledem k tomu, že některé databáze by získat velké, zatímco většina by zůstala malé.</span><span class="sxs-lookup"><span data-stu-id="d30f5-156">You'd hit table size limitations earlier than you might expect because some databases would get very large while most would remain small.</span></span>

<span data-ttu-id="d30f5-157">Dolů straně vodorovné oddíly je, že může být obtížné provést dotazy napříč všemi dat.</span><span class="sxs-lookup"><span data-stu-id="d30f5-157">A down side of horizontal partitioning is that it might be hard to do queries across all of the data.</span></span> <span data-ttu-id="d30f5-158">V tomto příkladu dotaz musel kreslení z až 26 různých databází, který zjistí všechna data uložená v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="d30f5-158">In this example, a query would have to draw from up to 26 different databases to get all of the data stored by the app.</span></span>

## <a name="hybrid-partitioning"></a><span data-ttu-id="d30f5-159">Hybridní dělení</span><span class="sxs-lookup"><span data-stu-id="d30f5-159">Hybrid partitioning</span></span>

<span data-ttu-id="d30f5-160">Můžete kombinovat svislého a vodorovného rozdělení do oddílů.</span><span class="sxs-lookup"><span data-stu-id="d30f5-160">You can combine vertical and horizontal partitioning.</span></span> <span data-ttu-id="d30f5-161">V příkladu data může například ukládání bitových kopií v úložišti objektů Blob a vodorovně rozdělení dat řetězec.</span><span class="sxs-lookup"><span data-stu-id="d30f5-161">For example, in the example data you could store the images in Blob storage and horizontally partition the string data.</span></span>

![Hybridní tabulky dat rozdělena na oddíly](data-partitioning-strategies/_static/image4.png)

## <a name="partitioning-a-production-application"></a><span data-ttu-id="d30f5-163">Vytváření oddílů produkční aplikace</span><span class="sxs-lookup"><span data-stu-id="d30f5-163">Partitioning a production application</span></span>

<span data-ttu-id="d30f5-164">Koncepčně je snadno zjistit, jak by fungují schéma rozdělení oddílů, ale žádné schéma rozdělení oddílů se zvýší složitost kódu a zavádí mnoho nové komplikací, ke které je třeba řešit.</span><span class="sxs-lookup"><span data-stu-id="d30f5-164">Conceptually it's easy to see how a partitioning scheme would work, but any partitioning scheme does increase code complexity and introduces many new complications that you have to deal with.</span></span> <span data-ttu-id="d30f5-165">Pokud přesouváte bitové kopie do úložiště objektů blob, co udělat po službu úložiště dolů?</span><span class="sxs-lookup"><span data-stu-id="d30f5-165">If you're moving images to blob storage, what do you do when the storage service is down?</span></span> <span data-ttu-id="d30f5-166">Jak zpracováváte zabezpečení objektů blob</span><span class="sxs-lookup"><span data-stu-id="d30f5-166">How do you handle blob security?</span></span> <span data-ttu-id="d30f5-167">Co se stane, pokud úložiště databáze a objektů blob synchronizované?</span><span class="sxs-lookup"><span data-stu-id="d30f5-167">What happens if the database and blob storage get out of sync?</span></span> <span data-ttu-id="d30f5-168">Pokud jste horizontálního dělení, jak bude zpracovávat dotazování napříč všemi databází?</span><span class="sxs-lookup"><span data-stu-id="d30f5-168">If you're sharding, how will you handle querying across all of the databases?</span></span>

<span data-ttu-id="d30f5-169">Komplikace jsou spravovat tak dlouho, dokud se pro ně plánování před přechodem do produkčního prostředí.</span><span class="sxs-lookup"><span data-stu-id="d30f5-169">The complications are manageable so long as you're planning for them before you go to production.</span></span> <span data-ttu-id="d30f5-170">Spousta lidí, kteří nebyla udělat, které chcete měly později.</span><span class="sxs-lookup"><span data-stu-id="d30f5-170">Many people who didn't do that wish they had later.</span></span> <span data-ttu-id="d30f5-171">V průměru náš tým zákazníka poradní tým (CAT) získá panicked telefonní hovory o jednou za měsíc od zákazníků, jejichž aplikace trvá Opravdu veliký způsobem a nebyla tak při tomto plánování.</span><span class="sxs-lookup"><span data-stu-id="d30f5-171">On average our Customer Advisory Team (CAT) team gets panicked phone calls about once a month from customers whose apps are taking off in a really big way, and they didn't do this planning.</span></span> <span data-ttu-id="d30f5-172">A říká se něco podobného jako: "Pomozte</span><span class="sxs-lookup"><span data-stu-id="d30f5-172">And they say something like: "Help!</span></span> <span data-ttu-id="d30f5-173">Všechno, co dát do jednoho datového úložiště, a v 45 dní kliknu dostatek místa na něm!"</span><span class="sxs-lookup"><span data-stu-id="d30f5-173">I put everything in a single data store, and in 45 days I'm going to run out of space on it!"</span></span> <span data-ttu-id="d30f5-174">A pokud máte spoustu součástí přístupu data store obchodní logika a máte zákazníkům, kteří používají vaši aplikaci, neexistuje žádný dobrý čas přejděte za den při migraci.</span><span class="sxs-lookup"><span data-stu-id="d30f5-174">And if you have a lot of business logic built into how you access your data store and you have customers who are using your app, there's no good time to go down for a day while you migrate.</span></span> <span data-ttu-id="d30f5-175">Jsme skončili projít herculean úsilí na pomoc oddílu odběratele svá data za chodu bez dolů doby.</span><span class="sxs-lookup"><span data-stu-id="d30f5-175">We end up going through herculean efforts to help the customer partition their data on the fly with no down time.</span></span> <span data-ttu-id="d30f5-176">Je velmi zajímavé a velmi strach, a není něco chcete být účastnící se můžete vyhnout. je-li!</span><span class="sxs-lookup"><span data-stu-id="d30f5-176">It's very exciting and very scary, and not something you want to be involved in if you can avoid it!</span></span> <span data-ttu-id="d30f5-177">Přemýšlíte o to předem a integraci do své aplikace budou život mnohem snazší, pokud aplikace zvětšování později.</span><span class="sxs-lookup"><span data-stu-id="d30f5-177">Thinking about this up front and integrating it into your app will make your life a lot easier if the app grows later.</span></span>

## <a name="summary"></a><span data-ttu-id="d30f5-178">Souhrn</span><span class="sxs-lookup"><span data-stu-id="d30f5-178">Summary</span></span>

<span data-ttu-id="d30f5-179">Efektivní schéma rozdělení oddílů můžete povolit cloudové aplikaci, kterou chcete škálovat petabajty dat v cloudu bez kritická místa.</span><span class="sxs-lookup"><span data-stu-id="d30f5-179">An effective partitioning scheme can enable your cloud app to scale to petabytes of data in the cloud without bottlenecks.</span></span> <span data-ttu-id="d30f5-180">A nemusíte předem platit za masivní počítače nebo širokou infrastrukturu, jak můžete, pokud aplikace byly spuštěny v datovém centru místní.</span><span class="sxs-lookup"><span data-stu-id="d30f5-180">And you don't have to pay up front for massive machines or extensive infrastructure as you might if you were running the app in an on-premises data center.</span></span> <span data-ttu-id="d30f5-181">V cloudu můžete postupně přidávat kapacitu podle ji potřebujete, a pouze věnujeme, pro co nejvíce, pokud používáte při použití ho.</span><span class="sxs-lookup"><span data-stu-id="d30f5-181">In the cloud you can you can incrementally add capacity as you need it, and you're only paying for as much as you're using when you use it.</span></span>

<span data-ttu-id="d30f5-182">V [další kapitoly](unstructured-blob-storage.md) ukážeme, jak aplikaci opravte implementuje vertikální dělení uložením bitové kopie v úložišti objektů Blob.</span><span class="sxs-lookup"><span data-stu-id="d30f5-182">In the [next chapter](unstructured-blob-storage.md) we'll see how the Fix It app implements vertical partitioning by storing images in Blob storage.</span></span>

## <a name="resources"></a><span data-ttu-id="d30f5-183">Prostředky</span><span class="sxs-lookup"><span data-stu-id="d30f5-183">Resources</span></span>

<span data-ttu-id="d30f5-184">Další informace o vytváření oddílů strategie najdete v následujících zdrojích informací.</span><span class="sxs-lookup"><span data-stu-id="d30f5-184">For more information about partitioning strategies, see the following resources.</span></span>

<span data-ttu-id="d30f5-185">Dokumentace:</span><span class="sxs-lookup"><span data-stu-id="d30f5-185">Documentation:</span></span>

- <span data-ttu-id="d30f5-186">[Osvědčené postupy pro návrh rozsáhlých služeb v systému Windows Azure Cloud Services](https://msdn.microsoft.com/en-us/library/windowsazure/jj717232.aspx).</span><span class="sxs-lookup"><span data-stu-id="d30f5-186">[Best Practices for the Design of Large-Scale Services on Windows Azure Cloud Services](https://msdn.microsoft.com/en-us/library/windowsazure/jj717232.aspx).</span></span> <span data-ttu-id="d30f5-187">Dokument White paper moduly SIMM značky a Michael Thomassy.</span><span class="sxs-lookup"><span data-stu-id="d30f5-187">White paper by Mark Simms and Michael Thomassy.</span></span>
- <span data-ttu-id="d30f5-188">[Microsoft Patterns and Practices - cloudu vzory návrhu](https://msdn.microsoft.com/en-us/library/dn568099.aspx).</span><span class="sxs-lookup"><span data-stu-id="d30f5-188">[Microsoft Patterns and Practices - Cloud Design Patterns](https://msdn.microsoft.com/en-us/library/dn568099.aspx).</span></span> <span data-ttu-id="d30f5-189">Najdete v části Vytvoření oddílů dat pokyny vzor horizontálního dělení.</span><span class="sxs-lookup"><span data-stu-id="d30f5-189">See Data Partitioning guidance, Sharding pattern.</span></span>

<span data-ttu-id="d30f5-190">Videa:</span><span class="sxs-lookup"><span data-stu-id="d30f5-190">Videos:</span></span>

- <span data-ttu-id="d30f5-191">[Bezporuchový: Vytváření škálovatelné, odolné cloudové služby](https://channel9.msdn.com/Series/FailSafe).</span><span class="sxs-lookup"><span data-stu-id="d30f5-191">[FailSafe: Building Scalable, Resilient Cloud Services](https://channel9.msdn.com/Series/FailSafe).</span></span> <span data-ttu-id="d30f5-192">Řada devět částí Ulrich Homann, Mercuri matolin a moduly SIMM značky.</span><span class="sxs-lookup"><span data-stu-id="d30f5-192">Nine-part series by Ulrich Homann, Marc Mercuri, and Mark Simms.</span></span> <span data-ttu-id="d30f5-193">Uvede základními koncepty a architektury zásady způsobem, velmi přístupné a zajímavé, s scénářů čerpají z prostředí Microsoft zákazníka poradní tým (CAT) s skutečným zákazníkům.</span><span class="sxs-lookup"><span data-stu-id="d30f5-193">Presents high-level concepts and architectural principles in a very accessible and interesting way, with stories drawn from Microsoft Customer Advisory Team (CAT) experience with actual customers.</span></span> <span data-ttu-id="d30f5-194">Přečtěte si rozdělení diskuzi v díl 7.</span><span class="sxs-lookup"><span data-stu-id="d30f5-194">See the partitioning discussion in episode 7.</span></span>
- <span data-ttu-id="d30f5-195">[Vytváření Big: Poučení vyplývající z zákazníky služby Windows Azure – část I](https://channel9.msdn.com/Events/Build/2012/3-029). Moduly SIMM označit popisuje rozdělení schémata horizontálního dělení strategie, jak implementovat horizontálního dělení a federace databáze SQL, počínaje 19:49.</span><span class="sxs-lookup"><span data-stu-id="d30f5-195">[Building Big: Lessons learned from Windows Azure customers - Part I](https://channel9.msdn.com/Events/Build/2012/3-029). Mark Simms discusses partitioning schemes, sharding strategies, how to implement sharding, and SQL Database Federations, starting at 19:49.</span></span> <span data-ttu-id="d30f5-196">Podobně jako u řady bezporuchový ale přejde do další postupy podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="d30f5-196">Similar to the Failsafe series but goes into more how-to details.</span></span>

<span data-ttu-id="d30f5-197">Ukázkový kód:</span><span class="sxs-lookup"><span data-stu-id="d30f5-197">Sample code:</span></span>

- <span data-ttu-id="d30f5-198">[Základy služby v systému Windows Azure Cloud](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span><span class="sxs-lookup"><span data-stu-id="d30f5-198">[Cloud Service Fundamentals in Windows Azure](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span></span> <span data-ttu-id="d30f5-199">Ukázkovou aplikaci, která zahrnuje horizontálně dělené databáze.</span><span class="sxs-lookup"><span data-stu-id="d30f5-199">Sample application that includes a sharded database.</span></span> <span data-ttu-id="d30f5-200">Popis schéma horizontálního dělení implementována najdete v tématu [DAL – horizontálního dělení RDBMS](https://blogs.msdn.com/b/windowsazure/archive/2013/09/05/dal-sharding-of-rdbms.aspx) na blogu k systému Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="d30f5-200">For a description of the sharding scheme implemented, see [DAL – Sharding of RDBMS](https://blogs.msdn.com/b/windowsazure/archive/2013/09/05/dal-sharding-of-rdbms.aspx) on the Windows Azure blog.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="d30f5-201">[Předchozí](data-storage-options.md)
[další](unstructured-blob-storage.md)</span><span class="sxs-lookup"><span data-stu-id="d30f5-201">[Previous](data-storage-options.md)
[Next](unstructured-blob-storage.md)</span></span>