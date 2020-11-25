# 09 events

## Communication vers un parent

<img src="assets/Screenshot 2020-09-22 at 13.54.37.png" alt="Screenshot 2020-09-22 at 13.54.37" style="zoom:50%;" />

On emmet un événement avec `$emit` et le parent écoute avec `@add-to-cart`, on passe alors le nom d'une méthode à l'écouteur d'évènement.

<img src="assets/Screenshot 2020-09-22 at 13.56.17.png" alt="Screenshot 2020-09-22 at 13.56.17" style="zoom:50%;" />

## Passer un paramètre

```js
methods: {
    addToCart() {
        this.$emit("add-to-cart", this.variants[this.selectedVariant].id);
    },
```

dans `main.js` :

```js
methods: {
    updateCart(id) {
        this.cart.push(id);
    },
```

Le `cart` affiche maintenant un tableau :

<img src="assets/Screenshot 2020-09-22 at 14.03.40.png" alt="Screenshot 2020-09-22 at 14.03.40" style="zoom:50%;" />

