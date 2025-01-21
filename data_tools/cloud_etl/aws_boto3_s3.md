# Cloud Computing : AWS Boto3 pour S3

## Introduction
Dans cette nouvelle étape consacrée à la **gestion du cloud** avec AWS, vous allez découvrir **Boto3**, la bibliothèque Python officielle pour interagir avec les services Amazon Web Services. Boto3 vous permet d’effectuer des actions telles que :

- La **création** de buckets S3.  
- L’**upload**, le **download**, et la **suppression** de fichiers (objets) dans des buckets.  
- La **gestion** et la **suppression** de buckets.  

Tout cela sans devoir passer par la console AWS ou l’AWS CLI : vous contrôlez tout via des scripts Python. C’est un outil essentiel pour automatiser vos tâches cloud et maintenir une infrastructure fiable et sécurisée.

---

## Objectifs
- **Installer** et **configurer** Boto3 pour automatiser les services AWS (S3) avec Python.  
- **Créer** et **gérer** des buckets S3 à la volée (création, listage, suppression).  
- **Transférer** des fichiers (upload/download/suppression) entre votre machine locale et S3.  
- **Mettre en place** de bonnes pratiques de sécurité (gestion des droits et accès).  
- **Comprendre** comment résoudre les erreurs courantes liées à Boto3 et AWS S3.

---

## Sommaire

1. [Configuration de Boto3](#configuration-de-boto3)  
   1.1 [Prérequis](#prérequis)  
   1.2 [Créer un nouvel environnement de travail](#1-créer-un-nouvel-environnement-de-travail)  
   1.3 [Installer Boto3](#installer-boto3)  
   1.4 [Créer un script Python](#2-créez-un-script)  
2. [Boto3 et S3](#boto3-et-s3)  
   - [Créer un bucket S3 avec Boto3](#créer-un-bucket-s3-avec-boto3)  
   - [Lister les buckets S3](#lister-les-buckets-s3)  
   - [Uploader un fichier dans un bucket S3](#uploader-un-fichier-dans-un-bucket-s3)  
   - [Télécharger un fichier depuis un bucket S3](#télécharger-un-fichier-depuis-un-bucket-s3)  
   - [Supprimer un fichier d’un bucket S3](#supprimer-un-fichier-dun-bucket-s3)  
   - [Supprimer un bucket S3](#supprimer-un-bucket-s3)  
3. [Ressources utiles de la quête](#ressources-utiles-de-la-quête)

---

## Configuration de Boto3

### Prérequis
- **Python** installé (vérifiez avec `python --version`).  
- **Clés d’accès AWS IAM** (Access Key ID et Secret Access Key) liées à un utilisateur IAM autorisé à gérer S3.  
- **AWS CLI configuré** (via `aws configure`) pour avoir vos identifiants IAM disponibles sur la machine.

---

### 1. Créer un nouvel environnement de travail

#### a. Créer un dossier
Créez un dossier, par exemple `boto3_quete` :
```bash
mkdir boto3_quete
cd boto3_quete
```
*(Vous pouvez aussi le créer manuellement si vous préférez.)*

#### b. Créer un environnement virtuel
```bash
python -m venv env
```
Activez ensuite l’environnement virtuel :  
- **Windows** :  
  ```bash
  .\env\Scripts\activate
  ```  
- **macOS / Linux** :  
  ```bash
  source env/bin/activate
  ```

---

### Installer Boto3
Dans votre environnement virtuel actif, installez la bibliothèque :
```bash
pip install boto3
```

---

### 2. Créez un script
Créez un script Python, par exemple `mon_script_boto.py`, où vous stockerez vos imports et instructions Boto3.  
*(Vous pouvez également ajouter un fichier `requirements.txt` si vous souhaitez versionner vos dépendances.)*

---

## Boto3 et S3

### Créer un bucket S3 avec Boto3

```python
import boto3

# Créer une session boto3 (utilisant les credentials config. via AWS CLI)
session = boto3.Session()

# Utiliser le client S3
s3 = session.client('s3', region_name='eu-west-3')

# Nommer votre bucket (attention, le nom doit être unique au niveau mondial)
bucket_name = 'mon-nouveau-bucket-exemple-pokemon'

# Créer le bucket
s3.create_bucket(
    Bucket=bucket_name,
    CreateBucketConfiguration={
        'LocationConstraint': 'eu-west-3'
    }
)

print(f"Bucket '{bucket_name}' créé avec succès.")
```

**Explications** :  
- `boto3.Session()` récupère par défaut vos credentials IAM depuis la config locale (`~/.aws/credentials`).  
- `region_name='eu-west-3'` (Paris), vous pouvez adapter selon vos besoins.  
- `create_bucket` prend un paramètre `Bucket` (nom du bucket) et éventuellement `CreateBucketConfiguration` (région).

---

### Lister les buckets S3

```python
import boto3

session = boto3.Session()
s3 = session.client('s3')

response = s3.list_buckets()

print("Liste des buckets S3 :")
for bucket in response['Buckets']:
    print(f" - {bucket['Name']}")
```

**Explications** :  
- `s3.list_buckets()` renvoie un dictionnaire avec la clé `'Buckets'` contenant la liste de vos buckets.  
- On itère dessus pour afficher leurs noms.

---

### Uploader un fichier dans un bucket S3

```python
import boto3

session = boto3.Session()
s3 = session.client('s3')

file_name = 'pokemons_data.csv'  # Fichier local
bucket_name = 'mon-nouveau-bucket-exemple-pokemon'

# Nom du fichier tel qu’il sera stocké dans S3
s3_file_name = 'pokemons_in_safari_zone.csv'

s3.upload_file(file_name, bucket_name, s3_file_name)

print(f"Fichier '{file_name}' uploadé avec succès dans le bucket '{bucket_name}' sous le nom '{s3_file_name}'.")
```

**Explications** :  
- `file_name` : chemin vers votre fichier local (ici, un CSV listant des Pokémon).  
- `bucket_name` : nom du bucket de destination.  
- `s3_file_name` : nom que portera le fichier dans S3.

---

### Télécharger un fichier depuis un bucket S3

```python
import boto3

session = boto3.Session()
s3 = session.client('s3')

bucket_name = 'mon-nouveau-bucket-exemple-pokemon'
file_name_s3 = 'pokemons_in_safari_zone.csv'
local_file_name = 'pokemon_downloaded.csv'

s3.download_file(bucket_name, file_name_s3, local_file_name)

print(f"Fichier '{file_name_s3}' téléchargé depuis le bucket '{bucket_name}' avec succès.")
```

**Explications** :  
- `download_file` prend en paramètres (le bucket, le key dans S3, le nom de fichier local).  
- Ici, on récupère `pokemons_in_safari_zone.csv` et on le renomme `pokemon_downloaded.csv` localement.

---

### Supprimer un fichier d’un bucket S3

```python
import boto3

session = boto3.Session()
s3 = session.client('s3')

bucket_name = 'mon-nouveau-bucket-exemple-pokemon'
file_name_s3 = 'pokemons_in_safari_zone.csv'

s3.delete_object(Bucket=bucket_name, Key=file_name_s3)

print(f"Fichier '{file_name_s3}' supprimé avec succès du bucket '{bucket_name}'.")
```

**Explications** :  
- `delete_object` supprime l’objet dont la clé (`Key`) est spécifiée.  
- Le bucket doit exister et l’objet doit être présent avant de pouvoir le supprimer.

---

### Supprimer un bucket S3
Pour supprimer un bucket, il doit être **vide** (pas d’objets restants). Vérifiez ou supprimez d’abord tous les fichiers, puis :

```python
import boto3

session = boto3.Session()
s3 = session.client('s3')

bucket_name = 'mon-nouveau-bucket-exemple-pokemon'

s3.delete_bucket(Bucket=bucket_name)

print(f"Bucket '{bucket_name}' supprimé avec succès.")
```

**Explications** :  
- `delete_bucket` échouera si le bucket n’est pas vide.  
- Vous pouvez automatiser la suppression de tous les objets restants avant de l’appeler.

---

## Ressources utiles de la quête
- [Documentation Boto3](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html) – Référence officielle.  
- [AWS Python SDK code examples](https://docs.aws.amazon.com/code-samples/latest/catalog/code-catalog-python-example_code-s3.html) – Exemples S3 en Python.  
- [Guide sur les bonnes pratiques IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) – Pour sécuriser l’accès à vos ressources.  

Avec ces commandes et scripts, vous pouvez déjà automatiser une bonne partie de vos interactions avec AWS S3. Amusez-vous à gérer vos propres fichiers ; faites toutefois attention à vos droits IAM et aux coûts potentiels engendrés par la création de multiples buckets. Bonne exploration du cloud avec Boto3 !  
