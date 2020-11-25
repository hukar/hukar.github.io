# BB. Les commandes usuelles

### Voire les versions installée

```bash
dotnet --list-sdks
```

### Connaitre la version de `.net`

```bash
dotnet --version
```

### Créer un fichier pour changer de version dans un répertoire

```bash
dotnet new globaljson
```

### Toutes les versions installées

```bash
dotnet --info
```

### Avoir de l'aide

```bash
dotnet -h
dotnet new -h
```

### Créer un fichier de solution

```bash
dotnet new sln
```

### Créer un projet

```bash
dotnet new classlib -n <Project>
```

`-n` nom.

### Ajouter tous les projets au fichier de solution

```bash
dotnet sln add **/
```

### Lister tous les projets de la solution

```bash
sln list
```

### Ajouter une ou plusieurs référence.S à un projet

```bash
dotnet add <Project> reference <Project_path_1> <Project_path_2>
```

### Lancer un projet

```bash
dotnet run -p <Project>
```

`-p` cible un projet.

### Ajouter un package

```bash
dotnet add Persistence/ package Microsoft.EntityFrameworkCore.Sqlite --version 3.1.9

dotnet add <Project> package <Package> [--version 3.1.9]
```





## Entity Framework : `dotnet ef`

