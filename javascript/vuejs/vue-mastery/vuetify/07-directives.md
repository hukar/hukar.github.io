# 07 `Directives`

## `v-resize`

```vue
<template>
    <v-row v-resize="onResize" align="center" justify="center">
        <v-subheader>
            Windo size
        </v-subheader>
        {{windowSize}}
    </v-row>
</template>
<script>
    export default {
        data() {
            return {
                windowSize: {},
            }
        },
        methods: {
            onResize() {
                this.windowSize = {x: window.innerWidth, y: window.innerHeight}
            }
        }
    }
</script>
```

<img src="assets/Screenshot 2020-11-25 at 11.29.44.png" alt="Screenshot 2020-11-25 at 11.29.44" style="zoom:50%;" />

## `v-ripple`

<img src="assets/Screenshot 2020-11-25 at 11.32.52.png" alt="Screenshot 2020-11-25 at 11.32.52" style="zoom:50%;" />

Ajoute l'effet `ripple` (vague).

```html
<div v-ripple class="elevation-2 pa-12 text-center headline">
    This element HTML is Rippled
</div>
```

`headline` : 

```css
{
    font-size: 1.5rem !important;
    font-weight: 400;
    line-height: 2rem;
    letter-spacing: normal !important;
    font-family: "Roboto", sans-serif !important;
}
```



## `v-intersect`

<img src="assets/Screenshot 2020-11-25 at 11.36.55.png" alt="Screenshot 2020-11-25 at 11.36.55" style="zoom:50%;" />

Souvent du contenu sort de la fenêtre visible.

On aimerait que le contenu non-visible ne soit pas rendu dans le `DOM` :

<img src="assets/Screenshot 2020-11-25 at 11.37.59.png" alt="Screenshot 2020-11-25 at 11.37.59" style="zoom:50%;" />

Cela impact les performances.

> ### Utilisation de `Intersection Observer API`
>
> https://developer.mozilla.org/fr/docs/Web/API/Intersection_Observer_API