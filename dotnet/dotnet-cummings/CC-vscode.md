# CC. `VSCode` tips

Pour ajouter les fichiers de configuration `.vscode` :

`cmd`+`shift`+`p` => taper `assets`<img src="assets/Screenshot 2020-11-03 at 10.23.40.png" alt="Screenshot 2020-11-03 at 10.23.40" style="zoom:33%;" />

## Auto save

<img src="assets/Screenshot 2020-11-03 at 10.29.01.png" alt="Screenshot 2020-11-03 at 10.29.01" style="zoom:33%;" />

## Masquer les dossiers `bin` et `obj`

<img src="assets/Screenshot 2020-11-03 at 11.03.53.png" alt="Screenshot 2020-11-03 at 11.03.53" style="zoom:33%;" />

## Utiliser l'affichage des dossiers normal

Décocher `Compact Folder` pour ne pas avoir les dossiers vides représentés sur un ligne.

<img src="assets/Screenshot 2020-11-03 at 11.09.24.png" alt="Screenshot 2020-11-03 at 11.09.24" style="zoom:33%;" />

## Voire les constructeur disponible et les générés

<img src="assets/Screenshot 2020-11-03 at 16.05.35.png" alt="Screenshot 2020-11-03 at 16.05.35" style="zoom:33%;" />

`cmd` + `shift` + `;`

## Voire les paramètres possible (`overload`) d'une méthode

`cmd` + `shift` + `space`

<img src="assets/Screenshot 2020-11-03 at 16.16.19.png" alt="Screenshot 2020-11-03 at 16.16.19" style="zoom:33%;" />

## Configurer les membres privés `C# extension`

<img src="assets/Screenshot 2020-11-03 at 16.52.37.png" alt="Screenshot 2020-11-03 at 16.52.37" style="zoom:33%;" />

<img src="assets/Screenshot 2020-11-03 at 16.53.08.png" alt="Screenshot 2020-11-03 at 16.53.08" style="zoom:33%;" />

Résultat du code généré

```csharp
public Startup(IConfiguration config)
{
}
```

<img src="assets/Screenshot 2020-11-03 at 16.55.58.png" alt="Screenshot 2020-11-03 at 16.55.58" style="zoom:33%;" />

```csharp
private readonly IConfiguration _config;

public Startup(IConfiguration config)
{
    _config = config;
}
```

