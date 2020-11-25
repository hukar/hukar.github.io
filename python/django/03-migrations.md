# 03 Les migrations

La migration sert à mettre à jour la base de données grâce aux schémas contenu dans l'application.

```bash
python manage.py migrate
```

## Ajouter notre `app` à `settings.py`

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'demo',
]
```

## Creér un modèle

Dans le fichier `models.py`

```python
from django.db import models

# Create your models here.
class Book(models.Model):
    title = models.CharField(max_length=36)
```

On crée une classe qui hérite de `models.Model`

Ensuite le champ `title` instancie la classe `models.CharField` en passant la taille de la chaîne de caractère au constructeur.

## Exécuter la commande `makemigrations`

```bash
python manage.py makemigrations
```

Cela va créer un fichier dans le dossier `migrations` de l'`app`

![Screenshot 2020-01-01 at 09.53.55](assets/Screenshot 2020-01-01 at 09.53.55.png)

`0001_initial.py`

```python
# Generated by Django 3.0.1 on 2020-01-01 08:51

from django.db import migrations, models


class Migration(migrations.Migration):

    initial = True

    dependencies = [
    ]

    operations = [
        migrations.CreateModel(
            name='Book',
            fields=[
                ('id', models.AutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                ('title', models.CharField(max_length=36)),
            ],
        ),
    ]
```

C'est un ensemble de règle pour la création de la table en base de données

## Appliquer la migration `migrate`

Pour appliquer la migration sur la base de données :

```bash
python manage.py migrate
Running migrations:
  Applying demo.0001_initial... OK
```
