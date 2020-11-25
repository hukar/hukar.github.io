# 03. `DbContext`

On va créer un dossier `Data` et dedans une classe `DataContext.cs`:

<img src="assets/Screenshot 2020-11-03 at 14.41.53.png" alt="Screenshot 2020-11-03 at 14.41.53" style="zoom:33%;" />

> Le namespace doit correspondre aux dossiers : `API.Data` => `API/Data`, c'est une bonne pratique.

```csharp
using API.Entities;
using Microsoft.EntityFrameworkCore;

namespace API.Data
{
    public class DataContext : DbContext
    {
        public DataContext(DbContextOptions options) : base(options)
        {
        }

        public DbSet<AppUser> users { get; set; }
    }
}
```

On a besoin du constructeur.

`DbSet<Type>` va créer une table en `DB` du type passé.

`users` sera le nom de cette table.

## ajouter le service dans `Startup.cs`

```csharp
public void ConfigureServices(IServiceCollection services)
{

    services.AddDbContext<DataContext>(options =>
                                       {
                                           options.UseSqlite("connection string");
                                       });
    // ...
```

`"connection string"` la chaine de caractère nécessaire à `SQLite` pour être connecté.



## Déterminer le `connection string`

Le meilleur endroit pour le conserver est dans `appsettings.Development.json`.

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Data source=datingapp.db"
  },
  "Logging": { //...
```

### Modification de l'injection de configuration `Startup.cs`

Avant :

```csharp
public Startup(IConfiguration configuration)
{
    Configuration = configuration;
}

public IConfiguration Configuration { get; }
```

> Juste une question de style



Après :

```csharp
private readonly IConfiguration _config;

public Startup(IConfiguration config)
{
    _config = config;
}
```

