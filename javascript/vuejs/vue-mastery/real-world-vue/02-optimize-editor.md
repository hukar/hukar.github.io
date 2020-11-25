# 02 Optimiser son éditeur

## Extension VSCode

### `Vetur` de Pine Yu

- syntax highlighting

- snippets `ctrl + space`
	- vue -> squelette de composant



### `eslint` et `prettier`

Pour éviter les conflits il y a une dépendance importante dans `package.json` :

```json
"@vue/eslint-config-prettier": "^6.0.0",
```



Dans `.eslintrc.js` :

```js
extends: ["plugin:vue/essential","plugin:prettier/recommended", "@vue/prettier"],
```

Un autre (quelle différence ?? => le javascript est *linté* prendre plutôt celui plus bas)

```js
extends: [
  "plugin:vue/recommende",  // vue/recommended sont des règles plus strict que /essential
  "@vue/prettier", // ADD
  "eslint:recommended" // ici le javacsript est linté
],
```

Si besoin pour éviter les conflits :

```js
"prettier/vue" // de eslint-config-prettier mais déjà injecté grace à @vue/prettier
```



Créer un fichier de configuration pour `prettier`

`.prettierrc.js`

```js
module.exports = {
  trailingComma: "es5",  // mettre une virgule à la fin des attributs d'un objets
  tabWidth: 4,
  semi: false,
  singleQuote: true,
  htmlWhitespaceSensitivity: 'ignore',  // pour éviter des chose bizarre dans le html
};
```



## User Settings

Pour éviter les conflits avec `eslint` on met `vetur validation template` à `false`.

```json
"vetur.validation.template": false
```

### Auto Fix On Save

```json
"editor.codeActionsOnSave": {
        // "source.fixAll.eslint": true
    	"source.fixAll": true  // fonctionne pour moi
    }
```

Décocher `Editor detect indentation` si nécessaire :

<img src="assets/Screenshot 2020-11-05 at 14.26.43.png" alt="Screenshot 2020-11-05 at 14.26.43" style="zoom:33%;" />

## Additional Snippets

Sarah Drasner

<img src="assets/Screenshot 2020-09-24 at 16.21.01.png" alt="Screenshot 2020-09-24 at 16.21.01" style="zoom:50%;" />

Ajouter alors ce `setting` :

