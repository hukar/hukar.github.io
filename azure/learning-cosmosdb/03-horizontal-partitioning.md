# 03 Horizontal Partitioning

## Mise à l'échelle élastique

<img src="assets/Screenshot 2020-07-28 at 08.51.28.png" alt="Screenshot 2020-07-28 at 08.51.28" style="zoom:50%;" />

<img src="assets/Screenshot 2020-07-28 at 08.54.04.png" alt="Screenshot 2020-07-28 at 08.54.04" style="zoom:33%;" />

Quand une partition est remplie dans un `container`, **Cosmos DB** en crée une nouvelle automatiquement.

Comment ces données sont réparties entre les différentes partitions ? `partition Key`.

## Choisir une `partition key`

<img src="assets/Screenshot 2020-07-28 at 09.05.37.png" alt="Screenshot 2020-07-28 at 09.05.37" style="zoom:50%;" />

Un choix judicieux permettra une mise à l'échelle très grande.

Les `items` doivent pouvoir se répartir correctement avec une bonne `partition key`.

Une `partition` réunis physiquement tous les `items` de même valeur de `partition key`.

Une partition est une limite pour les procédures stockées.

Il faut éviter les goulot d'étranglement pour le stockage et les performance => repartition uniforme des `items` dans les partitions.

<img src="assets/Screenshot 2020-07-28 at 09.17.35.png" alt="Screenshot 2020-07-28 at 09.17.35" style="zoom:33%;" />

Ici le choix de la ville comme `partition key` n'est pas forcement judicieux, car il y a des grosses villes et des petites villes.

Le code postal (`zipCode`) serait un chois plus judicieux au niveau de la repartition des données.

<img src="assets/Screenshot 2020-07-28 at 09.22.40.png" alt="Screenshot 2020-07-28 at 09.22.40" style="zoom:50%;" />

Une requête sera toujours plus efficace si elle n'impact qu'une partition (une machine physique).

La `partition key` doit être choisie en fonction des requêtes les plus courantes.

Pour un réseau social l'`userID` peut être un choix judicieux pour récupérer tous les `posts` de quelqu'un.

### Choisir la date de création : mauvaise idée

<img src="assets/Screenshot 2020-07-28 at 09.28.14.png" alt="Screenshot 2020-07-28 at 09.28.14" style="zoom:33%;" />

la répartition des données est bonne, mais par contre toutes les écritures se font sur la même partition => `hot partition`.

<img src="assets/Screenshot 2020-07-28 at 09.30.21.png" alt="Screenshot 2020-07-28 at 09.30.21" style="zoom:33%;" />

Si on a `400 RUs` de débit pour un `container`, celui-ci est distribué uniformément entre toutes les partitions.

Si on a dix partitions, le débit (`throughput`) est donc de `40RUs` , avec la **date de création** comme `partition key` on risue de vite dépasser le `throughput` alloué.

<img src="assets/Screenshot 2020-07-28 at 09.34.33.png" alt="Screenshot 2020-07-28 at 09.34.33" style="zoom:33%;" />

Avec `UserId` comme `partition key` les écritures sont uniformément réparties.

<img src="assets/Screenshot 2020-07-28 at 09.36.22.png" alt="Screenshot 2020-07-28 at 09.36.22" style="zoom:33%;" />

## Résolution de problème

<img src="assets/Screenshot 2020-07-28 at 09.43.00.png" alt="Screenshot 2020-07-28 at 09.43.00" style="zoom:33%;" />

Il est possible qu'un habitant (`tenant`) est plus de données que les autres, par exemple une grosse compagnie.

On peut alors dédier un container spécialement à ce `tenant 10` et organiser les partitions avec une autre `partition key`.

<img src="assets/Screenshot 2020-07-28 at 09.46.51.png" alt="Screenshot 2020-07-28 at 09.46.51" style="zoom:33%;" />

ce `container` possède alors son propre débit (`throughput`).

## Cross Partition Query

<img src="assets/Screenshot 2020-07-28 at 09.52.06.png" alt="Screenshot 2020-07-28 at 09.52.06" style="zoom:33%;" />

`fan-out execution` : déployer l'exécution.

Une requête  Cross-Partition sera exécuté à travers plusieurs machines physique, elle sera donc plus coûteuse qu'une requête sur une même partition.



## Changer de `partition key`

<img src="assets/Screenshot 2020-07-28 at 10.42.14.png" alt="Screenshot 2020-07-28 at 10.42.14" style="zoom:50%;" />

La `partition key ` ne peut pas être changée.

Il est donc préférable de créer une propriété `pk` avec une copie de la valeur de la `partition key` réel choisie.

Il faut toujours utiliser un `guid` comme propriété `id` pour éviter les collisions en cas de migration sur place.

