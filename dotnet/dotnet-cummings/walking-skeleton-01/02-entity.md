# 02. entities

Une `entity` est un abstraction d'une entité du monde physique.

`Entity Framework` utilise des conventions de nomage pour reconnaitre certain éléments :

`Id` pour une clé primaire.

On crée un dossier `Entities` et une classe `AppUser.cs`

```csharp
namespace API.Entities
{
    public class AppUser
    {
        public int Id { get; set; }
        public string UserName { get; set; }
    }
}
```

## Introduction à `Entity Framework`

<img src="assets/Screenshot 2020-11-03 at 14.18.02.png" alt="Screenshot 2020-11-03 at 14.18.02" style="zoom:33%;" />

`Entity Framework` est un pont entre les classes du `Domain` et la base de données.

Les classes du `Domain` sont les `entities`.

La classe la plus importante de `Entity Framewoork` est `DbContext`.

`Entity Framework` offre des méthodes qui abstraient le `SQL` nécessaire.

Le provider ici `Sqlite Provider` va traduire dans le langage `SQL` compatible avec la `DB`.

## Fonctionnalités d'`EF`

- Utilisation de `Linq` pour les requêtes.
- Guette les changements.
- Sauve les objets en `BD`.
- Utilise automatiquement la concurrence.
- Utilise les transactions.
- Possède du cache (si une même requête est soumise deux fois, conserve les données dans un cache).
- Intègre des conventions (comme pour `Id`).
- Ces conventions sont configurables.
- Permet de créer des migrations (`code first`) pour créer des `DB` à partir du code pré-existant.

## Installer `EF`

```bash
dotnet add API/ package Microsoft.EntityFrameworkCore.Sqlite --version 5.0.0-rc.2.20475.6
```

Attention que la version de `EF` corresponde bien à celle de `.net`.

<img src="assets/Screenshot 2020-11-03 at 14.39.01.png" alt="Screenshot 2020-11-03 at 14.39.01" style="zoom:33%;" />

