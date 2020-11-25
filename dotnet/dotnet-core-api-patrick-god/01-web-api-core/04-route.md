# 04 Ajouter une route

En ajoutant une route sur la première fonction `get` on résout le problème :

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
        // ...

        [Route("GetAll")]
        public IActionResult Get() {
            return Ok(characters);  
        }

        public IActionResult GetSingle() {
            return Ok(characters[0]);
        }
    }
}
```

L'`url` n'est pas sensible à la casse.

`http://localhost:5000/Character/getall` :

<img src="assets/Screenshot 2020-07-09 at 13.51.00.png" alt="Screenshot 2020-07-09 at 13.51.00" style="zoom:25%;" />

`http://localhost:5000/Character`

<img src="assets/Screenshot 2020-07-09 at 13.51.36.png" alt="Screenshot 2020-07-09 at 13.51.36" style="zoom:25%;" />

On peut spécifier la méthode explicitement en remplaçant `Route` par `HttpGet` :

```cs
[HttpGet("GetAll")]
public IActionResult Get() {
    return Ok(characters); 
}
```

## Route avec paramètres

`Controllers/CharacterController.cs`

```cs
// ...
using System.Linq;
// pour la méthode FirstOrDefault

// ...
        private static List<Character> characters = new List<Character> {
            new Character(),
            new Character {
                Id = 1,
                Name = "Sam"
            }
        };
		// ...

        [HttpGet("{id}")]
        public IActionResult GetSingle(int id) {
            return Ok(characters.FirstOrDefault(c => c.Id == id));
        }
```

On ajoute un `Id` au deuxième caractère pour pouvoir les retrouver par leur `Id`.

`using System.Linq;` permet d'utiliser `FirstOrDefault`.

Les paramètre sont mis entre accolades.

`http://localhost:5000/Character/1`

<img src="assets/Screenshot 2020-07-09 at 14.04.02.png" alt="Screenshot 2020-07-09 at 14.04.02" style="zoom:25%;" />

