# Téléchargement de fichiers avec `Node`

## Sans utilisation de code tierce (`multer` ou `formidable`)

### Le `html`

`form.html`

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <form action="upload-file" method="post" enctype="multipart/form-data">
        <input type="file" name="coco"><br>
        <button type="submit">go !!</button>
    </form>
</body>

</html>
```

Pour le `input` de type `file`, préciser le `name` est obligatoire si on veut que l'upload s'effectue.

### Le server `express`

`server.js`

```js
const express = require("express");
const path = require("path");
const fs = require("fs");

const server = express();

server.get("/", (req, res) => {
  const file = path.join(__dirname, "form.html");
  res.sendFile(file);
});
```

`.sendFile` permet d'envoyer le `html` facilement.

```js
server.post("/upload-file", (req, res) => {
  console.log("file sent");
  let i = 0;

  req.on("data", chunk => {
    i++;
    console.log("chunk :", chunk);
    fs.writeFileSync(`./chunk/part_${i}.txt`, chunk.toString());
  });
```
Ici j'enregistre en brute la réponse du navigateur dans des fichiers texte.

```js
  req.on("end", () => {
    console.log("upload are finished");
    res.redirect("back");
```
`.redirect("back")` permet de revenir sur la dernière `url`visitée.

```js
  });
});

const PORT = process.env.NODE_PORT || 6060;
server.listen(PORT, console.log(`server is running on ${PORT}`));
```

à ce stade on récupère un résultat brute qu'il restera à parser.

### Résultats

`part_1.txt`

```
------WebKitFormBoundaryQzt8lL4LcYNOiSQg
Content-Disposition: form-data; name="coco"; filename="cv-2018.pdf"
Content-Type: application/pdf

%PDF-1.7
%����
3 0 obj
<</Length 2 0 R/Filter/FlateDecode/N 3/Range[0 1 0 1 0 1 ]>>
stream
xڝ�wTT��Ͻwz��0�z�.0��. Qf� �Ml��@DE�����H��b!(�`HPb0���dF�J|yy����ǽ��g�s��{��. $O./� �'�z8�W�Gб� x�� 0Y驾A��@$/7z��
```

On trouve au début du premier morceau reçu les informations importantes :

`Content-Dispositon` dans la réponse `http` permet de détérminer si c'est du `html` ou du contenu téléchargeable

Sinon utilisé dans le cas d'un formulaire `multipart/form-data` utilisé pour l'upload de fichier (voire exemple dans la réponse).

`name`

`filename`

`Content-Type`

---

`part_2.txt`

```
0000109977 00000 n 
0000111565 00000 n 
trailer
<</Size 66/Root 65 0 R/Info 50 0 R/ID[<F4BEDD181B30016A4A8126E47163848B><F4BEDD181B30016A4A8126E47163848B>]>>
startxref
111661
%%EOF

------WebKitFormBoundaryQzt8lL4LcYNOiSQg--
```



## Test avec des champs classiques

`form.html`

```html
<form action="upload-file" method="post" enctype="multipart/form-data">
    <!-- <input type="file" name="coco"><br> -->
    <input type="text" name="Coutry">
    <input type="text" name="age">
    <textarea name="story" id="story" cols="30" rows="10"></textarea>
    <button type="submit">go !!</button>
</form>
```

`part_1.txt`

```
------WebKitFormBoundaryxlR0okNuZeB59lx7
Content-Disposition: form-data; name="Coutry"

Turkish
------WebKitFormBoundaryxlR0okNuZeB59lx7
Content-Disposition: form-data; name="age"

29
------WebKitFormBoundaryxlR0okNuZeB59lx7
Content-Disposition: form-data; name="story"

My story is rich !! (°-°)/ 
J'aime le fromage de chèvre !!
Un château fort.
------WebKitFormBoundaryxlR0okNuZeB59lx7--

```

Si on ne met pas le `name` dans le `html` , le champ n'est pas envoyé :

`form.html`

```html
<form action="upload-file" method="post" enctype="multipart/form-data">
    <!-- <input type="file" name="coco"><br> -->
    <input type="text">
    <input type="text" name="age">
    <textarea name="story" id="story" cols="30" rows="10"></textarea>
    <button type="submit">go !!</button>
</form>
```

`part_1.txt`

```
------WebKitFormBoundary6Qjz1JS5Js2Z5MN8
Content-Disposition: form-data; name="age"

36
------WebKitFormBoundary6Qjz1JS5Js2Z5MN8
Content-Disposition: form-data; name="story"

J'ai retiré le name de country
------WebKitFormBoundary6Qjz1JS5Js2Z5MN8--

```

## Utilisation de `Content-Disposition` dans la réponse `http`

### Afficher un `pdf` dans le navigateur `"Content-Type"="application/pdf"`

```js
server.get("/pdf", (req, res) => {
  const pdf = path.join(__dirname, "files", "cv-2018.pdf");

  res.writeHead(200, {
    "Content-Type": "application/pdf"
  });

  const readdable = fs.createReadStream(pdf);

  readdable.pipe(res);
});
```

Avec `express.js`

```js
server.get("/pdf", (req, res) => {
  const pdf = path.join(__dirname, "files", "cv-2018.pdf");

  res.sendFile(pdf);
});
```

### Forcer le téléchargement 

### `"Content-Disposition"="attachment;filename='myfile.txt'"`

```js
server.get("/pdf/2", (req, res) => {
  const pdf = path.join(__dirname, "files", "cv-2018.pdf");

  res.writeHead(200, {
    "Content-Type": "application/pdf",
    "Content-Disposition": 'attachment; filename="titi.pdf"'
  });

  const readdable = fs.createReadStream(pdf);

  readdable.pipe(res);
});
```

`filename` : on peut choisir le nom du fichier téléchargé dans le navigateur.

avec `express.js`

```js
server.get("/pdf/2", (req, res) => {
  const pdf = path.join(__dirname, "files", "cv-2018.pdf");

  res.download(pdf);
});
```

## Méthode de parsage d'un upload de document

### Version très simple

On va juste séparer le header du body de son content.

On doit trouver la ligne vide séparant ces deux parties : `"\r\n\r\n"`

```js
server.post("/upload-file", (req, res) => {
  console.log("file sent");
    // pour gérer plusieurs chunk pour les gros fichiers
  let flagHeader = true;
  let chars = "";
  let i = 0;

  req.on("data", chunk => {
    console.log("chunk", chunk);
    console.log("chunk.toString", chunk.toString("binary"));

    // aller jusqu'au premier saut de ligne caractère "\r\n\r\n"
    while (chars !== "\r\n\r\n") {
      chars = chunk.slice(i, i + 4).toString();
      i = i + 4;
    }

    // header du body
    const headerBody = chunk.toString("binary", 0, i);
    console.log("headerBody :\n", headerBody);

    // contenu du body
    const contentBody = chunk.toString("binary", i);
    console.log("contentBody :\n", contentBody);
  });

  req.on("end", () => {
    console.log("upload are finished");
    res.redirect("back");
  });
});
```

```
server is running on 4546
file sent
chunk <Buffer 2d 2d 2d 2d 2d 2d 57 65 62 4b 69 74 46 6f 72 6d 42 6f 75 6e 64 61 72 79 5a 77 4e 4b 44 6b 41 57 41 42 6f 73 53 31 55 43 0d 0a 43 6f 6e 74 65 6e 74 2d ... 170 more bytes>
chunk.toString ------WebKitFormBoundaryZwNKDkAWABosS1UC
Content-Disposition: form-data; name="coco"; filename="tiny.txt"
Content-Type: text/plain

un petit document
chÃ¨vre (Â°Â°-Â°Â°)/
------WebKitFormBoundaryZwNKDkAWABosS1UC--
```
```

headerBody :
 ------WebKitFormBoundaryZwNKDkAWABosS1UC
Content-Disposition: form-data; name="coco"; filename="tiny.txt"
Content-Type: text/plain
```
```

contentBody :
 un petit document
chÃ¨vre (Â°Â°-Â°Â°)/
------WebKitFormBoundaryZwNKDkAWABosS1UC--

upload are finished
```

utilisation de deux méthode de `buffer` :

`.slice(debut[, fin])` renvoie la partie du `buffer` aux indices `debut` inclus et `fin` exclus, attention c'est le même `buffer`.

`.toString(encoding [, début[, fin]])` renvoie un texte encodé grâce à `encoding` de la partie du `buffer` aux indices `debut` inclus et `fin` exclus.