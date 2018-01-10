---
title: Reference syntaxe Razor pro ASP.NET Core
author: rick-anderson
description: "Další informace o syntaxi Razor kód pro vložení kódu na serveru do webové stránky."
keywords: Direktivy Razor ASP.NET Core, Razor,
ms.author: riande
manager: wpickett
ms.date: 10/18/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/views/razor
ms.openlocfilehash: e3c3149254d602db1fcc6d42360690be026189a5
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/10/2017
---
# <a name="razor-syntax-for-aspnet-core"></a><span data-ttu-id="38516-104">Syntaxe Razor pro ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="38516-104">Razor syntax for ASP.NET Core</span></span>

<span data-ttu-id="38516-105">Podle [Rick Anderson](https://twitter.com/RickAndMSFT), [Luke Latham](https://github.com/guardrex), [Taylora MÜLLENA](https://twitter.com/ntaylormullen), a [Vicarel Dana](https://github.com/Rabadash8820)</span><span class="sxs-lookup"><span data-stu-id="38516-105">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Luke Latham](https://github.com/guardrex),  [Taylor Mullen](https://twitter.com/ntaylormullen), and [Dan Vicarel](https://github.com/Rabadash8820)</span></span>

<span data-ttu-id="38516-106">Syntaxe Razor je syntaxe kód pro vložení kódu na serveru do webové stránky.</span><span class="sxs-lookup"><span data-stu-id="38516-106">Razor is a markup syntax for embedding server-based code into webpages.</span></span> <span data-ttu-id="38516-107">Syntaxe Razor se skládá z Razor značek, C# a HTML.</span><span class="sxs-lookup"><span data-stu-id="38516-107">The Razor syntax consists of Razor markup, C#, and HTML.</span></span> <span data-ttu-id="38516-108">Soubory obsahující Razor obecně *.cshtml* příponu souboru.</span><span class="sxs-lookup"><span data-stu-id="38516-108">Files containing Razor generally have a *.cshtml* file extension.</span></span>

## <a name="rendering-html"></a><span data-ttu-id="38516-109">Vykreslování HTML</span><span class="sxs-lookup"><span data-stu-id="38516-109">Rendering HTML</span></span>

<span data-ttu-id="38516-110">Výchozí jazyk Razor jsou ve formátu HTML.</span><span class="sxs-lookup"><span data-stu-id="38516-110">The default Razor language is HTML.</span></span> <span data-ttu-id="38516-111">Vykreslování HTML z kódu Razor je nejsou jiné než vykreslování protokolu HTML ze souboru HTML.</span><span class="sxs-lookup"><span data-stu-id="38516-111">Rendering HTML from Razor markup is no different than rendering HTML from an HTML file.</span></span>  <span data-ttu-id="38516-112">Značka jazyka HTML v *.cshtml* soubory Razor je vykreslen metodou serveru beze změny.</span><span class="sxs-lookup"><span data-stu-id="38516-112">HTML markup in *.cshtml* Razor files is rendered by the server unchanged.</span></span>

## <a name="razor-syntax"></a><span data-ttu-id="38516-113">Syntaxe Razor</span><span class="sxs-lookup"><span data-stu-id="38516-113">Razor syntax</span></span>

<span data-ttu-id="38516-114">Syntaxe Razor podporuje C# a používá `@` symbol, který má přechod z HTML a C#.</span><span class="sxs-lookup"><span data-stu-id="38516-114">Razor supports C# and uses the `@` symbol to transition from HTML to C#.</span></span> <span data-ttu-id="38516-115">Syntaxe Razor vyhodnotí výrazy jazyka C# a vykreslí je ve výstupním formátu HTML.</span><span class="sxs-lookup"><span data-stu-id="38516-115">Razor evaluates C# expressions and renders them in the HTML output.</span></span>

<span data-ttu-id="38516-116">Když `@` následuje symbol [Razor vyhrazené – klíčové slovo](#razor-reserved-keywords), přechází do kódu Razor specifické.</span><span class="sxs-lookup"><span data-stu-id="38516-116">When an `@` symbol is followed by a [Razor reserved keyword](#razor-reserved-keywords), it transitions into Razor-specific markup.</span></span> <span data-ttu-id="38516-117">Jinak přejde do prostý C#.</span><span class="sxs-lookup"><span data-stu-id="38516-117">Otherwise, it transitions into plain C#.</span></span>

<span data-ttu-id="38516-118">Řídicí `@` symbolů v kódu Razor, použijte druhý `@` symbol:</span><span class="sxs-lookup"><span data-stu-id="38516-118">To escape an `@` symbol in Razor markup, use a second `@` symbol:</span></span>

```cshtml
<p>@@Username</p>
```

<span data-ttu-id="38516-119">Kód je vykreslena ve formátu HTML s jedním `@` symbol:</span><span class="sxs-lookup"><span data-stu-id="38516-119">The code is rendered in HTML with a single `@` symbol:</span></span>

```html
<p>@Username</p>
```

<span data-ttu-id="38516-120">Atributy HTML a obsah, který obsahuje e-mailové adresy nejsou s pracovat `@` symbol jako znak přechodu.</span><span class="sxs-lookup"><span data-stu-id="38516-120">HTML attributes and content containing email addresses don't treat the `@` symbol as a transition character.</span></span> <span data-ttu-id="38516-121">E-mailové adresy v následujícím příkladu jsou nezměněné pomocí syntaxe Razor analýza:</span><span class="sxs-lookup"><span data-stu-id="38516-121">The email addresses in the following example are untouched by Razor parsing:</span></span>

```cshtml
<a href="mailto:Support@contoso.com">Support@contoso.com</a>
```

## <a name="implicit-razor-expressions"></a><span data-ttu-id="38516-122">Implicitní výrazy Razor</span><span class="sxs-lookup"><span data-stu-id="38516-122">Implicit Razor expressions</span></span>

<span data-ttu-id="38516-123">Implicitní výrazy Razor začínat `@` následuje kód C#:</span><span class="sxs-lookup"><span data-stu-id="38516-123">Implicit Razor expressions start with `@` followed by C# code:</span></span>

```cshtml
<p>@DateTime.Now</p>
<p>@DateTime.IsLeapYear(2016)</p>
```

<span data-ttu-id="38516-124">S výjimkou jazyka C# `await` – klíčové slovo, implicitní výrazy nesmí obsahovat mezery.</span><span class="sxs-lookup"><span data-stu-id="38516-124">With the exception of the C# `await` keyword, implicit expressions must not contain spaces.</span></span> <span data-ttu-id="38516-125">Pokud příkaz jazyka C# zrušte ukončuje, můžete intermingled mezery:</span><span class="sxs-lookup"><span data-stu-id="38516-125">If the C# statement has a clear ending, spaces can be intermingled:</span></span>

```cshtml
<p>@await DoSomething("hello", "world")</p>
```

<span data-ttu-id="38516-126">Implicitní výrazy **nelze** obsahovat obecnými typy C#, jako znaků v závorkách (`<>`) se interpretují jako značky jazyka HTML.</span><span class="sxs-lookup"><span data-stu-id="38516-126">Implicit expressions **cannot** contain C# generics, as the characters inside the brackets (`<>`) are interpreted as an HTML tag.</span></span> <span data-ttu-id="38516-127">Následující kód je **není** platné:</span><span class="sxs-lookup"><span data-stu-id="38516-127">The following code is **not** valid:</span></span>

```cshtml
<p>@GenericMethod<int>()</p>
```

<span data-ttu-id="38516-128">Předchozí kód vygeneruje chybu kompilátoru podobně jako jednu z těchto možností:</span><span class="sxs-lookup"><span data-stu-id="38516-128">The preceding code generates a compiler error similar to one of the following:</span></span>

 * <span data-ttu-id="38516-129">Element "int" nebyla uzavřena.</span><span class="sxs-lookup"><span data-stu-id="38516-129">The "int" element was not closed.</span></span>  <span data-ttu-id="38516-130">Všechny elementy musí být buď samoobslužné zavírání nebo koncová značka.</span><span class="sxs-lookup"><span data-stu-id="38516-130">All elements must be either self-closing or have a matching end tag.</span></span>
 *  <span data-ttu-id="38516-131">Metoda skupiny 'GenericMethod' bez delegátem typu 'objekt' nelze převést.</span><span class="sxs-lookup"><span data-stu-id="38516-131">Cannot convert method group 'GenericMethod' to non-delegate type 'object'.</span></span> <span data-ttu-id="38516-132">Opravdu chcete vyvolat metodu? "</span><span class="sxs-lookup"><span data-stu-id="38516-132">Did you intend to invoke the method?\`</span></span> 
 
<span data-ttu-id="38516-133">Volání obecné metody musí být uzavřen do [explicitní výraz Razor](#explicit-razor-expressions) nebo [blok kódu Razor](#razor-code-blocks).</span><span class="sxs-lookup"><span data-stu-id="38516-133">Generic method calls must be wrapped in an [explicit Razor expression](#explicit-razor-expressions) or a [Razor code block](#razor-code-blocks).</span></span> <span data-ttu-id="38516-134">Toto omezení se nevztahuje na *.vbhtml* Razor soubory, protože syntaxe jazyka Visual Basic umístí parametry obecného typu místo závorky v závorkách.</span><span class="sxs-lookup"><span data-stu-id="38516-134">This restriction doesn't apply to *.vbhtml* Razor files because Visual Basic syntax places parentheses around generic type parameters instead of brackets.</span></span>

## <a name="explicit-razor-expressions"></a><span data-ttu-id="38516-135">Explicitní výrazy Razor</span><span class="sxs-lookup"><span data-stu-id="38516-135">Explicit Razor expressions</span></span>

<span data-ttu-id="38516-136">Explicitní výrazy Razor obsahovat `@` symbol s vyrovnáváním závorky.</span><span class="sxs-lookup"><span data-stu-id="38516-136">Explicit Razor expressions consist of an `@` symbol with balanced parenthesis.</span></span> <span data-ttu-id="38516-137">K vykreslení čas poslední týden, se používá následující syntaxe Razor kód:</span><span class="sxs-lookup"><span data-stu-id="38516-137">To render last week's time, the following Razor markup is used:</span></span>

```cshtml
<p>Last week this time: @(DateTime.Now - TimeSpan.FromDays(7))</p>
```

<span data-ttu-id="38516-138">Veškerý obsah v rámci `@()` závorky je vyhodnocena a vykresleny výstup.</span><span class="sxs-lookup"><span data-stu-id="38516-138">Any content within the `@()` parenthesis is evaluated and rendered to the output.</span></span>

<span data-ttu-id="38516-139">Implicitní výrazy, které jsou popsané v předchozí části, obecně nesmí obsahovat mezery.</span><span class="sxs-lookup"><span data-stu-id="38516-139">Implicit expressions, described in the previous section, generally can't contain spaces.</span></span> <span data-ttu-id="38516-140">V následujícím kódu není jeden týden odečten od aktuální čas:</span><span class="sxs-lookup"><span data-stu-id="38516-140">In the following code, one week isn't subtracted from the current time:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact.cshtml?range=17)]

<span data-ttu-id="38516-141">Vykreslí kód HTML následující:</span><span class="sxs-lookup"><span data-stu-id="38516-141">The code renders the following HTML:</span></span>

```html
<p>Last week: 7/7/2016 4:39:52 PM - TimeSpan.FromDays(7)</p>
```

<span data-ttu-id="38516-142">Explicitní výrazy můžete použít ke zřetězení textu pomocí výsledek výrazu:</span><span class="sxs-lookup"><span data-stu-id="38516-142">Explicit expressions can be used to concatenate text with an expression result:</span></span>

```cshtml
@{
    var joe = new Person("Joe", 33);
}

<p>Age@(joe.Age)</p>
```

<span data-ttu-id="38516-143">Bez explicitního výrazu `<p>Age@joe.Age</p>` je považován za e-mailovou adresu a `<p>Age@joe.Age</p>` je vykreslen.</span><span class="sxs-lookup"><span data-stu-id="38516-143">Without the explicit expression, `<p>Age@joe.Age</p>` is treated as an email address, and `<p>Age@joe.Age</p>` is rendered.</span></span> <span data-ttu-id="38516-144">Když k zapsání jako výraz explicitní `<p>Age33</p>` je vykreslen.</span><span class="sxs-lookup"><span data-stu-id="38516-144">When written as an explicit expression, `<p>Age33</p>` is rendered.</span></span>


<span data-ttu-id="38516-145">Explicitní výrazy můžete použít k vykreslení výstupu z obecné metody v *.cshtml* soubory.</span><span class="sxs-lookup"><span data-stu-id="38516-145">Explicit expressions can be used to render output from generic methods in *.cshtml* files.</span></span> <span data-ttu-id="38516-146">Ve výrazu implicitní znaků v závorkách (`<>`) se interpretují jako značky jazyka HTML.</span><span class="sxs-lookup"><span data-stu-id="38516-146">In an implicit expression, the characters inside the brackets (`<>`) are interpreted as an HTML tag.</span></span> <span data-ttu-id="38516-147">Následující kód je **není** platný Razor:</span><span class="sxs-lookup"><span data-stu-id="38516-147">The following markup is **not** valid Razor:</span></span>

```cshtml
<p>@GenericMethod<int>()</p>
```

<span data-ttu-id="38516-148">Předchozí kód vygeneruje chybu kompilátoru podobně jako jednu z těchto možností:</span><span class="sxs-lookup"><span data-stu-id="38516-148">The preceding code generates a compiler error similar to one of the following:</span></span>

 * <span data-ttu-id="38516-149">Element "int" nebyla uzavřena.</span><span class="sxs-lookup"><span data-stu-id="38516-149">The "int" element was not closed.</span></span>  <span data-ttu-id="38516-150">Všechny elementy musí být buď samoobslužné zavírání nebo koncová značka.</span><span class="sxs-lookup"><span data-stu-id="38516-150">All elements must be either self-closing or have a matching end tag.</span></span>
 *  <span data-ttu-id="38516-151">Metoda skupiny 'GenericMethod' bez delegátem typu 'objekt' nelze převést.</span><span class="sxs-lookup"><span data-stu-id="38516-151">Cannot convert method group 'GenericMethod' to non-delegate type 'object'.</span></span> <span data-ttu-id="38516-152">Opravdu chcete vyvolat metodu? "</span><span class="sxs-lookup"><span data-stu-id="38516-152">Did you intend to invoke the method?\`</span></span> 
 
 <span data-ttu-id="38516-153">Následující kód ukazuje zápisu správný způsob, jak tento kód.</span><span class="sxs-lookup"><span data-stu-id="38516-153">The following markup shows the correct way write this code.</span></span>  <span data-ttu-id="38516-154">Kód je zapsána jako explicitní výrazu:</span><span class="sxs-lookup"><span data-stu-id="38516-154">The code is written as an explicit expression:</span></span>

```cshtml
<p>@(GenericMethod<int>())</p>
```

<span data-ttu-id="38516-155">Poznámka: Toto omezení se nevztahuje na *.vbhtml* soubory Razor.</span><span class="sxs-lookup"><span data-stu-id="38516-155">Note: this restriction doesn't apply to *.vbhtml* Razor files.</span></span>  <span data-ttu-id="38516-156">S *.vbhtml* soubory Razor, syntaxe jazyka Visual Basic umístí parametry obecného typu místo závorky v závorkách.</span><span class="sxs-lookup"><span data-stu-id="38516-156">With *.vbhtml* Razor files, Visual Basic syntax places parentheses around generic type parameters instead of brackets.</span></span>

## <a name="expression-encoding"></a><span data-ttu-id="38516-157">Výraz kódování</span><span class="sxs-lookup"><span data-stu-id="38516-157">Expression encoding</span></span>

<span data-ttu-id="38516-158">Jsou výrazy jazyka C#, která se vyhodnotí jako řetězec kódovaný jazykem HTML.</span><span class="sxs-lookup"><span data-stu-id="38516-158">C# expressions that evaluate to a string are HTML encoded.</span></span> <span data-ttu-id="38516-159">Výrazy jazyka C#, která se vyhodnotí jako `IHtmlContent` vykreslují přímo přes `IHtmlContent.WriteTo`.</span><span class="sxs-lookup"><span data-stu-id="38516-159">C# expressions that evaluate to `IHtmlContent` are rendered directly through `IHtmlContent.WriteTo`.</span></span> <span data-ttu-id="38516-160">C# výrazů, které nejsou vyhodnocení `IHtmlContent` jsou převedeno na řetězec pomocí `ToString` a kódováním než jejich se zobrazí.</span><span class="sxs-lookup"><span data-stu-id="38516-160">C# expressions that don't evaluate to `IHtmlContent` are converted to a string by `ToString` and encoded before they're rendered.</span></span>

```cshtml
@("<span>Hello World</span>")
```

<span data-ttu-id="38516-161">Vykreslí kód HTML následující:</span><span class="sxs-lookup"><span data-stu-id="38516-161">The code renders the following HTML:</span></span>

```html
&lt;span&gt;Hello World&lt;/span&gt;
```

<span data-ttu-id="38516-162">HTML je zobrazena v prohlížeči jako:</span><span class="sxs-lookup"><span data-stu-id="38516-162">The HTML is shown in the browser as:</span></span>

```
<span>Hello World</span>
```

<span data-ttu-id="38516-163">`HtmlHelper.Raw`výstup není kódovaný ale vykresleno jako značka jazyka HTML.</span><span class="sxs-lookup"><span data-stu-id="38516-163">`HtmlHelper.Raw` output isn't encoded but rendered as HTML markup.</span></span>

> [!WARNING]
> <span data-ttu-id="38516-164">Pomocí `HtmlHelper.Raw` unsanitized uživatelský vstup je bezpečnostní riziko.</span><span class="sxs-lookup"><span data-stu-id="38516-164">Using `HtmlHelper.Raw` on unsanitized user input is a security risk.</span></span> <span data-ttu-id="38516-165">Uživatelský vstup může obsahovat jiné zneužití nebo škodlivý JavaScript.</span><span class="sxs-lookup"><span data-stu-id="38516-165">User input might contain malicious JavaScript or other exploits.</span></span> <span data-ttu-id="38516-166">Úpravě uživatelský vstup je obtížné.</span><span class="sxs-lookup"><span data-stu-id="38516-166">Sanitizing user input is difficult.</span></span> <span data-ttu-id="38516-167">Nepoužívejte `HtmlHelper.Raw` se vstupem uživatele.</span><span class="sxs-lookup"><span data-stu-id="38516-167">Avoid using `HtmlHelper.Raw` with user input.</span></span>

```cshtml
@Html.Raw("<span>Hello World</span>")
```

<span data-ttu-id="38516-168">Vykreslí kód HTML následující:</span><span class="sxs-lookup"><span data-stu-id="38516-168">The code renders the following HTML:</span></span>

```html
<span>Hello World</span>
```

## <a name="razor-code-blocks"></a><span data-ttu-id="38516-169">Bloky kódu Razor</span><span class="sxs-lookup"><span data-stu-id="38516-169">Razor code blocks</span></span>

<span data-ttu-id="38516-170">Bloky kódu Razor začínat `@` a jsou uvedeny v `{}`.</span><span class="sxs-lookup"><span data-stu-id="38516-170">Razor code blocks start with `@` and are enclosed by `{}`.</span></span> <span data-ttu-id="38516-171">Na rozdíl od výrazy není vykreslen kódu C# do bloků kódu.</span><span class="sxs-lookup"><span data-stu-id="38516-171">Unlike expressions, C# code inside code blocks isn't rendered.</span></span> <span data-ttu-id="38516-172">Bloky kódu a výrazy v zobrazení sdílejí stejný obor a jsou definovány v pořadí:</span><span class="sxs-lookup"><span data-stu-id="38516-172">Code blocks and expressions in a view share the same scope and are defined in order:</span></span>

```cshtml
@{
    var quote = "The future depends on what you do today. - Mahatma Gandhi";
}

<p>@quote</p>

@{
    quote = "Hate cannot drive out hate, only love can do that. - Martin Luther King, Jr.";
}

<p>@quote</p>
```

<span data-ttu-id="38516-173">Vykreslí kód HTML následující:</span><span class="sxs-lookup"><span data-stu-id="38516-173">The code renders the following HTML:</span></span>

```html
<p>The future depends on what you do today. - Mahatma Gandhi</p>
<p>Hate cannot drive out hate, only love can do that. - Martin Luther King, Jr.</p>
```

### <a name="implicit-transitions"></a><span data-ttu-id="38516-174">Implicitní přechody</span><span class="sxs-lookup"><span data-stu-id="38516-174">Implicit transitions</span></span>

<span data-ttu-id="38516-175">Je výchozí jazyk v bloku kódu C#, ale stránky Razor můžete přejít zpět do formátu HTML:</span><span class="sxs-lookup"><span data-stu-id="38516-175">The default language in a code block is C#, but the Razor Page can transition back to HTML:</span></span>

```cshtml
@{
    var inCSharp = true;
    <p>Now in HTML, was in C# @inCSharp</p>
}
```

### <a name="explicit-delimited-transition"></a><span data-ttu-id="38516-176">Explicitní přechod s oddělovači</span><span class="sxs-lookup"><span data-stu-id="38516-176">Explicit delimited transition</span></span>

<span data-ttu-id="38516-177">K definování část bloku kódu, který by měl vykreslení HTML, uzavřete znaků pro vykreslování s syntaxi Razor  **\<text >** značky:</span><span class="sxs-lookup"><span data-stu-id="38516-177">To define a subsection of a code block that should render HTML, surround the characters for rendering with the Razor **\<text>** tag:</span></span>

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    <text>Name: @person.Name</text>
}
```

<span data-ttu-id="38516-178">Tuto metodu použijte k vykreslení HTML, který není obklopená značky jazyka HTML.</span><span class="sxs-lookup"><span data-stu-id="38516-178">Use this approach to render HTML that isn't surrounded by an HTML tag.</span></span> <span data-ttu-id="38516-179">Bez značku HTML nebo Razor nastane běhová chyba syntaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="38516-179">Without an HTML or Razor tag, a Razor runtime error occurs.</span></span>

<span data-ttu-id="38516-180"> **\<Text >** značka je vhodné pro řízení prázdných znaků při vykreslování obsahu:</span><span class="sxs-lookup"><span data-stu-id="38516-180">The **\<text>** tag is useful to control whitespace when rendering content:</span></span>

* <span data-ttu-id="38516-181">Pouze obsah, mezi  **\<text >** je vykreslen.</span><span class="sxs-lookup"><span data-stu-id="38516-181">Only the content between the **\<text>** tag is rendered.</span></span> 
* <span data-ttu-id="38516-182">Žádné prázdné před nebo po  **\<text >** značky se zobrazí ve výstupu protokolu HTML.</span><span class="sxs-lookup"><span data-stu-id="38516-182">No whitespace before or after the **\<text>** tag appears in the HTML output.</span></span>

### <a name="explicit-line-transition-with-"></a><span data-ttu-id="38516-183">Explicitní řádek přechodu se @:</span><span class="sxs-lookup"><span data-stu-id="38516-183">Explicit Line Transition with @:</span></span>

<span data-ttu-id="38516-184">K vykreslení zbytek celý řádek jako kód HTML uvnitř bloku kódu, použijte `@:` syntaxe:</span><span class="sxs-lookup"><span data-stu-id="38516-184">To render the rest of an entire line as HTML inside a code block, use the `@:` syntax:</span></span>

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    @:Name: @person.Name
}
```

<span data-ttu-id="38516-185">Bez `@:` v kódu, je generována chyba runtime Razor.</span><span class="sxs-lookup"><span data-stu-id="38516-185">Without the `@:` in the code,  a Razor runtime error is generated.</span></span>

<span data-ttu-id="38516-186">Upozornění: Navíc `@` znaky v souboru nástroje Razor mohou způsobit chyby kompilátoru příčina na příkazy v bloku později.</span><span class="sxs-lookup"><span data-stu-id="38516-186">Warning: Extra `@` characters in a Razor file can cause  cause compiler errors at statements later in the block.</span></span> <span data-ttu-id="38516-187">Tyto chyby kompilátoru může být obtížné zjistit, protože dojde k chybě skutečné před ohlášené chyby.</span><span class="sxs-lookup"><span data-stu-id="38516-187">These compiler errors can be difficult to understand because the actual error occurs before the reported error.</span></span>  <span data-ttu-id="38516-188">Tato chyba je běžné po kombinování více implicitního nebo explicitního výrazů do jednoho kód bloku.</span><span class="sxs-lookup"><span data-stu-id="38516-188">This error is common after combining multiple implicit/explicit expressions into a single code block.</span></span>

## <a name="control-structures"></a><span data-ttu-id="38516-189">Řídicí struktury</span><span class="sxs-lookup"><span data-stu-id="38516-189">Control Structures</span></span>

<span data-ttu-id="38516-190">Řídicí struktury, jsou rozšíření bloky kódu.</span><span class="sxs-lookup"><span data-stu-id="38516-190">Control structures are an extension of code blocks.</span></span> <span data-ttu-id="38516-191">Všechny aspekty bloky kódu (Přechod na kód, vložené C#) také použít následující struktury:</span><span class="sxs-lookup"><span data-stu-id="38516-191">All aspects of code blocks (transitioning to markup, inline C#) also apply to the following structures:</span></span>

### <a name="conditionals-if-else-if-else-and-switch"></a><span data-ttu-id="38516-192">Podmíněné příkazy @if, pokud jiný, #else a@switch</span><span class="sxs-lookup"><span data-stu-id="38516-192">Conditionals @if, else if, else, and @switch</span></span>

<span data-ttu-id="38516-193">`@if`ovládací prvky při spuštění kódu:</span><span class="sxs-lookup"><span data-stu-id="38516-193">`@if` controls when code runs:</span></span>

```cshtml
@if (value % 2 == 0)
{
    <p>The value was even.</p>
}
```

<span data-ttu-id="38516-194">`else`a `else if` nevyžadují `@` symbol:</span><span class="sxs-lookup"><span data-stu-id="38516-194">`else` and `else if` don't require the `@` symbol:</span></span>

```cshtml
@if (value % 2 == 0)
{
    <p>The value was even.</p>
}
else if (value >= 1337)
{
    <p>The value is large.</p>
}
else
{
    <p>The value is odd and small.</p>
}
```

<span data-ttu-id="38516-195">Následující kód ukazuje, jak používat příkaz switch:</span><span class="sxs-lookup"><span data-stu-id="38516-195">The following markup shows how to use a switch statement:</span></span>

```cshtml
@switch (value)
{
    case 1:
        <p>The value is 1!</p>
        break;
    case 1337:
        <p>Your number is 1337!</p>
        break;
    default:
        <p>Your number wasn't 1 or 1337.</p>
        break;
}
```

### <a name="looping-for-foreach-while-and-do-while"></a><span data-ttu-id="38516-196">Ve smyčce @for, @foreach, @while, a @do při</span><span class="sxs-lookup"><span data-stu-id="38516-196">Looping @for, @foreach, @while, and @do while</span></span>

<span data-ttu-id="38516-197">Použitím šablon HTML, které lze vykreslit s opakování ve smyčce řídicí příkazy.</span><span class="sxs-lookup"><span data-stu-id="38516-197">Templated HTML can be rendered with looping control statements.</span></span>  <span data-ttu-id="38516-198">K vykreslení seznam lidí, kteří:</span><span class="sxs-lookup"><span data-stu-id="38516-198">To render a list of people:</span></span>

```cshtml
@{
    var people = new Person[]
    {
          new Person("Weston", 33),
          new Person("Johnathon", 41),
          ...
    };
}
```

<span data-ttu-id="38516-199">Podporovány jsou následující příkazy opakování:</span><span class="sxs-lookup"><span data-stu-id="38516-199">The following looping statements are supported:</span></span>

`@for`

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>
}
```

`@foreach`

```cshtml
@foreach (var person in people)
{
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>
}
```

`@while`

```cshtml
@{ var i = 0; }
@while (i < people.Length)
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>

    i++;
}
```

`@do while`

```cshtml
@{ var i = 0; }
@do
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>

    i++;
} while (i < people.Length);
```

### <a name="compound-using"></a><span data-ttu-id="38516-200">Složené@using</span><span class="sxs-lookup"><span data-stu-id="38516-200">Compound @using</span></span>

<span data-ttu-id="38516-201">V jazyce C# `using` příkaz slouží k zajištění uvolnění objektu.</span><span class="sxs-lookup"><span data-stu-id="38516-201">In C#, a `using` statement is used to ensure an object is disposed.</span></span> <span data-ttu-id="38516-202">V prostředí Razor shodný mechanismus slouží k vytvoření pomocné rutiny HTML, které obsahují další obsah.</span><span class="sxs-lookup"><span data-stu-id="38516-202">In Razor, the same mechanism is used to create HTML Helpers that contain additional content.</span></span> <span data-ttu-id="38516-203">V následujícím kódu pomocné rutiny HTML, vykreslení značku formuláře s `@using` příkaz:</span><span class="sxs-lookup"><span data-stu-id="38516-203">In the following code, HTML Helpers render a form tag with the `@using` statement:</span></span>


```cshtml
@using (Html.BeginForm())
{
    <div>
        email:
        <input type="email" id="Email" value="">
        <button>Register</button>
    </div>
}
```

<span data-ttu-id="38516-204">Lze provést akce na úrovni oboru [značky Pomocníci](xref:mvc/views/tag-helpers/intro).</span><span class="sxs-lookup"><span data-stu-id="38516-204">Scope-level actions can be performed with [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span>

### <a name="try-catch-finally"></a><span data-ttu-id="38516-205">@try, nakonec catch</span><span class="sxs-lookup"><span data-stu-id="38516-205">@try, catch, finally</span></span>

<span data-ttu-id="38516-206">Zpracovávání výjimek v jazyce je podobná C#:</span><span class="sxs-lookup"><span data-stu-id="38516-206">Exception handling is similar to C#:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact7.cshtml)]

### <a name="lock"></a>@lock

<span data-ttu-id="38516-207">Syntaxe Razor má možnost chránit kritické oddíly s příkazy uzamčení:</span><span class="sxs-lookup"><span data-stu-id="38516-207">Razor has the capability to protect critical sections with lock statements:</span></span>

```cshtml
@lock (SomeLock)
{
    // Do critical section work
}
```

### <a name="comments"></a><span data-ttu-id="38516-208">Komentáře</span><span class="sxs-lookup"><span data-stu-id="38516-208">Comments</span></span>

<span data-ttu-id="38516-209">Syntaxe Razor podporuje komentáře jazyka C# a HTML:</span><span class="sxs-lookup"><span data-stu-id="38516-209">Razor supports C# and HTML comments:</span></span>

```cshtml
@{
    /* C# comment */
    // Another C# comment
}
<!-- HTML comment -->
```

<span data-ttu-id="38516-210">Vykreslí kód HTML následující:</span><span class="sxs-lookup"><span data-stu-id="38516-210">The code renders the following HTML:</span></span>

```html
<!-- HTML comment -->
```

<span data-ttu-id="38516-211">Komentáře syntaxe Razor serverem jsou odebrány, než se zobrazí webová stránka.</span><span class="sxs-lookup"><span data-stu-id="38516-211">Razor comments are removed by the server before the webpage is rendered.</span></span> <span data-ttu-id="38516-212">Používá syntaxi Razor `@*  *@` pro vymezení komentáře.</span><span class="sxs-lookup"><span data-stu-id="38516-212">Razor uses `@*  *@` to delimit comments.</span></span> <span data-ttu-id="38516-213">Následující kód je označeno jako komentář, tak server nemá vykreslení žádné značky:</span><span class="sxs-lookup"><span data-stu-id="38516-213">The following code is commented out, so the server doesn't render any markup:</span></span>

```cshtml
@*
    @{
        /* C# comment */
        // Another C# comment
    }
    <!-- HTML comment -->
*@
```

## <a name="directives"></a><span data-ttu-id="38516-214">Direktivy</span><span class="sxs-lookup"><span data-stu-id="38516-214">Directives</span></span>

<span data-ttu-id="38516-215">Direktivy Razor jsou reprezentované pomocí implicitní výrazy s následující vyhrazená slova `@` symbol.</span><span class="sxs-lookup"><span data-stu-id="38516-215">Razor directives are represented by implicit expressions with reserved keywords following the `@` symbol.</span></span> <span data-ttu-id="38516-216">Direktivu obvykle mění způsob zobrazení je analyzována nebo jinou funkci povolí.</span><span class="sxs-lookup"><span data-stu-id="38516-216">A directive typically changes the way a view is parsed or enables different functionality.</span></span>

<span data-ttu-id="38516-217">Pochopení, jak Razor generuje kód pro zobrazení usnadňuje pochopili, jak funguje direktivy.</span><span class="sxs-lookup"><span data-stu-id="38516-217">Understanding how Razor generates code for a view makes it easier to understand how directives work.</span></span>

[!code-html[Main](razor/sample/Views/Home/Contact8.cshtml)]

<span data-ttu-id="38516-218">Generuje kód třídu podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="38516-218">The code generates a class similar to the following:</span></span>

```csharp
public class _Views_Something_cshtml : RazorPage<dynamic>
{
    public override async Task ExecuteAsync()
    {
        var output = "Getting old ain't for wimps! - Anonymous";

        WriteLiteral("/r/n<div>Quote of the Day: ");
        Write(output);
        WriteLiteral("</div>");
    }
}
```

<span data-ttu-id="38516-219">Dále v tomto článku v části [zobrazení třídy Razor C# vytvořené pro zobrazení](#viewing-the-razor-c-class-generated-for-a-view) vysvětluje, jak zobrazit tento vygenerované třídy.</span><span class="sxs-lookup"><span data-stu-id="38516-219">Later in this article, the section [Viewing the Razor C# class generated for a view](#viewing-the-razor-c-class-generated-for-a-view) explains how to view this generated class.</span></span>

### <a name="using"></a>@using

<span data-ttu-id="38516-220">`@using` – Direktiva přidá jazyka C# `using` direktivy generované zobrazení:</span><span class="sxs-lookup"><span data-stu-id="38516-220">The `@using` directive adds the C# `using` directive to the generated view:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact9.cshtml)]

### <a name="model"></a>@model

<span data-ttu-id="38516-221">`@model` – Direktiva Určuje typ modelu předána do zobrazení:</span><span class="sxs-lookup"><span data-stu-id="38516-221">The `@model` directive specifies the type of the model passed to a view:</span></span>

```cshtml
@model TypeNameOfModel
```

<span data-ttu-id="38516-222">V aplikaci ASP.NET MVC základní vytvořené pomocí jednotlivých uživatelských účtů *Views/Account/Login.cshtml* zobrazení obsahuje následující prohlášení modelu:</span><span class="sxs-lookup"><span data-stu-id="38516-222">In an ASP.NET Core MVC app created with individual user accounts, the *Views/Account/Login.cshtml* view contains the following model declaration:</span></span>

```cshtml
@model LoginViewModel
```

<span data-ttu-id="38516-223">Vygenerované třídy dědí z `RazorPage<dynamic>`:</span><span class="sxs-lookup"><span data-stu-id="38516-223">The class generated inherits from `RazorPage<dynamic>`:</span></span>

```csharp
public class _Views_Account_Login_cshtml : RazorPage<LoginViewModel>
```

<span data-ttu-id="38516-224">Zpřístupní Razor `Model` vlastnost pro přístup k modelu předaná do zobrazení:</span><span class="sxs-lookup"><span data-stu-id="38516-224">Razor exposes a `Model` property for accessing the model passed to the view:</span></span>

```cshtml
<div>The Login Email: @Model.Email</div>
```

<span data-ttu-id="38516-225">`@model` – Direktiva Určuje typ této vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="38516-225">The `@model` directive specifies the type of this property.</span></span> <span data-ttu-id="38516-226">Direktiva Určuje `T` v `RazorPage<T>` že generované třídy, zobrazení je odvozena z.</span><span class="sxs-lookup"><span data-stu-id="38516-226">The directive specifies the `T` in `RazorPage<T>` that the generated class that the view derives from.</span></span> <span data-ttu-id="38516-227">Pokud `@model` direktivy iisn't zadána, `Model` vlastnost je typu `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="38516-227">If  the `@model` directive iisn't specified, the `Model` property is of type `dynamic`.</span></span> <span data-ttu-id="38516-228">Hodnota modelu se z řadiče předaná do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="38516-228">The value of the model is passed from the controller to the view.</span></span> <span data-ttu-id="38516-229">Další informace najdete v tématu [silného typu modely a @model – klíčové slovo.</span><span class="sxs-lookup"><span data-stu-id="38516-229">For more information, see [Strongly typed models and the @model keyword.</span></span>

### <a name="inherits"></a>@inherits

<span data-ttu-id="38516-230">`@inherits` – Direktiva poskytuje úplné řízení třídy dědí zobrazení:</span><span class="sxs-lookup"><span data-stu-id="38516-230">The `@inherits` directive provides  full control of the class the view inherits:</span></span>

```cshtml
@inherits TypeNameOfClassToInheritFrom
```

<span data-ttu-id="38516-231">Následující kód je vlastní typ stránky Razor:</span><span class="sxs-lookup"><span data-stu-id="38516-231">The following code is a custom Razor page type:</span></span>

[!code-csharp[Main](razor/sample/Classes/CustomRazorPage.cs)]

<span data-ttu-id="38516-232">`CustomText` Se zobrazí v zobrazení:</span><span class="sxs-lookup"><span data-stu-id="38516-232">The `CustomText` is displayed in a view:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact10.cshtml)]

<span data-ttu-id="38516-233">Vykreslí kód HTML následující:</span><span class="sxs-lookup"><span data-stu-id="38516-233">The code renders the following HTML:</span></span>

```html
<div>Custom text: Gardyloo! - A Scottish warning yelled from a window before dumping a slop bucket on the street below.</div>
```

 <span data-ttu-id="38516-234">`@model`a `@inherits` lze použít ve stejném zobrazení.</span><span class="sxs-lookup"><span data-stu-id="38516-234">`@model` and `@inherits` can be used in the same view.</span></span>  <span data-ttu-id="38516-235">`@inherits`může být v *_ViewImports.cshtml* soubor, který importuje zobrazení:</span><span class="sxs-lookup"><span data-stu-id="38516-235">`@inherits` can be in a *_ViewImports.cshtml* file that the view imports:</span></span>

[!code-cshtml[Main](razor/sample/Views/_ViewImportsModel.cshtml)]

<span data-ttu-id="38516-236">Následující kód je příkladem zobrazení silného typu:</span><span class="sxs-lookup"><span data-stu-id="38516-236">The following code is an example of a strongly-typed view:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Login1.cshtml)]

<span data-ttu-id="38516-237">Pokud "rick@contoso.com" je předán v modelu zobrazení generuje následující kód HTML:</span><span class="sxs-lookup"><span data-stu-id="38516-237">If "rick@contoso.com" is passed in the model, the view generates the following HTML markup:</span></span>

```html
<div>The Login Email: rick@contoso.com</div>
<div>Custom text: Gardyloo! - A Scottish warning yelled from a window before dumping a slop bucket on the street below.</div>
```

### <a name="inject"></a>@inject


<span data-ttu-id="38516-238">`@inject` – Direktiva umožňuje vložit služby z této stránky Razor [kontejneru služby](xref:fundamentals/dependency-injection) do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="38516-238">The `@inject` directive enables the Razor Page to inject a service from the [service container](xref:fundamentals/dependency-injection) into a view.</span></span> <span data-ttu-id="38516-239">Další informace najdete v tématu [vkládání závislostí do zobrazení](xref:mvc/views/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="38516-239">For more information, see [Dependency injection into views](xref:mvc/views/dependency-injection).</span></span>

### <a name="functions"></a>@functions

<span data-ttu-id="38516-240">`@functions` – Direktiva umožňuje přidat obsah na úrovni funkce do zobrazení Razor stránky:</span><span class="sxs-lookup"><span data-stu-id="38516-240">The `@functions` directive enables a Razor Page to add function-level content to a view:</span></span>

```cshtml
@functions { // C# Code }
```

<span data-ttu-id="38516-241">Příklad:</span><span class="sxs-lookup"><span data-stu-id="38516-241">For example:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact6.cshtml)]

<span data-ttu-id="38516-242">Kód generuje následující kód HTML:</span><span class="sxs-lookup"><span data-stu-id="38516-242">The code generates the following HTML markup:</span></span>

```html
<div>From method: Hello</div>
```

<span data-ttu-id="38516-243">Následující kód je generovaná třída Razor C#:</span><span class="sxs-lookup"><span data-stu-id="38516-243">The following code is the generated Razor C# class:</span></span>

[!code-csharp[Main](razor/sample/Classes/Views_Home_Test_cshtml.cs?range=1-19)]

### <a name="section"></a>@section

<span data-ttu-id="38516-244">`@section` – Direktiva se používá ve spojení s [rozložení](xref:mvc/views/layout) umožnit zobrazení k vykreslení obsahu v různých částech stránky HTML.</span><span class="sxs-lookup"><span data-stu-id="38516-244">The `@section` directive is used in conjunction with the [layout](xref:mvc/views/layout) to enable views to render content in different parts of the HTML page.</span></span> <span data-ttu-id="38516-245">Další informace najdete v tématu [části](xref:mvc/views/layout#layout-sections-label).</span><span class="sxs-lookup"><span data-stu-id="38516-245">For more information, see [Sections](xref:mvc/views/layout#layout-sections-label).</span></span>

## <a name="tag-helpers"></a><span data-ttu-id="38516-246">Pomocníci značky</span><span class="sxs-lookup"><span data-stu-id="38516-246">Tag Helpers</span></span>

<span data-ttu-id="38516-247">Existují tři direktivy, které se týkají [značky Pomocníci](xref:mvc/views/tag-helpers/intro).</span><span class="sxs-lookup"><span data-stu-id="38516-247">There are three directives that pertain to [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span>

| <span data-ttu-id="38516-248">– Direktiva</span><span class="sxs-lookup"><span data-stu-id="38516-248">Directive</span></span> | <span data-ttu-id="38516-249">Funkce</span><span class="sxs-lookup"><span data-stu-id="38516-249">Function</span></span> |
| --------- | -------- |
| [@addTagHelper](xref:mvc/views/tag-helpers/intro#add-helper-label) | <span data-ttu-id="38516-250">Zpřístupní Pomocníci značky k zobrazení.</span><span class="sxs-lookup"><span data-stu-id="38516-250">Makes Tag Helpers available to a view.</span></span> |
| [@removeTagHelper](xref:mvc/views/tag-helpers/intro#remove-razor-directives-label) | <span data-ttu-id="38516-251">Odebere značky Pomocníci dříve přidány ze zobrazení.</span><span class="sxs-lookup"><span data-stu-id="38516-251">Removes Tag Helpers previously added from a view.</span></span> |
| [@tagHelperPrefix](xref:mvc/views/tag-helpers/intro#prefix-razor-directives-label) | <span data-ttu-id="38516-252">Určuje předponu značky, chcete-li povolit podporu pomocníků značky a vytvoření značky pomocná využití explicitní.</span><span class="sxs-lookup"><span data-stu-id="38516-252">Specifies a tag prefix to enable Tag Helper support and to make Tag Helper usage explicit.</span></span> |

## <a name="razor-reserved-keywords"></a><span data-ttu-id="38516-253">Klíčová slova Razor vyhrazena</span><span class="sxs-lookup"><span data-stu-id="38516-253">Razor reserved keywords</span></span>

### <a name="razor-keywords"></a><span data-ttu-id="38516-254">Klíčová slova Razor</span><span class="sxs-lookup"><span data-stu-id="38516-254">Razor keywords</span></span>

* <span data-ttu-id="38516-255">stránka (vyžaduje základní technologie ASP.NET 2.0 a novější)</span><span class="sxs-lookup"><span data-stu-id="38516-255">page (Requires ASP.NET Core 2.0 and later)</span></span>
* <span data-ttu-id="38516-256">– funkce</span><span class="sxs-lookup"><span data-stu-id="38516-256">functions</span></span>
* <span data-ttu-id="38516-257">dědí</span><span class="sxs-lookup"><span data-stu-id="38516-257">inherits</span></span>
* <span data-ttu-id="38516-258">model</span><span class="sxs-lookup"><span data-stu-id="38516-258">model</span></span>
* <span data-ttu-id="38516-259">section</span><span class="sxs-lookup"><span data-stu-id="38516-259">section</span></span>
* <span data-ttu-id="38516-260">pomocné rutiny (aktuálně se nepodporuje ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="38516-260">helper (Not currently supported by ASP.NET Core)</span></span>

<span data-ttu-id="38516-261">Klíčová slova Razor jsou uvozeny zpětným `@(Razor Keyword)` (například `@(functions)`).</span><span class="sxs-lookup"><span data-stu-id="38516-261">Razor keywords are escaped with `@(Razor Keyword)` (for example, `@(functions)`).</span></span>

### <a name="c-razor-keywords"></a><span data-ttu-id="38516-262">Klíčová slova jazyka C# Razor</span><span class="sxs-lookup"><span data-stu-id="38516-262">C# Razor keywords</span></span>

* <span data-ttu-id="38516-263">case</span><span class="sxs-lookup"><span data-stu-id="38516-263">case</span></span>
* <span data-ttu-id="38516-264">do</span><span class="sxs-lookup"><span data-stu-id="38516-264">do</span></span>
* <span data-ttu-id="38516-265">default</span><span class="sxs-lookup"><span data-stu-id="38516-265">default</span></span>
* <span data-ttu-id="38516-266">pro</span><span class="sxs-lookup"><span data-stu-id="38516-266">for</span></span>
* <span data-ttu-id="38516-267">foreach</span><span class="sxs-lookup"><span data-stu-id="38516-267">foreach</span></span>
* <span data-ttu-id="38516-268">if</span><span class="sxs-lookup"><span data-stu-id="38516-268">if</span></span>
* <span data-ttu-id="38516-269">else</span><span class="sxs-lookup"><span data-stu-id="38516-269">else</span></span>
* <span data-ttu-id="38516-270">lock</span><span class="sxs-lookup"><span data-stu-id="38516-270">lock</span></span>
* <span data-ttu-id="38516-271">– přepínač</span><span class="sxs-lookup"><span data-stu-id="38516-271">switch</span></span>
* <span data-ttu-id="38516-272">Zkuste</span><span class="sxs-lookup"><span data-stu-id="38516-272">try</span></span>
* <span data-ttu-id="38516-273">catch</span><span class="sxs-lookup"><span data-stu-id="38516-273">catch</span></span>
* <span data-ttu-id="38516-274">finally</span><span class="sxs-lookup"><span data-stu-id="38516-274">finally</span></span>
* <span data-ttu-id="38516-275">používání</span><span class="sxs-lookup"><span data-stu-id="38516-275">using</span></span>
* <span data-ttu-id="38516-276">while</span><span class="sxs-lookup"><span data-stu-id="38516-276">while</span></span>

<span data-ttu-id="38516-277">Klíčová slova jazyka C# Razor musí být znaky s `@(@C# Razor Keyword)` (například `@(@case)`).</span><span class="sxs-lookup"><span data-stu-id="38516-277">C# Razor keywords must be double-escaped with `@(@C# Razor Keyword)` (for example, `@(@case)`).</span></span> <span data-ttu-id="38516-278">První `@` řídicí sekvence analyzátor Razor.</span><span class="sxs-lookup"><span data-stu-id="38516-278">The first `@` escapes the Razor parser.</span></span> <span data-ttu-id="38516-279">Druhý `@` řídicí sekvence analyzátor jazyka C#.</span><span class="sxs-lookup"><span data-stu-id="38516-279">The second `@` escapes the C# parser.</span></span>

### <a name="reserved-keywords-not-used-by-razor"></a><span data-ttu-id="38516-280">Vyhrazená slova, která nepoužívá Razor</span><span class="sxs-lookup"><span data-stu-id="38516-280">Reserved keywords not used by Razor</span></span>

* <span data-ttu-id="38516-281">– obor názvů</span><span class="sxs-lookup"><span data-stu-id="38516-281">namespace</span></span>
* <span data-ttu-id="38516-282">třída</span><span class="sxs-lookup"><span data-stu-id="38516-282">class</span></span>

## <a name="viewing-the-razor-c-class-generated-for-a-view"></a><span data-ttu-id="38516-283">Zobrazení třídy Razor C# vytvořené pro zobrazení</span><span class="sxs-lookup"><span data-stu-id="38516-283">Viewing the Razor C# class generated for a view</span></span>

<span data-ttu-id="38516-284">Přidejte následující třídu do projektu ASP.NET MVC jádra:</span><span class="sxs-lookup"><span data-stu-id="38516-284">Add the following class to the ASP.NET Core MVC project:</span></span>

[!code-csharp[Main](razor/sample/Utilities/CustomTemplateEngine.cs)]

<span data-ttu-id="38516-285">Přepsání `RazorTemplateEngine` přidal MVC s `CustomTemplateEngine` třídy:</span><span class="sxs-lookup"><span data-stu-id="38516-285">Override the `RazorTemplateEngine` added by MVC with the `CustomTemplateEngine` class:</span></span>

[!code-csharp[Main](razor/sample/Startup.cs?highlight=4&range=10-14)]

<span data-ttu-id="38516-286">Nastavit bod přerušení na `return csharpDocument` prohlášení o `CustomTemplateEngine`.</span><span class="sxs-lookup"><span data-stu-id="38516-286">Set a break point on the `return csharpDocument` statement of `CustomTemplateEngine`.</span></span> <span data-ttu-id="38516-287">Při spuštění programu zastavení okamžiku přerušení, zobrazit hodnotu `generatedCode`.</span><span class="sxs-lookup"><span data-stu-id="38516-287">When program execution stops at the break point, view the value of `generatedCode`.</span></span>

![Zobrazení textu vizualizér generatedCode](razor/_static/tvr.png)

## <a name="view-lookups-and-case-sensitivity"></a><span data-ttu-id="38516-289">Zobrazení vyhledávání a rozlišování velkých a malých písmen</span><span class="sxs-lookup"><span data-stu-id="38516-289">View lookups and case sensitivity</span></span>

<span data-ttu-id="38516-290">Zobrazovací modul Razor provede malá a velká písmena vyhledávání pro zobrazení.</span><span class="sxs-lookup"><span data-stu-id="38516-290">The Razor view engine performs case-sensitive lookups for views.</span></span> <span data-ttu-id="38516-291">Nicméně skutečné vyhledávání je dáno podkladový systém souborů:</span><span class="sxs-lookup"><span data-stu-id="38516-291">However, the actual lookup is determined by the underlying file system:</span></span>

* <span data-ttu-id="38516-292">Na základě zdrojového souboru:</span><span class="sxs-lookup"><span data-stu-id="38516-292">File based source:</span></span> 
  * <span data-ttu-id="38516-293">V operačních systémech se systémy souborů malá a velká písmena (například Windows) jsou fyzický soubor poskytovatele vyhledávání malá a velká písmena.</span><span class="sxs-lookup"><span data-stu-id="38516-293">On operating systems with case insensitive file systems (for example, Windows), physical file provider lookups are case insensitive.</span></span> <span data-ttu-id="38516-294">Například `return View("Test")` výsledkem shod */Views/Home/Test.cshtml*, */Views/home/test.cshtml*a všechny ostatní variant velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="38516-294">For example, `return View("Test")` results in matches for */Views/Home/Test.cshtml*, */Views/home/test.cshtml*, and any other casing variant.</span></span>
  * <span data-ttu-id="38516-295">V systémech souborů s malá a velká písmena (například Linux, OSX a s `EmbeddedFileProvider`), hledání se malá a velká písmena.</span><span class="sxs-lookup"><span data-stu-id="38516-295">On case-sensitive file systems (for example, Linux, OSX, and with `EmbeddedFileProvider`), lookups are case-sensitive.</span></span> <span data-ttu-id="38516-296">Například `return View("Test")` konkrétně odpovídá */Views/Home/Test.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="38516-296">For example, `return View("Test")` specifically matches */Views/Home/Test.cshtml*.</span></span>
* <span data-ttu-id="38516-297">Předkompilované zobrazení: základní technologie ASP.NET 2.0 a vyšší, vyhledávání předkompilovaných zobrazení je rozlišování malých a velkých písmen pro všechny operační systémy.</span><span class="sxs-lookup"><span data-stu-id="38516-297">Precompiled views: With ASP.NET Core 2.0 and later, looking up precompiled views is case insensitive on all operating systems.</span></span> <span data-ttu-id="38516-298">Toto chování je stejné chování zprostředkovatele fyzického souboru v systému Windows.</span><span class="sxs-lookup"><span data-stu-id="38516-298">The behavior is identical to physical file provider's behavior on Windows.</span></span> <span data-ttu-id="38516-299">Pokud se dvě předkompilovaných zobrazení liší pouze v případě, výsledek vyhledávání je Nedeterministický.</span><span class="sxs-lookup"><span data-stu-id="38516-299">If two precompiled views differ only in case, the result of lookup is non-deterministic.</span></span>

<span data-ttu-id="38516-300">Vývojáři se doporučuje tak, aby odpovídaly malá a velká písmena názvů souborů a adresářů na malá a velká písmena systému:</span><span class="sxs-lookup"><span data-stu-id="38516-300">Developers are encouraged to match the casing of file and directory names to the casing of:</span></span>

    * <span data-ttu-id="38516-301">Názvy oblasti, kontroleru a akce.</span><span class="sxs-lookup"><span data-stu-id="38516-301">Area, controller, and action names.</span></span> 
    * <span data-ttu-id="38516-302">Stránky Razor.</span><span class="sxs-lookup"><span data-stu-id="38516-302">Razor Pages.</span></span>
    
<span data-ttu-id="38516-303">Přiřazení případ zajišťuje, že nasazení najít jejich zobrazení bez ohledu na podkladový systém souborů.</span><span class="sxs-lookup"><span data-stu-id="38516-303">Matching case ensures the deployments find their views regardless of the underlying file system.</span></span>