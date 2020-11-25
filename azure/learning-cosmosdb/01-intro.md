# 01 Introduction learning `Cosmos DB`

## résoudre le `Big Data` avec `NoSQL`

Les 3 V du `NoSQL` :

- Volume
- Variety
- Velocity

### Scale up et Scale out : Volume

| <img src="assets/Screenshot 2020-07-25 at 10.09.52.png" alt="Screenshot 2020-07-25 at 10.09.52" style="zoom: 33%;" /> | <img src="assets/Screenshot 2020-07-25 at 10.11.51.png" alt="Screenshot 2020-07-25 at 10.11.51" style="zoom:33%;" /> |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
|                                                              |                                                              |

Quand se n'est plus possible de monter en puissance (`scale up`) on doit multiplier les machines (`scale out`).

`NoSQL` permet un `scale-out`

### No schema : Variety

Les données sont hétérogènes.

###Haute disponibilité, cohérence, résilience : Velocity

Le `NoSQL` permet un accès rapide aux données.

## Qu'est qu'une DB `NoSQL` ?

<img src="assets/Screenshot 2020-07-25 at 10.20.47.png" alt="Screenshot 2020-07-25 at 10.20.47" style="zoom:50%;" />

**Distribué** : La réplication des données permet un haut débit (`throughput`), une grande disponibilité et peu de latence.

**mise à l'échelle horizontale** (`scale-out`) : le partitionnement horizontal permet virtuellement de n'avoir aucune limites de stockage et de débit.

**Sans schéma** : La structure des données n'est pas figée.

## Qu'est que `Cosmos DB` ?

<img src="assets/Screenshot 2020-07-25 at 10.28.20.png" alt="Screenshot 2020-07-25 at 10.28.20" style="zoom:50%;" />

`Cosmos DB` est une évolution de `DocumentDB`.

Elle peut être distribuée mondialement et est multi-model.

## Get Started

<img src="assets/Screenshot 2020-07-25 at 11.30.14.png" alt="Screenshot 2020-07-25 at 11.30.14" style="zoom:50%;" />

## Créer un compte `Cosmos DB`

Via Azure.

## Créer un `container`

<img src="assets/Screenshot 2020-07-25 at 12.15.57.png" alt="Screenshot 2020-07-25 at 12.15.57" style="zoom:33%;" />

Une Base de données peut contenir plusieurs `container`.

Ce qui différencie les `container` entre eux, c'est le débit (`throughput`) et la `partition key`.

### Pourquoi créer un nouveau `container` ?

Si on doit définir une nouvelle `partition key` ou si on souhaite un débit différent des `container` déjà existant.

## Créer un document

`item` et `document` sont des termes synonymes.

```json
{
  "familyName": "Snugg",
  "address": {
    "addressLine": "67642 Merry",
    "city": "Fort Worth",
    "state": "Texas",
    "zipCode": "76178"
  },
  "parents": [
    "Lotta",
    "Quill",
    "Evan",
    "Samuele",
    "Malachi"
  ],
  "kids": [
    "Patten",
    "Raynor",
    "Jade"
  ]
}
```



<img src="assets/Screenshot 2020-07-25 at 17.52.30.png" alt="Screenshot 2020-07-25 at 17.52.30" style="zoom:50%;" />

Si on ne fournit pas d'`id`, celui-ci est créé automatiquement.

### Pas de schema

Un nouvel item peut très bien avoir un nouveau champ : `pets`.

<img src="assets/Screenshot 2020-07-25 at 17.58.25.png" alt="Screenshot 2020-07-25 at 17.58.25" style="zoom:50%;" />

## Exécuter une requête

<img src="assets/Screenshot 2020-07-25 at 18.03.46.png" alt="Screenshot 2020-07-25 at 18.03.46" style="zoom:50%;" />

On clique sur le bouton `new SQL query`.

<img src="assets/Screenshot 2020-07-25 at 18.05.09.png" alt="Screenshot 2020-07-25 at 18.05.09" style="zoom:50%;" />

```sql
SELECT * FROM c WHERE c.address.city = 'Norwalk'
```

La requête renvoie un `item`.

### `IS_DEFINED`

```sql
SELECT * FROM c WHERE IS_DEFINED(c.pets)
```

renvoie les `items` où la propriété `pets` est définie.

### `ARRAY_LENGTH`

```sql
SELECT * FROM c WHERE ARRAY_LENGTH(c.kids) > 2
```

<img src="assets/Screenshot 2020-07-25 at 18.11.52.png" alt="Screenshot 2020-07-25 at 18.11.52" style="zoom:50%;" />

Deux `items` ont plus de deux `kids`.

## Multi Model

<img src="assets/Screenshot 2020-07-26 at 08.21.37.png" alt="Screenshot 2020-07-26 at 08.21.37" style="zoom:50%;" />

## Automatic Index

`Cosmos DB` indexe automatiquement toutes les propriétés dans tous les `items`.

On appelle aussi ce procédé `inverted indexing`.

<img src="assets/Screenshot 2020-07-26 at 08.45.50.png" alt="Screenshot 2020-07-26 at 08.45.50" style="zoom:50%;" />

<img src="assets/Screenshot 2020-07-26 at 08.47.06.png" alt="Screenshot 2020-07-26 at 08.47.06" style="zoom:50%;" />

