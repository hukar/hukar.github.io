# Intervertir les slots de déploiement

<img src="assets/Screenshot 2020-07-16 at 11.51.53.png" alt="Screenshot 2020-07-16 at 11.51.53" style="zoom:50%;" />

Il faut cliquer sur `swap`.

Les variables d'environnement dont `Deployment slot setting` est coché ne seront pas copier lors du `swap`.

On devrait donc avoir un nouveau `MESSAGE`.

### Avant le swap

#### `staging`

<img src="assets/Screenshot 2020-07-16 at 11.54.19.png" alt="Screenshot 2020-07-16 at 11.54.19" style="zoom:50%;" />

#### `production`

<img src="assets/Screenshot 2020-07-16 at 11.54.43.png" alt="Screenshot 2020-07-16 at 11.54.43" style="zoom:50%;" />

### après le `swap`

#### `staging`

<img src="assets/Screenshot 2020-07-16 at 11.58.07.png" alt="Screenshot 2020-07-16 at 11.58.07" style="zoom:50%;" />

#### `production`

<img src="assets/Screenshot 2020-07-16 at 11.58.28.png" alt="Screenshot 2020-07-16 at 11.58.28" style="zoom:50%;" />

On voit que la variable d'environnement `MESSAGE` est restée liée à un `slots` (ici `production`). 

