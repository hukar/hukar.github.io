# 07. `Slots`

Parfois on vaudrait pouvoir personnaliser un composant à chaque usage.

Les `slots` permettent d'insérer un template à l'intérieur d'un composant :

<img src="assets/Screenshot 2020-11-06 at 14.42.08.png" alt="Screenshot 2020-11-06 at 14.42.08" style="zoom: 25%;" />

Le `slot` a accès aux `data` du parent comme le montre l'exemple ci-dessous.

<img src="assets/Screenshot 2020-11-06 at 14.45.30.png" alt="Screenshot 2020-11-06 at 14.45.30" style="zoom:25%;" />

## `Named Slot`

ON peut avoir plusieurs `slots` dans un composant.

Pour que `Vue` puisse les différencier, il faut leur donner un nom.

<img src="assets/Screenshot 2020-11-06 at 14.52.18.png" alt="Screenshot 2020-11-06 at 14.52.18" style="zoom:25%;" />

On est pas obligé de nommé le deuxième `slot` car il devient évident.

<img src="assets/Screenshot 2020-11-06 at 14.54.31.png" alt="Screenshot 2020-11-06 at 14.54.31" style="zoom:25%;" />

Pour passer plusieurs éléments à un `slot`, on utilise le tag `<template>` :

<img src="assets/Screenshot 2020-11-06 at 14.55.54.png" alt="Screenshot 2020-11-06 at 14.55.54" style="zoom:25%;" />

Après tout un composant est simplement un code de `template`.

Le `<template>` évite de surcharger le `DOM` avec des `<div>` inutile.

