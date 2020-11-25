# 03 controller

Si on utilise la vue, on hérite de `Controller`, mais pour une `API` on a besoin que de `ControllerBase`.

`Controllers/CharacterController.cs`

```cs
using dotnet_rpg.Models;
using Microsoft.AspNetCore.Mvc;

namespace dotnet_rpg.Controllers
{
    [ApiController] // automatique 404 error, httpresponse; enable routing
    [Route("[Controller]")]  // use name of controller
    public class CharacterController: ControllerBase
    {
        // fonctionne aussi avec un champs non static
        private static Character knight = new Character();
		
        // [HttpGet]
        public IActionResult Get() {
            // BadRequest(); 400
            // NotFound(); 404
            return Ok(knight);  // 200
        }
    }
}
```

Si la méthode `IActionResult` porte un nom explicite de méthode `HTTP`, celle-ci est déduite, pas besoin de l'attribut `[HttpGet]` au dessus.

`[Route("[Controller]")]` signifie que le nom du contrôleur est aussi le nom de la route :

```
http://localhost:5000/character
```

#### ! ce n'est pas case sensitive pour l'url

<img src="assets/Screenshot 2020-07-09 at 11.49.44.png" alt="Screenshot 2020-07-09 at 11.49.44" style="zoom:25%;" />

### Avec une liste de caractères :

```cs
using System.Collections.Generic;
using dotnet_rpg.Models;
using Microsoft.AspNetCore.Mvc;

namespace dotnet_rpg.Controllers
{
    [ApiController] // automatique 404 error, httpresponse; enable routing
    [Route("[Controller]")]  // use name of controller
    public class CharacterController: ControllerBase
    {
        private static List<Character> characters = new List<Character> {
            new Character(),
            new Character {
                Name = "Sam"
            }
        };

        public IActionResult Get() {
            return Ok(characters);  // 200
        }
    }
}
```

<img src="assets/Screenshot 2020-07-09 at 11.54.49.png" alt="Screenshot 2020-07-09 at 11.54.49" style="zoom:25%;" />

### Méthode pour un seul caractère

Ajoutons une méthode qui renvoie un seul caractère :

`controllers/CharacterController.cs`

```cs
public IActionResult GetSingle() {
    return Ok(characters[0]);
}
```

<img src="assets/Screenshot 2020-07-09 at 13.45.38.png" alt="Screenshot 2020-07-09 at 13.45.38" style="zoom:25%;" />

On obtient une erreur de type `AmbiguousMatchException` car il y a deux méthodes `GET`.

