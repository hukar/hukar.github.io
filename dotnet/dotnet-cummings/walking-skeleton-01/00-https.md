# 00. `HTTPS`

## Lancement de l'application

```bash
dotnet run -p API/
```

Il demande la première fois un accès au `keychain`.

En `HTTPS` on obtient l'écran suivant :

<img src="../assets/Screenshot 2020-11-03 at 11.49.09.png" alt="Screenshot 2020-11-03 at 11.49.09" style="zoom:33%;" />

<img src="../assets/Screenshot 2020-11-03 at 11.50.38.png" alt="Screenshot 2020-11-03 at 11.50.38" style="zoom:33%;" />

## Générer un certificats

```bash
🦄 DatingApp dotnet dev-certs https --trust

Trusting the HTTPS development certificate was requested. If the certificate is not already trusted we will run the following command:
'sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain <<certificate>>'
This command might prompt you for your password to install the certificate on the system keychain.
Password:
A valid HTTPS certificate is already present.
```

<img src="../assets/Screenshot 2020-11-03 at 11.56.46.png" alt="Screenshot 2020-11-03 at 11.56.46" style="zoom:33%;" />

Voila maintenant le certificat est trouvé.