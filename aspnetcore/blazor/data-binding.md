---
title: Datová vazba ASP.NET Core Blazor
author: guardrex
description: Přečtěte si o scénářích datových vazeb pro komponenty a prvky modelu DOM v aplikacích Blazor.
monikerRange: '>= aspnetcore-3.1'
ms.author: riande
ms.custom: mvc
ms.date: 02/12/2020
no-loc:
- Blazor
- SignalR
uid: blazor/data-binding
ms.openlocfilehash: c38e6095d4e93d3eead10fa8bb0356b2113bb220
ms.sourcegitcommit: 6645435fc8f5092fc7e923742e85592b56e37ada
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77453231"
---
# <a name="aspnet-core-opno-locblazor-data-binding"></a><span data-ttu-id="10f45-103">Datová vazba ASP.NET Core Blazor</span><span class="sxs-lookup"><span data-stu-id="10f45-103">ASP.NET Core Blazor data binding</span></span>

<span data-ttu-id="10f45-104">Od [Luke Latham](https://github.com/guardrex) a [Daniel Skořepa](https://github.com/danroth27)</span><span class="sxs-lookup"><span data-stu-id="10f45-104">By [Luke Latham](https://github.com/guardrex) and [Daniel Roth](https://github.com/danroth27)</span></span>

<span data-ttu-id="10f45-105">Datové vazby na součásti a prvky modelu DOM jsou provedeny atributem [`@bind`](xref:mvc/views/razor#bind) .</span><span class="sxs-lookup"><span data-stu-id="10f45-105">Data binding to both components and DOM elements is accomplished with the [`@bind`](xref:mvc/views/razor#bind) attribute.</span></span> <span data-ttu-id="10f45-106">Následující příklad váže vlastnost `CurrentValue` k hodnotě v textovém poli:</span><span class="sxs-lookup"><span data-stu-id="10f45-106">The following example binds a `CurrentValue` property to the text box's value:</span></span>

```razor
<input @bind="CurrentValue" />

@code {
    private string CurrentValue { get; set; }
}
```

<span data-ttu-id="10f45-107">Pokud textové pole ztratí fokus, je hodnota vlastnosti aktualizována.</span><span class="sxs-lookup"><span data-stu-id="10f45-107">When the text box loses focus, the property's value is updated.</span></span>

<span data-ttu-id="10f45-108">Textové pole je aktualizováno v uživatelském rozhraní pouze v případě, že je komponenta vykreslena, nikoli v reakci na změnu hodnoty vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="10f45-108">The text box is updated in the UI only when the component is rendered, not in response to changing the property's value.</span></span> <span data-ttu-id="10f45-109">Vzhledem k tomu, že se komponenty vykreslují po spuštění kódu obslužné rutiny události, se aktualizace vlastností *obvykle* projeví v uživatelském rozhraní hned po aktivaci obslužné rutiny události.</span><span class="sxs-lookup"><span data-stu-id="10f45-109">Since components render themselves after event handler code executes, property updates are *usually* reflected in the UI immediately after an event handler is triggered.</span></span>

<span data-ttu-id="10f45-110">Použití `@bind` s vlastností `CurrentValue` (`<input @bind="CurrentValue" />`) je v podstatě ekvivalentem následujícího:</span><span class="sxs-lookup"><span data-stu-id="10f45-110">Using `@bind` with the `CurrentValue` property (`<input @bind="CurrentValue" />`) is essentially equivalent to the following:</span></span>

```razor
<input value="@CurrentValue"
    @onchange="@((ChangeEventArgs __e) => CurrentValue = 
        __e.Value.ToString())" />
        
@code {
    private string CurrentValue { get; set; }
}
```

<span data-ttu-id="10f45-111">Při vykreslení komponenty se `value` vstupního elementu dostane z vlastnosti `CurrentValue`.</span><span class="sxs-lookup"><span data-stu-id="10f45-111">When the component is rendered, the `value` of the input element comes from the `CurrentValue` property.</span></span> <span data-ttu-id="10f45-112">Pokud uživatel zadá do textového pole a změní fokus prvku, je vyvolána událost `onchange` a vlastnost `CurrentValue` je nastavena na změněnou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="10f45-112">When the user types in the text box and changes element focus, the `onchange` event is fired and the `CurrentValue` property is set to the changed value.</span></span> <span data-ttu-id="10f45-113">Ve skutečnosti je generování kódu složitější, protože `@bind` zpracovává případy, kde jsou prováděny převody typů.</span><span class="sxs-lookup"><span data-stu-id="10f45-113">In reality, the code generation is more complex because `@bind` handles cases where type conversions are performed.</span></span> <span data-ttu-id="10f45-114">V zásadě `@bind` přidruží aktuální hodnotu výrazu k atributu `value` a zpracovává změny pomocí registrované obslužné rutiny.</span><span class="sxs-lookup"><span data-stu-id="10f45-114">In principle, `@bind` associates the current value of an expression with a `value` attribute and handles changes using the registered handler.</span></span>

<span data-ttu-id="10f45-115">Kromě zpracování `onchange`ch událostí pomocí syntaxe `@bind` lze vlastnost nebo pole svázat pomocí jiných událostí zadáním atributu [`@bind-value`](xref:mvc/views/razor#bind) s parametrem `event` ([`@bind-value:event`](xref:mvc/views/razor#bind)).</span><span class="sxs-lookup"><span data-stu-id="10f45-115">In addition to handling `onchange` events with `@bind` syntax, a property or field can be bound using other events by specifying an [`@bind-value`](xref:mvc/views/razor#bind) attribute with an `event` parameter ([`@bind-value:event`](xref:mvc/views/razor#bind)).</span></span> <span data-ttu-id="10f45-116">Následující příklad váže vlastnost `CurrentValue` pro událost `oninput`:</span><span class="sxs-lookup"><span data-stu-id="10f45-116">The following example binds the `CurrentValue` property for the `oninput` event:</span></span>

```razor
<input @bind-value="CurrentValue" @bind-value:event="oninput" />

@code {
    private string CurrentValue { get; set; }
}
```

<span data-ttu-id="10f45-117">Na rozdíl od `onchange`, která je aktivována, když prvek ztratí fokus, `oninput` při změně hodnoty textového pole aktivována.</span><span class="sxs-lookup"><span data-stu-id="10f45-117">Unlike `onchange`, which fires when the element loses focus, `oninput` fires when the value of the text box changes.</span></span>

<span data-ttu-id="10f45-118">`@bind-value` v předchozím příkladu se váže:</span><span class="sxs-lookup"><span data-stu-id="10f45-118">`@bind-value` in the preceding example binds:</span></span>

* <span data-ttu-id="10f45-119">Zadaný výraz (`CurrentValue`) k atributu `value` elementu.</span><span class="sxs-lookup"><span data-stu-id="10f45-119">The specified expression (`CurrentValue`) to the element's `value` attribute.</span></span>
* <span data-ttu-id="10f45-120">Delegát události změny pro událost určenou v `@bind-value:event`.</span><span class="sxs-lookup"><span data-stu-id="10f45-120">A change event delegate to the event specified by `@bind-value:event`.</span></span>

### <a name="unparsable-values"></a><span data-ttu-id="10f45-121">Hodnoty, které nelze analyzovat</span><span class="sxs-lookup"><span data-stu-id="10f45-121">Unparsable values</span></span>

<span data-ttu-id="10f45-122">Když uživatel poskytne neanalyzovatelné hodnoty prvku DataBound, hodnota neanalyzovat se automaticky vrátí na předchozí hodnotu, když se aktivuje událost BIND.</span><span class="sxs-lookup"><span data-stu-id="10f45-122">When a user provides an unparsable value to a databound element, the unparsable value is automatically reverted to its previous value when the bind event is triggered.</span></span>

<span data-ttu-id="10f45-123">Představte si následující scénář:</span><span class="sxs-lookup"><span data-stu-id="10f45-123">Consider the following scenario:</span></span>

* <span data-ttu-id="10f45-124">Element `<input>` je vázán na typ `int` s počáteční hodnotou `123`:</span><span class="sxs-lookup"><span data-stu-id="10f45-124">An `<input>` element is bound to an `int` type with an initial value of `123`:</span></span>

  ```razor
  <input @bind="MyProperty" />

  @code {
      [Parameter]
      public int MyProperty { get; set; } = 123;
  }
  ```
* <span data-ttu-id="10f45-125">Uživatel aktualizuje hodnotu prvku tak, aby `123.45` na stránce a změnil fokus prvku.</span><span class="sxs-lookup"><span data-stu-id="10f45-125">The user updates the value of the element to `123.45` in the page and changes the element focus.</span></span>

<span data-ttu-id="10f45-126">V předchozím scénáři je hodnota elementu vrácena na `123`.</span><span class="sxs-lookup"><span data-stu-id="10f45-126">In the preceding scenario, the element's value is reverted to `123`.</span></span> <span data-ttu-id="10f45-127">Pokud je hodnota `123.45` zamítnuta ve prospěch původní hodnoty `123`, uživateli se rozumí, že jejich hodnota nebyla přijata.</span><span class="sxs-lookup"><span data-stu-id="10f45-127">When the value `123.45` is rejected in favor of the original value of `123`, the user understands that their value wasn't accepted.</span></span>

<span data-ttu-id="10f45-128">Ve výchozím nastavení se vazba vztahuje na událost `onchange` elementu (`@bind="{PROPERTY OR FIELD}"`).</span><span class="sxs-lookup"><span data-stu-id="10f45-128">By default, binding applies to the element's `onchange` event (`@bind="{PROPERTY OR FIELD}"`).</span></span> <span data-ttu-id="10f45-129">K nastavení jiné události použijte `@bind-value="{PROPERTY OR FIELD}" @bind-value:event={EVENT}`.</span><span class="sxs-lookup"><span data-stu-id="10f45-129">Use `@bind-value="{PROPERTY OR FIELD}" @bind-value:event={EVENT}` to set a different event.</span></span> <span data-ttu-id="10f45-130">Pro událost `oninput` (`@bind-value:event="oninput"`) dojde k reverzi po stisknutí klávesy, která zavádí neanalyzovatelné hodnoty.</span><span class="sxs-lookup"><span data-stu-id="10f45-130">For the `oninput` event (`@bind-value:event="oninput"`), the reversion occurs after any keystroke that introduces an unparsable value.</span></span> <span data-ttu-id="10f45-131">Při cílení na událost `oninput` s typem svázaným `int`je uživateli zabráněno v psaní `.`ho znaku.</span><span class="sxs-lookup"><span data-stu-id="10f45-131">When targeting the `oninput` event with an `int`-bound type, a user is prevented from typing a `.` character.</span></span> <span data-ttu-id="10f45-132">Znak `.` je okamžitě odebrán, takže uživatel obdrží okamžitou zpětnou vazbu, že jsou povolena pouze celá čísla.</span><span class="sxs-lookup"><span data-stu-id="10f45-132">A `.` character is immediately removed, so the user receives immediate feedback that only whole numbers are permitted.</span></span> <span data-ttu-id="10f45-133">Existují situace, kdy se hodnota `oninput` události nedoporučuje, například pokud by měl být uživatel povolen k vymazání neanalyzovatelné `<input>` hodnoty.</span><span class="sxs-lookup"><span data-stu-id="10f45-133">There are scenarios where reverting the value on the `oninput` event isn't ideal, such as when the user should be allowed to clear an unparsable `<input>` value.</span></span> <span data-ttu-id="10f45-134">K alternativám patří:</span><span class="sxs-lookup"><span data-stu-id="10f45-134">Alternatives include:</span></span>

* <span data-ttu-id="10f45-135">Nepoužívejte událost `oninput`.</span><span class="sxs-lookup"><span data-stu-id="10f45-135">Don't use the `oninput` event.</span></span> <span data-ttu-id="10f45-136">Použijte výchozí `onchange` událost (`@bind="{PROPERTY OR FIELD}"`), kde neplatnou hodnotu vrátí, dokud prvek neztratí fokus.</span><span class="sxs-lookup"><span data-stu-id="10f45-136">Use the default `onchange` event (`@bind="{PROPERTY OR FIELD}"`), where an invalid value isn't reverted until the element loses focus.</span></span>
* <span data-ttu-id="10f45-137">Vytvořte propojení s typem s možnou hodnotou null, například `int?` nebo `string`, a poskytněte vlastní logiku pro zpracování neplatných položek.</span><span class="sxs-lookup"><span data-stu-id="10f45-137">Bind to a nullable type, such as `int?` or `string`, and provide custom logic to handle invalid entries.</span></span>
* <span data-ttu-id="10f45-138">Použijte [komponentu ověřování formuláře](xref:blazor/forms-validation), například `InputNumber` nebo `InputDate`.</span><span class="sxs-lookup"><span data-stu-id="10f45-138">Use a [form validation component](xref:blazor/forms-validation), such as `InputNumber` or `InputDate`.</span></span> <span data-ttu-id="10f45-139">Komponenty ověřování formuláře mají integrovanou podporu pro správu neplatných vstupů.</span><span class="sxs-lookup"><span data-stu-id="10f45-139">Form validation components have built-in support to manage invalid inputs.</span></span> <span data-ttu-id="10f45-140">Součásti pro ověření formuláře:</span><span class="sxs-lookup"><span data-stu-id="10f45-140">Form validation components:</span></span>
  * <span data-ttu-id="10f45-141">Povolí uživateli zadání neplatných vstupů a přijetí chyb ověřování na přidruženém `EditContext`.</span><span class="sxs-lookup"><span data-stu-id="10f45-141">Permit the user to provide invalid input and receive validation errors on the associated `EditContext`.</span></span>
  * <span data-ttu-id="10f45-142">Zobrazí chyby ověřování v uživatelském rozhraní, aniž by došlo ke konfliktu s uživatelem, který zadává další data z formuláře.</span><span class="sxs-lookup"><span data-stu-id="10f45-142">Display validation errors in the UI without interfering with the user entering additional webform data.</span></span>

### <a name="format-strings"></a><span data-ttu-id="10f45-143">Řetězce formátu</span><span class="sxs-lookup"><span data-stu-id="10f45-143">Format strings</span></span>

<span data-ttu-id="10f45-144">Datové vazby fungují s <xref:System.DateTime> formátovacími řetězci pomocí [`@bind:format`](xref:mvc/views/razor#bind).</span><span class="sxs-lookup"><span data-stu-id="10f45-144">Data binding works with <xref:System.DateTime> format strings using [`@bind:format`](xref:mvc/views/razor#bind).</span></span> <span data-ttu-id="10f45-145">Jiné formátovací výrazy, jako je například Měna nebo formáty čísel, nejsou v tuto chvíli k dispozici.</span><span class="sxs-lookup"><span data-stu-id="10f45-145">Other format expressions, such as currency or number formats, aren't available at this time.</span></span>

```razor
<input @bind="StartDate" @bind:format="yyyy-MM-dd" />

@code {
    [Parameter]
    public DateTime StartDate { get; set; } = new DateTime(2020, 1, 1);
}
```

<span data-ttu-id="10f45-146">V předchozím kódu je výchozí hodnota typu pole `<input>` elementu (`type`) `text`.</span><span class="sxs-lookup"><span data-stu-id="10f45-146">In the preceding code, the `<input>` element's field type (`type`) defaults to `text`.</span></span> <span data-ttu-id="10f45-147">`@bind:format` se podporuje pro vázání následujících typů .NET:</span><span class="sxs-lookup"><span data-stu-id="10f45-147">`@bind:format` is supported for binding the following .NET types:</span></span>

* <xref:System.DateTime?displayProperty=fullName>
* <span data-ttu-id="10f45-148"><xref:System.DateTime?displayProperty=fullName>?</span><span class="sxs-lookup"><span data-stu-id="10f45-148"><xref:System.DateTime?displayProperty=fullName>?</span></span>
* <xref:System.DateTimeOffset?displayProperty=fullName>
* <span data-ttu-id="10f45-149"><xref:System.DateTimeOffset?displayProperty=fullName>?</span><span class="sxs-lookup"><span data-stu-id="10f45-149"><xref:System.DateTimeOffset?displayProperty=fullName>?</span></span>

<span data-ttu-id="10f45-150">Atribut `@bind:format` určuje formát data, který má být použit pro `value` elementu `<input>`.</span><span class="sxs-lookup"><span data-stu-id="10f45-150">The `@bind:format` attribute specifies the date format to apply to the `value` of the `<input>` element.</span></span> <span data-ttu-id="10f45-151">Formát se používá také k analýze hodnoty při výskytu události `onchange`.</span><span class="sxs-lookup"><span data-stu-id="10f45-151">The format is also used to parse the value when an `onchange` event occurs.</span></span>

<span data-ttu-id="10f45-152">Zadání formátu pro typ pole `date` se nedoporučuje, protože Blazor obsahuje integrovanou podporu pro formátování dat.</span><span class="sxs-lookup"><span data-stu-id="10f45-152">Specifying a format for the `date` field type isn't recommended because Blazor has built-in support to format dates.</span></span> <span data-ttu-id="10f45-153">Navzdory doporučení použijte formát data `yyyy-MM-dd`, aby vazba fungovala správně, pokud je zadán typ `date` pole:</span><span class="sxs-lookup"><span data-stu-id="10f45-153">In spite of the recommendation, only use the `yyyy-MM-dd` date format for binding to work correctly if a format is supplied with the `date` field type:</span></span>

```razor
<input type="date" @bind="StartDate" @bind:format="yyyy-MM-dd">
```

### <a name="parent-to-child-binding-with-component-parameters"></a><span data-ttu-id="10f45-154">Vazba nadřazený-to-podřízený s parametry komponenty</span><span class="sxs-lookup"><span data-stu-id="10f45-154">Parent-to-child binding with component parameters</span></span>

<span data-ttu-id="10f45-155">Vazba rozpoznává parametry komponenty, kde `@bind-{property}` mohou svázat hodnotu vlastnosti z nadřazené komponenty dolů až k podřízené součásti.</span><span class="sxs-lookup"><span data-stu-id="10f45-155">Binding recognizes component parameters, where `@bind-{property}` can bind a property value from a parent component down to a child component.</span></span> <span data-ttu-id="10f45-156">Vazba z podřízeného na nadřazenou položku je popsaná v tématu [vazba typu podřízená k nadřazenému s zřetězenou](#child-to-parent-binding-with-chained-bind) vazbou.</span><span class="sxs-lookup"><span data-stu-id="10f45-156">Binding from a child to a parent is covered in the [Child-to-parent binding with chained bind](#child-to-parent-binding-with-chained-bind) section.</span></span>

<span data-ttu-id="10f45-157">Následující podřízená komponenta (`ChildComponent`) má parametr `Year` součásti a `YearChanged` zpětného volání:</span><span class="sxs-lookup"><span data-stu-id="10f45-157">The following child component (`ChildComponent`) has a `Year` component parameter and `YearChanged` callback:</span></span>

```razor
<h2>Child Component</h2>

<p>Year: @Year</p>

@code {
    [Parameter]
    public int Year { get; set; }

    [Parameter]
    public EventCallback<int> YearChanged { get; set; }
}
```

<span data-ttu-id="10f45-158">`EventCallback<T>` je vysvětleno v <xref:blazor/event-handling#eventcallback>.</span><span class="sxs-lookup"><span data-stu-id="10f45-158">`EventCallback<T>` is explained in <xref:blazor/event-handling#eventcallback>.</span></span>

<span data-ttu-id="10f45-159">Následující nadřazená komponenta používá:</span><span class="sxs-lookup"><span data-stu-id="10f45-159">The following parent component uses:</span></span>

* <span data-ttu-id="10f45-160">`ChildComponent` a váže parametr `ParentYear` z nadřazené položky k parametru `Year` pro podřízenou komponentu.</span><span class="sxs-lookup"><span data-stu-id="10f45-160">`ChildComponent` and binds the `ParentYear` parameter from the parent to the `Year` parameter on the child component.</span></span>
* <span data-ttu-id="10f45-161">Událost `onclick` slouží ke spuštění metody `ChangeTheYear`.</span><span class="sxs-lookup"><span data-stu-id="10f45-161">The `onclick` event is used to trigger the `ChangeTheYear` method.</span></span> <span data-ttu-id="10f45-162">Další informace naleznete v tématu <xref:blazor/event-handling>.</span><span class="sxs-lookup"><span data-stu-id="10f45-162">For more information, see <xref:blazor/event-handling>.</span></span>

```razor
@page "/ParentComponent"

<h1>Parent Component</h1>

<p>ParentYear: @ParentYear</p>

<ChildComponent @bind-Year="ParentYear" />

<button class="btn btn-primary" @onclick="ChangeTheYear">
    Change Year to 1986
</button>

@code {
    [Parameter]
    public int ParentYear { get; set; } = 1978;

    private void ChangeTheYear()
    {
        ParentYear = 1986;
    }
}
```

<span data-ttu-id="10f45-163">Načtení `ParentComponent` vytvoří následující kód:</span><span class="sxs-lookup"><span data-stu-id="10f45-163">Loading the `ParentComponent` produces the following markup:</span></span>

```html
<h1>Parent Component</h1>

<p>ParentYear: 1978</p>

<h2>Child Component</h2>

<p>Year: 1978</p>
```

<span data-ttu-id="10f45-164">Pokud je hodnota vlastnosti `ParentYear` změněna výběrem tlačítka v `ParentComponent`, je aktualizována vlastnost `Year` `ChildComponent`.</span><span class="sxs-lookup"><span data-stu-id="10f45-164">If the value of the `ParentYear` property is changed by selecting the button in the `ParentComponent`, the `Year` property of the `ChildComponent` is updated.</span></span> <span data-ttu-id="10f45-165">Nová hodnota `Year` se vykreslí v uživatelském rozhraní, když se `ParentComponent` znovu vykreslí:</span><span class="sxs-lookup"><span data-stu-id="10f45-165">The new value of `Year` is rendered in the UI when the `ParentComponent` is rerendered:</span></span>

```html
<h1>Parent Component</h1>

<p>ParentYear: 1986</p>

<h2>Child Component</h2>

<p>Year: 1986</p>
```

<span data-ttu-id="10f45-166">Parametr `Year` je svázán, protože má doprovodnou událost `YearChanged`, která odpovídá typu `Year` parametru.</span><span class="sxs-lookup"><span data-stu-id="10f45-166">The `Year` parameter is bindable because it has a companion `YearChanged` event that matches the type of the `Year` parameter.</span></span>

<span data-ttu-id="10f45-167">Podle konvence `<ChildComponent @bind-Year="ParentYear" />` v podstatě ekvivalentem zápisu:</span><span class="sxs-lookup"><span data-stu-id="10f45-167">By convention, `<ChildComponent @bind-Year="ParentYear" />` is essentially equivalent to writing:</span></span>

```razor
<ChildComponent @bind-Year="ParentYear" @bind-Year:event="YearChanged" />
```

<span data-ttu-id="10f45-168">Obecně platí, že vlastnost může být svázána s odpovídající obslužnou rutinou události pomocí atributu `@bind-property:event`.</span><span class="sxs-lookup"><span data-stu-id="10f45-168">In general, a property can be bound to a corresponding event handler using `@bind-property:event` attribute.</span></span> <span data-ttu-id="10f45-169">Například vlastnost `MyProp` může být svázána s `MyEventHandler` pomocí následujících dvou atributů:</span><span class="sxs-lookup"><span data-stu-id="10f45-169">For example, the property `MyProp` can be bound to `MyEventHandler` using the following two attributes:</span></span>

```razor
<MyComponent @bind-MyProp="MyValue" @bind-MyProp:event="MyEventHandler" />
```

### <a name="child-to-parent-binding-with-chained-bind"></a><span data-ttu-id="10f45-170">Vazba podřízenosti k nadřazené položce s zřetězenou vazbou</span><span class="sxs-lookup"><span data-stu-id="10f45-170">Child-to-parent binding with chained bind</span></span>

<span data-ttu-id="10f45-171">Běžným scénářem je zřetězení parametru vázaného na data na element stránky ve výstupu součásti.</span><span class="sxs-lookup"><span data-stu-id="10f45-171">A common scenario is chaining a data-bound parameter to a page element in the component's output.</span></span> <span data-ttu-id="10f45-172">Tento scénář se nazývá *zřetězená vazba* , protože k více úrovním vazby dochází současně.</span><span class="sxs-lookup"><span data-stu-id="10f45-172">This scenario is called a *chained bind* because multiple levels of binding occur simultaneously.</span></span>

<span data-ttu-id="10f45-173">Zřetězenou BIND nelze implementovat s syntaxí `@bind` v elementu stránky.</span><span class="sxs-lookup"><span data-stu-id="10f45-173">A chained bind can't be implemented with `@bind` syntax in the page's element.</span></span> <span data-ttu-id="10f45-174">Obslužná rutina události a hodnota se musí zadat samostatně.</span><span class="sxs-lookup"><span data-stu-id="10f45-174">The event handler and value must be specified separately.</span></span> <span data-ttu-id="10f45-175">Nadřazená komponenta však může použít `@bind` syntaxe s parametrem komponenty.</span><span class="sxs-lookup"><span data-stu-id="10f45-175">A parent component, however, can use `@bind` syntax with the component's parameter.</span></span>

<span data-ttu-id="10f45-176">Následující součást `PasswordField` (*PasswordField. Razor*):</span><span class="sxs-lookup"><span data-stu-id="10f45-176">The following `PasswordField` component (*PasswordField.razor*):</span></span>

* <span data-ttu-id="10f45-177">Nastaví hodnotu `<input>` elementu na vlastnost `Password`.</span><span class="sxs-lookup"><span data-stu-id="10f45-177">Sets an `<input>` element's value to a `Password` property.</span></span>
* <span data-ttu-id="10f45-178">Zpřístupňuje změny vlastnosti `Password` nadřazené komponentě pomocí [vnořenou eventCallback](xref:blazor/event-handling#eventcallback).</span><span class="sxs-lookup"><span data-stu-id="10f45-178">Exposes changes of the `Password` property to a parent component with an [EventCallback](xref:blazor/event-handling#eventcallback).</span></span>
* <span data-ttu-id="10f45-179">Používá událost `onclick` slouží ke spuštění metody `ToggleShowPassword`.</span><span class="sxs-lookup"><span data-stu-id="10f45-179">Uses the `onclick` event is used to trigger the `ToggleShowPassword` method.</span></span> <span data-ttu-id="10f45-180">Další informace naleznete v tématu <xref:blazor/event-handling>.</span><span class="sxs-lookup"><span data-stu-id="10f45-180">For more information, see <xref:blazor/event-handling>.</span></span>

```razor
<h1>Child Component</h2>

Password: 

<input @oninput="OnPasswordChanged" 
       required 
       type="@(_showPassword ? "text" : "password")" 
       value="@Password" />

<button class="btn btn-primary" @onclick="ToggleShowPassword">
    Show password
</button>

@code {
    private bool _showPassword;

    [Parameter]
    public string Password { get; set; }

    [Parameter]
    public EventCallback<string> PasswordChanged { get; set; }

    private Task OnPasswordChanged(ChangeEventArgs e)
    {
        Password = e.Value.ToString();

        return PasswordChanged.InvokeAsync(Password);
    }

    private void ToggleShowPassword()
    {
        _showPassword = !_showPassword;
    }
}
```

<span data-ttu-id="10f45-181">Komponenta `PasswordField` se používá v jiné součásti:</span><span class="sxs-lookup"><span data-stu-id="10f45-181">The `PasswordField` component is used in another component:</span></span>

```razor
@page "/ParentComponent"

<h1>Parent Component</h1>

<PasswordField @bind-Password="_password" />

@code {
    private string _password;
}
```

<span data-ttu-id="10f45-182">Chcete-li provést kontrolu nebo chyby depeše v předchozím příkladu:</span><span class="sxs-lookup"><span data-stu-id="10f45-182">To perform checks or trap errors on the password in the preceding example:</span></span>

* <span data-ttu-id="10f45-183">Vytvořte pole zálohování pro `Password` (`_password` v následujícím ukázkovém kódu).</span><span class="sxs-lookup"><span data-stu-id="10f45-183">Create a backing field for `Password` (`_password` in the following example code).</span></span>
* <span data-ttu-id="10f45-184">Proveďte kontroly nebo chyby depeší ve `Password` setter.</span><span class="sxs-lookup"><span data-stu-id="10f45-184">Perform the checks or trap errors in the `Password` setter.</span></span>

<span data-ttu-id="10f45-185">Následující příklad poskytuje okamžitou zpětnou vazbu uživateli, pokud se v hodnotě hesla používá mezera:</span><span class="sxs-lookup"><span data-stu-id="10f45-185">The following example provides immediate feedback to the user if a space is used in the password's value:</span></span>

```razor
@page "/ParentComponent"

<h1>Parent Component</h1>

Password: 

<input @oninput="OnPasswordChanged" 
       required 
       type="@(_showPassword ? "text" : "password")" 
       value="@Password" />

<button class="btn btn-primary" @onclick="ToggleShowPassword">
    Show password
</button>

<span class="text-danger">@_validationMessage</span>

@code {
    private bool _showPassword;
    private string _password;
    private string _validationMessage;

    [Parameter]
    public string Password
    {
        get { return _password ?? string.Empty; }
        set
        {
            if (_password != value)
            {
                if (value.Contains(' '))
                {
                    _validationMessage = "Spaces not allowed!";
                }
                else
                {
                    _password = value;
                    _validationMessage = string.Empty;
                }
            }
        }
    }

    [Parameter]
    public EventCallback<string> PasswordChanged { get; set; }

    private Task OnPasswordChanged(ChangeEventArgs e)
    {
        Password = e.Value.ToString();

        return PasswordChanged.InvokeAsync(Password);
    }

    private void ToggleShowPassword()
    {
        _showPassword = !_showPassword;
    }
}
```

### <a name="radio-buttons"></a><span data-ttu-id="10f45-186">Přepínací tlačítka</span><span class="sxs-lookup"><span data-stu-id="10f45-186">Radio buttons</span></span>

<span data-ttu-id="10f45-187">Informace o vazbě na přepínače ve formuláři naleznete v tématu <xref:blazor/forms-validation#work-with-radio-buttons>.</span><span class="sxs-lookup"><span data-stu-id="10f45-187">For information on binding to radio buttons in a form, see <xref:blazor/forms-validation#work-with-radio-buttons>.</span></span>