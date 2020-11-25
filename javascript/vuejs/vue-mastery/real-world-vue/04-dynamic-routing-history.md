# 04 `Dynamic routing` et `history mode`

## Dynamic Route

<img src="assets/Screenshot 2020-09-25 at 16.13.31.png" alt="Screenshot 2020-09-25 at 16.13.31" style="zoom: 50%;" />

dans `router/index.js`

```js
const routes = [
    {
        path: '/user/:name',
        name: 'user',
        component: User,
    },
```

`:name` paramètre dynamique.

Dans `views/User.vue`

```vue
<template>
    <h1>User : {{ $route.params.name }}</h1>
</template>
```

`$route.params.nom_du_paramètre`

Dans `App.vue` :

```vue
<router-link :to="{ name: 'user', params: { name: 'Hukar' } }">
  User
</router-link>
```

<img src="assets/Screenshot 2020-09-25 at 16.29.57.png" alt="Screenshot 2020-09-25 at 16.29.57" style="zoom:50%;" />

### Passer le paramètre dans les `props`

```js
// router/inde.js
{
  path: '/user/:name',
  name: 'user',
  component: User,
  props: true, // passe $route.params aux props
},
```

```vue
// App.vue
<router-link :to="{ name: 'user', params: { name: 'Hukar' } }">
  User
</router-link>
```

```vue
// views/User.js
<template>
    <h1>User : {{ name }}</h1>
</template>

<script>
export default {
    props: ['name'],
}
</script>
```

Écriture corrigée par le **linter** :

```vue
<template>
    <h1>Hello {{ username }}</h1>
</template>
<script>
export default {
    props: {
        username: { type: String, required: true },
    },
}
</script>
```

`require-prop-types` donner un type aux propriétés.

`require-default-prop` Donner une valeur par défaut ou les mettre à `required: true`.

## Retirer le `#` des routes 

<img src="assets/Screenshot 2020-09-25 at 16.43.58.png" alt="Screenshot 2020-09-25 at 16.43.58" style="zoom:150%;" />

<img src="assets/Screenshot 2020-09-25 at 16.45.01.png" alt="Screenshot 2020-09-25 at 16.45.01" style="zoom:50%;" />

```js
const routes = [
    {
        path: '/user/:name',
        name: 'user',
        component: User,
        props: true,
    },
]

const router = new VueRouter({
    mode: 'history',
    routes,
})

export default router
```

<img src="assets/Screenshot 2020-09-25 at 16.47.26.png" alt="Screenshot 2020-09-25 at 16.47.26" style="zoom:150%;" />

Plus de `#` dans l'`URL`.

<img src="assets/Screenshot 2020-09-25 at 16.48.44.png" alt="Screenshot 2020-09-25 at 16.48.44" style="zoom:50%;" />

#### ! attention maintenant le serveur renvoie les erreurs 404 vers index.html

On doit implémenter les erreurs dans le routeur de `Vue.js`

```js
 const router = new VueRouter({
      mode: 'history',
      routes: [
        ...
        { path: '*', component: NotFoundComponent }
      ]
    })
```

Cette route `catch them all` doit être à la fin du tableau `routes`.

Le serveur doit être configuré pour renvoyer toutes les demandes vers `index.html`.

