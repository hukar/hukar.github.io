# 05 Méthode `POST`

```cs
[HttpPost]
public IActionResult AddCharacter(Character newCharacter) {
    characters.Add(newCharacter);

    return Ok(characters);
}
```

Maintenant avec **Postman** on envoie un nouveau caractère :

<img src="assets/Screenshot 2020-07-09 at 14.19.53.png" alt="Screenshot 2020-07-09 at 14.19.53" style="zoom: 33%;" />

On récupère l'ensemble des caractères :

<img src="assets/Screenshot 2020-07-09 at 14.20.31.png" alt="Screenshot 2020-07-09 at 14.20.31" style="zoom:33%;" />

