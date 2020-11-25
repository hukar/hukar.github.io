# 06. Composants globaux

## Import locale

<img src="assets/Screenshot 2020-11-06 at 11.49.24.png" alt="Screenshot 2020-11-06 at 11.49.24" style="zoom:33%;" />

## accès global

Il peut être intéressant de rendre l'accès à un composant global, si celui-ci est utilisé par plusieurs autres composants.

<img src="assets/Screenshot 2020-11-06 at 11.51.32.png" alt="Screenshot 2020-11-06 at 11.51.32" style="zoom:25%;" />

Les icône et les boutons sont de bon candidat à être globaux.

## Enregistrer globalement un composant

Dans `main.js` :

```js
import Vue from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'
import BaseIcon from '@/components/BaseIcon'  // on ajoute le composant

Vue.component('BaseIcon', BaseIcon) // on l'injecte dans les composants globaux

Vue.config.productionTip = false
new Vue({
    router,
    store,
    render: h => h(App),
}).$mount('#app')
```



## Enregistrement automatique des composants

Il faut installer `Lodash` :

<img src="assets/Screenshot 2020-11-06 at 12.05.54.png" alt="Screenshot 2020-11-06 at 12.05.54" style="zoom:25%;" />

`main.js`

```js
    import Vue from 'vue'
    import upperFirst from 'lodash/upperFirst'
    import camelCase from 'lodash/camelCase'
    
    const requireComponent = require.context(
      './components', // le dossier où regarder
      false, // pas de manière recursive
      /Base[A-Z]\w+\.(vue|js)$/ // BaseSomething.vue
    )
    
    requireComponent.keys().forEach(fileName => {
      const componentConfig = requireComponent(fileName)
    
      const componentName = upperFirst(
        camelCase(
          fileName.replace(/^\.\/(.*)\.\w+$/, '$1') // retire tout ce qui est avant et après
        )
      )
    
      Vue.component(
        componentName,
        componentConfig.default || componentConfig
      )
    }) 
```



## Créer un `BaseComponent` : `BaseIcon`

D'abord installer `feather-sprite.svg`

```bash
npm install feather-icons
```

On trouvera dans `node_modules` le fichier `feather-sprite.svg` qu'on copiera dans `public`.

`BaseIcon.vue`

```vue
<template>
    <div class="icon-wrapper">
        <svg class="icon" :width="width" :height="height">
            <use :href="'/feather-sprite.svg#' + name" />
        </svg>
    </div>
</template>

<script>
export default {
    props: {
        name: {
            type: String,
            required: true,
        },
        width: {
            type: [Number, String],
            default: 24,
        },
        height: {
            type: [Number, String],
            default: 24,
        },
    },
}
</script>

<style lang="scss" scoped>
.icon-wrapper {
    display: inline-flex;
    align-items: center;
    color: rgba(0, 0, 0, 0.4);
    font-size: 1rem;
    font-weight: 600;
}
.icon {
    stroke: currentColor;
    stroke-width: 2;
    stroke-linecap: round;
    stroke-linejoin: round;
    fill: none;
    margin-right: 6px;
}
</style>
```

`<use>` permet de cloner dans le `DOM` un morceau de `SVG` défini ailleurs.

<img src="assets/Screenshot 2020-11-06 at 12.45.07.png" alt="Screenshot 2020-11-06 at 12.45.07" style="zoom:33%;" />

<img src="assets/Screenshot 2020-11-06 at 12.51.09.png" alt="Screenshot 2020-11-06 at 12.51.09" style="zoom:33%;" />

