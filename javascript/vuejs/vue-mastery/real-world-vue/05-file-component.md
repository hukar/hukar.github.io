# 05. File Component

## Anatomie

On utilise le snippet `vbase` :

<img src="assets/Screenshot 2020-11-06 at 06.48.48.png" alt="Screenshot 2020-11-06 at 06.48.48" style="zoom:33%;" />

## Préprocesseur

<img src="assets/Screenshot 2020-11-06 at 06.54.50.png" alt="Screenshot 2020-11-06 at 06.54.50" style="zoom:33%;" />

On peut définir des processeur de langage comme `Typescript`, `plug` ou `Scss`.

### Ajoutons `scss`

```vue
<style lang="scss" scoped>

</style>
```

On utilise l'interface graphique de `vue-cli` :

```bash
vue ui
```

<img src="assets/Screenshot 2020-11-06 at 06.59.34.png" alt="Screenshot 2020-11-06 at 06.59.34" style="zoom:33%;" />

On a deux package à installer : `sass-loader` et `node-sass`

<img src="assets/Screenshot 2020-11-06 at 07.01.14.png" alt="Screenshot 2020-11-06 at 07.01.14" style="zoom:33%;" />

Ces informations se trouvent sur ce site :

https://vue-loader.vuejs.org/

<img src="assets/Screenshot 2020-11-06 at 07.05.45.png" alt="Screenshot 2020-11-06 at 07.05.45" style="zoom:33%;" />

## définir des datas

snippet : `vdata`.

```vue
<template>
    <div>
        <h4>{{ title }}</h4>
    </div>
</template>

<script>
export default {
    data() {
        return {
            title: 'Park Cleanup',
        }
    },
}
</script>
```

Le `template` doit avoir un éléme,t `root` ici `div`.

## Style

Le style est `scoped` :

```vue
<style lang="scss" scoped>
h4 {
    color: greenyellow;
}
</style>
```

<img src="assets/Screenshot 2020-11-06 at 09.57.11-4653114.png" alt="Screenshot 2020-11-06 at 09.57.11" style="zoom:33%;" />

Si on retire le mot `scoped` on a :

<img src="assets/Screenshot 2020-11-06 at 10.01.33.png" alt="Screenshot 2020-11-06 at 10.01.33" style="zoom:33%;" />

La règle devient générale, elle n'est plus *scopée*.

## Composants imbriqués : `nested components`

snippet `vimport`, `vcomponent`.

```vue
        <EventCard />
    </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue'

export default {
    components: {
        EventCard,
    },
}
</script>
```

`@` représente le dossier `src`.

## Style Global

Dans la balise `<style>` de `App.vue`, sans le mot `scoped`.



## Composant et `router-link`

On peut entourer un composant avec la balise `<router-link>` pour le rendre cliquable et navigable.

```vue
<template>
    <router-link class="event-link" :to="{ name: 'Show', params: { id: '1' } }">
        <div class="event-card -shadow">
            <span class="eyebrow">@{{ event.time }} on {{ event.date }}</span>
            <h4 class="title">{{ event.title }}</h4>
            <span>{{ event.attendees.length }} attending</span>
        </div>
    </router-link>
</template>
```

