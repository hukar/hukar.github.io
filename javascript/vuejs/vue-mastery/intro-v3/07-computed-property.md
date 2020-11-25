# 07 Propriétés calculées

Une propriété calculée permet d'encapsuler la logique d'une propriété obtenu à partir d'autres propriétés.

## Calculé le titre

On ajoute à l'objet d'options la clé `computed` :

```js
const app = Vue.createApp({
  data() {
    return {
      key: value
    }
  },
  methods: {
    myMethod() {
      
    },
    mySecondMethod() {
      
    }
  },
  computed: {
    title() {
      return this.key + 'is the title'
    }
  }
})
```

```js
const app = Vue.createApp({
    data() {
        return {
            product: 'Socks',
            brand: 'Vue Mastery',
            // ...
        }
    },
    methods: { /* ... */ },
    computed: {
        title() {
            return this.brand + ' -- ' + this.product
        },
    },
})
```

<img src="assets/Screenshot 2020-09-21 at 15.46.26.png" alt="Screenshot 2020-09-21 at 15.46.26" style="zoom:67%;" />

Le résultat d'une propriété calculée est mis en cache pour améliorer les performances.