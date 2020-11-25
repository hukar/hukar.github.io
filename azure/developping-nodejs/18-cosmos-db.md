# 18 Cosmos DB 

<img src="assets/Screenshot 2020-07-17 at 15.39.02.png" alt="Screenshot 2020-07-17 at 15.39.02" style="zoom:50%;" />

La particularité de Cosmos Db est de puvoir travailler avec de différentes manières.

On a aussi des options `Production` qui active des fonctionnalités :

<img src="assets/Screenshot 2020-07-17 at 15.44.41.png" alt="Screenshot 2020-07-17 at 15.44.41" style="zoom:25%;" />

<img src="assets/Screenshot 2020-07-17 at 15.44.49.png" alt="Screenshot 2020-07-17 at 15.44.49" style="zoom:25%;" />

<img src="assets/Screenshot 2020-07-17 at 15.54.47.png" alt="Screenshot 2020-07-17 at 15.54.47" style="zoom:50%;" />

On peut maintenant aller sur la ressource.

<img src="assets/Screenshot 2020-07-17 at 15.56.33.png" alt="Screenshot 2020-07-17 at 15.56.33" style="zoom:50%;" />

## Créer un conteneur

<img src="assets/Screenshot 2020-07-17 at 16.33.45.png" alt="Screenshot 2020-07-17 at 16.33.45" style="zoom:33%;" />

On a maintenant un conteneur.

<img src="assets/Screenshot 2020-07-17 at 16.35.49.png" alt="Screenshot 2020-07-17 at 16.35.49" style="zoom:50%;" />



## Relier `Cosmos Db` à son application `NodeJS`

### Installer le `sdk`

```bash
npm i @azure/cosmos
```

### Créer un CosmosClient

Dans un dossier `data` on crée le fichier `coursedb.js`

```js
const CosmosClient = require('@azure/cosmos').CosmosClient;
const coursesData = require('./courses.json');
```

Ici on importe le client Cosmos `require('@azure/cosmos').CosmosClient` et les données des cours `courses.json`

```js

```

<img src="assets/Screenshot 2020-07-17 at 17.14.53.png" alt="Screenshot 2020-07-17 at 17.14.53" style="zoom:33%;" />

Dans overview on retrouve l'`URI` :

```
https://webappcosmosdb.documents.azure.com:443/
```

<img src="assets/Screenshot 2020-07-17 at 17.16.03.png" alt="Screenshot 2020-07-17 at 17.16.03" style="zoom:50%;" />

Dans `Keys` on trouve deux clés différente mais ayant le même rôle (deux pour des raisons de stratégie de sécurité).