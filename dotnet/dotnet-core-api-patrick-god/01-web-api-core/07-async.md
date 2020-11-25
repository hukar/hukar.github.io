# 07 Appel asynchrone

## Utilisation des `Task<>`

Dans `ICharacterService.cs` on va entourer nos type avec `Task<>` :

```csharp
using System.Collections.Generic;
using System.Threading.Tasks;
using dotnet_rpg.Models;

namespace dotnet_rpg.Services.CharacterService
{
    public interface ICharacterService
    {
        Task<List<Character>> GetAllCharacters();

        Task<Character> GetCharacterById(int id);
        Task<List<Character>> AddCharacter(Character newCharacter);
    }
}
```

On utilise `using System.Threading.Tasks`.

On modifie aussi `CharacterService.cs` de la même manière en ajoutant le mot clé `async` :

```csharp
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using dotnet_rpg.Models;

namespace dotnet_rpg.Services.CharacterService
{
    public class CharacterService : ICharacterService
    {
        private static List<Character> characters = new List<Character> {
            new Character(),
            new Character { Id = 1, Name = "Sam" },
            new Character { Id = 2, Name = "Tom" }
        };
        
        public async Task<List<Character>> AddCharacter(Character newCharacter)
        {
            characters.Add(newCharacter);
            return characters;
        }

        public async Task<List<Character>> GetAllCharacters()
        {
            return characters;
        }

        public async Task<Character> GetCharacterById(int id)
        {
            return characters.FirstOrDefault(c => c.Id == id);
        }
    }
}
```

De même on va modifier `CharacterController.cs` et on ajoute le mot clé `await` devant l'appelle des méthodes asynchrone de `CharacterService.cs` :

```csharp
// ...
using System.Threading.Tasks;

namespace dotnet_rpg.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class CharacterController : ControllerBase
    {
        // ...

        [HttpGet("GetAll")]
        public async Task<IActionResult> Get()
        {
            return Ok(await _characterService.GetAllCharacters());
        }

        [HttpGet("{id}")]
        public async Task<IActionResult> GetSingle(int id)
        {
            return Ok(await _characterService.GetCharacterById(id));
        }

        [HttpPost]
        public async Task<IActionResult> AddCharacter(Character newCharacter)
        {
            return Ok(await _characterService.AddCharacter(newCharacter));
        }

    }
}
```

<img src="assets/Screenshot 2020-10-14 at 17.25.47.png" alt="Screenshot 2020-10-14 at 17.25.47" style="zoom:50%;" />

On récupère des métadonnées en plus.