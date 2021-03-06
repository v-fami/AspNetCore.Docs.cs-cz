---
title: Migrace ověřování a identity na ASP.NET Core
author: ardalis
description: Naučte se migrovat ověřování a identitu z projektu ASP.NET MVC do projektu ASP.NET Core MVC.
ms.author: riande
ms.date: 10/14/2016
uid: migration/identity
ms.openlocfilehash: f821930dbd36de18db31104cddf34c563009a506
ms.sourcegitcommit: 9a129f5f3e31cc449742b164d5004894bfca90aa
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78661852"
---
# <a name="migrate-authentication-and-identity-to-aspnet-core"></a>Migrace ověřování a identity na ASP.NET Core

[Steve Smith](https://ardalis.com/)

V předchozím článku jsme [migrovali konfiguraci z projektu ASP.NET MVC na ASP.NET Core MVC](xref:migration/configuration). V tomto článku migrujeme funkce registrace, přihlašování a správy uživatelů.

## <a name="configure-identity-and-membership"></a>Konfigurace identity a členství

V ASP.NET MVC jsou funkce ověřování a identity nakonfigurované pomocí ASP.NET Identity v *Startup.auth.cs* a *IdentityConfig.cs*, které jsou umístěné ve složce *app_start* . Ve ASP.NET Core MVC jsou tyto funkce nakonfigurované v *Startup.cs*.

Nainstalujte `Microsoft.AspNetCore.Identity.EntityFrameworkCore` a `Microsoft.AspNetCore.Authentication.Cookies` balíčky NuGet.

Pak otevřete *Startup.cs* a aktualizujte metodu `Startup.ConfigureServices`, aby používala Entity Framework a služby identit:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    // Add EF services to the services container.
    services.AddDbContext<ApplicationDbContext>(options =>
        options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));

    services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();

     services.AddMvc();
}
```

V tomto okamžiku existují dva typy odkazované ve výše uvedeném kódu, které jsme ještě nemigrovali z projektu ASP.NET MVC: `ApplicationDbContext` a `ApplicationUser`. Vytvořte novou složku *modelů* v projektu ASP.NET Core a přidejte do ní dvě třídy odpovídající těmto typům. Verze ASP.NET MVC těchto tříd najdete v */Models/IdentityModels.cs*, ale v migrovaném projektu budeme používat jeden soubor na třídu, protože to je mnohem jasné.

*ApplicationUser.cs*:

```csharp
using Microsoft.AspNetCore.Identity.EntityFrameworkCore;

namespace NewMvcProject.Models
{
  public class ApplicationUser : IdentityUser
  {
  }
}
```

*ApplicationDbContext.cs*:

```csharp
using Microsoft.AspNetCore.Identity.EntityFrameworkCore;
using Microsoft.Data.Entity;

namespace NewMvcProject.Models
{
    public class ApplicationDbContext : IdentityDbContext<ApplicationUser>
    {
        public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
            : base(options)
        {
        }

        protected override void OnModelCreating(ModelBuilder builder)
        {
            base.OnModelCreating(builder);
            // Customize the ASP.NET Core Identity model and override the defaults if needed.
            // For example, you can rename the ASP.NET Core Identity table names and more.
            // Add your customizations after calling base.OnModelCreating(builder);
        }
    }
}
```

ASP.NET Core webový projekt MVC Starter neobsahuje mnoho přizpůsobení uživatelů nebo `ApplicationDbContext`. Při migraci reálné aplikace je také potřeba migrovat všechny vlastní vlastnosti a metody pro uživatele a `DbContext` třídy vaší aplikace, stejně jako všechny jiné třídy modelu, které vaše aplikace využívá. Například pokud má vaše `DbContext` `DbSet<Album>`, je nutné migrovat třídu `Album`.

Když jsou tyto soubory na místě, soubor *Startup.cs* se dá zkompilovat tak, že aktualizuje jeho příkazy `using`:

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Identity;
using Microsoft.AspNetCore.Hosting;
using Microsoft.EntityFrameworkCore;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
```

Naše aplikace je teď připravená podporovat ověřování a služby identit. Stačí tyto funkce zpřístupnit uživatelům.

## <a name="migrate-registration-and-login-logic"></a>Migrace logiky registrace a přihlášení

Služba identit nakonfigurovaná pro přístup k aplikacím a datům nakonfigurovaným pomocí Entity Framework a SQL Server je připravená přidat podporu pro registraci a přihlášení do aplikace. Odhlaste se [dříve v procesu migrace](xref:migration/mvc#migrate-the-layout-file) a odkomentujme odkaz na *_LoginPartial* v *_Layout. cshtml*. Nyní je čas vrátit se k tomuto kódu, odkomentovat ho a přidat v nezbytných řadičích a zobrazeních pro podporu funkcí přihlášení.

Odkomentuje `@Html.Partial` řádku v *_Layout. cshtml*:

```cshtml
      <li>@Html.ActionLink("Contact", "Contact", "Home")</li>
    </ul>
    @*@Html.Partial("_LoginPartial")*@
  </div>
</div>
```

Nyní přidejte nové zobrazení Razor s názvem *_LoginPartial* do *zobrazení/sdílená* složka:

Aktualizujte *_LoginPartial. cshtml* pomocí následujícího kódu (nahraďte celý jeho obsah):

```cshtml
@inject SignInManager<ApplicationUser> SignInManager
@inject UserManager<ApplicationUser> UserManager

@if (SignInManager.IsSignedIn(User))
{
    <form asp-area="" asp-controller="Account" asp-action="Logout" method="post" id="logoutForm" class="navbar-right">
        <ul class="nav navbar-nav navbar-right">
            <li>
                <a asp-area="" asp-controller="Manage" asp-action="Index" title="Manage">Hello @UserManager.GetUserName(User)!</a>
            </li>
            <li>
                <button type="submit" class="btn btn-link navbar-btn navbar-link">Log out</button>
            </li>
        </ul>
    </form>
}
else
{
    <ul class="nav navbar-nav navbar-right">
        <li><a asp-area="" asp-controller="Account" asp-action="Register">Register</a></li>
        <li><a asp-area="" asp-controller="Account" asp-action="Login">Log in</a></li>
    </ul>
}
```

V tuto chvíli byste měli být schopni aktualizovat web v prohlížeči.

## <a name="summary"></a>Souhrn

ASP.NET Core zavádí změny v ASP.NET Identitych funkcích. V tomto článku jste viděli, jak migrovat funkce pro správu ověřování a správy uživatelů ASP.NET Identity ASP.NET Core.
