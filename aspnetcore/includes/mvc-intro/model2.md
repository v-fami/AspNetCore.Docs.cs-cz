<a name="dc"></a>

<span data-ttu-id="0e5d8-101">Přidejte následující `MvcMovieContext` třídu *modely* složky:</span><span class="sxs-lookup"><span data-stu-id="0e5d8-101">Add the following `MvcMovieContext` class to the *Models* folder:</span></span>  

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Data/MvcMovieContext.cs)]


<span data-ttu-id="0e5d8-102">Předchozí kód vytvoří `DbSet` vlastnost sady entit.</span><span class="sxs-lookup"><span data-stu-id="0e5d8-102">The preceding code creates a `DbSet` property for the entity set.</span></span> <span data-ttu-id="0e5d8-103">V terminologii Entity Framework obvykle sadu entit odpovídá databázové tabulky a entity odpovídající řádek v tabulce.</span><span class="sxs-lookup"><span data-stu-id="0e5d8-103">In Entity Framework terminology, an entity set typically corresponds to a database table, and an entity corresponds to a row in the table.</span></span>

<a name="cs"></a>

### <a name="add-a-database-connection-string"></a><span data-ttu-id="0e5d8-104">Přidat připojovací řetězec databáze</span><span class="sxs-lookup"><span data-stu-id="0e5d8-104">Add a database connection string</span></span>

<span data-ttu-id="0e5d8-105">Přidat připojovací řetězec pro *appsettings.json* souboru:</span><span class="sxs-lookup"><span data-stu-id="0e5d8-105">Add a connection string to the *appsettings.json* file:</span></span>

[!code-json[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/appsettings_SQLite.json?highlight=8-10)]

### <a name="add-required-nuget-packages"></a><span data-ttu-id="0e5d8-106">Přidat požadované balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="0e5d8-106">Add required NuGet packages</span></span>

<span data-ttu-id="0e5d8-107">Spusťte následující příkaz rozhraní příkazového řádku .NET Core pro přidání SQLite a CodeGeneration.Design do projektu:</span><span class="sxs-lookup"><span data-stu-id="0e5d8-107">Run the following .NET Core CLI command to add SQLite and CodeGeneration.Design  to the project:</span></span>

```console
dotnet add package Microsoft.EntityFrameworkCore.SQLite
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
```

<span data-ttu-id="0e5d8-108">`Microsoft.VisualStudio.Web.CodeGeneration.Design` Balíčky jsou požadovány pro generování uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="0e5d8-108">The `Microsoft.VisualStudio.Web.CodeGeneration.Design` package is required for scaffolding.</span></span>

<a name="reg"></a>

### <a name="register-the-database-context"></a><span data-ttu-id="0e5d8-109">Zaregistrujte kontext databáze</span><span class="sxs-lookup"><span data-stu-id="0e5d8-109">Register the database context</span></span>

<span data-ttu-id="0e5d8-110">Přidejte následující `using` příkazů v horní části *Startup.cs*:</span><span class="sxs-lookup"><span data-stu-id="0e5d8-110">Add the following `using` statements at the top of *Startup.cs*:</span></span>

```csharp
using MvcMovie.Models;
using Microsoft.EntityFrameworkCore;
```

<span data-ttu-id="0e5d8-111">Zaregistrujte kontext databáze s [injektáž závislostí](xref:fundamentals/dependency-injection) kontejneru v `Startup.ConfigureServices`.</span><span class="sxs-lookup"><span data-stu-id="0e5d8-111">Register the database context with the [dependency injection](xref:fundamentals/dependency-injection) container in `Startup.ConfigureServices`.</span></span>

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Startup.cs?name=snippet_UseSqlite&highlight=11-12)]

<span data-ttu-id="0e5d8-112">Sestavte projekt jako kontrolu chyb.</span><span class="sxs-lookup"><span data-stu-id="0e5d8-112">Build the project as a check for errors.</span></span>