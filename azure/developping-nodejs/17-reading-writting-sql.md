# 17 Lecture et écriture Azure SQL et NodeJS

## Connecter la DB

On crée un dossier `data` et dedans un fichier `userdb.js`

```js
const { Connection, Request } = require("tedious");

const config = {
    authentication: {
        options: {
            userName: "weappuser",
            password: "ferTREgh56yhjju89",
        },
        type: "default",
    },
    server: "hukar-webappdb.database.windows.net",
    options: {
        database: "webappdb",
        encrypt: true,
        trustServerCertificate: false,
        rowCollectionOnRequestCompletion: true,
    },
}
```

Dans une vraie application les credentials et le serveur ne sont pas codés en dur mais accessible via des variables d'environnement.

```js

// mapping for use async/await syntax
const getConnection = async () => {
    return new Promise((resolve, reject) => {
        const connection = new Connection(config);
        connection.on('connect', (err) => {
            if(err) {
                reject(err);
            } else {
                resolve(connection);
            }
        })
    });
}
```

On crée un mapping pour utiliser `async/await`.

```js
const executeQuery = async (sql) => {
    return new Promise((resolve, reject) => {
        try {
            const connection = await getConnection();
            const request = new Request(sql, (err, rowCount, rows) => {
                if(err) {
                    reject(err);
                } else {
                    resolve({ rowCount, rows})
                }
            });
            connection.execSql(request);
        } catch(err) {
            reject(err);
        }
    });
};
```

Cette fonction va exécuter la requête `SQL`.

### Insérer des données

toujours dans le fichier `userdb.js`.

```js
module.exports.createUsers = async () => {
    const sql = `
    INSERT INTO users (name, email) VALUES ('raymond', 'raymond@titi.com')
    INSERT INTO users (name, email) VALUES ('jeannette', 'jeannette@titi.com')
    INSERT INTO users (name, email) VALUES ('boris', 'boris@titi.com')
    `;

    return await executeQuery(sql);
};
```



### Lire les données

```js
module.exports.queryUsers = async () => {
    const sql = `SELECT + FROM users`;

    return await executeQuery(sql);
};
```

## Dans `index.js`

```js
var express = require("express");
var router = express.Router();
const { queryUsers, createUsers } = require("../data/userdb");

/* GET home page. */
router
    .get("/", async (req, res, next) => {
        try {
          const { rows } = await queryUsers();
          res.send(rows);
        } catch (err) {
          res.status(500).send(err.message);
        }
    })
    .put("/", async (req, res, next) => {
      try {
        const { rowCount } = await createUsers();
        res.send(`Number of users added : ${rowCount}`);
      } catch (err) {
        res.status(500).send(err.message);
      }
    });

module.exports = router;
```

On insère les données avec `curl` :

```bash
🦄 webapp curl -X PUT localhost:3000/
Number of users added : 3
```

`-X` use the specified proxy.

On obtient dans le navigateur :

<img src="assets/Screenshot 2020-07-17 at 15.08.13.png" alt="Screenshot 2020-07-17 at 15.08.13" style="zoom:33%;" />

