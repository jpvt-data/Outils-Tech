# Introduction à DBT (Data Build Tool)

## Objectifs
- **Comprendre** le fonctionnement et l’utilité de DBT pour la **transformation** des données.  
- **Installer** et **configurer** DBT Core en local.  
- **Identifier** la structure d’un projet DBT et ses dossiers principaux.

---

## Sommaire
1. [Qu’est-ce que DBT ?](#quest-ce-que-dbt-)
2. [Installation de DBT](#installation-de-dbt)
3. [Structure d’un projet DBT](#structure-dun-projet-dbt-)
4. [Challenge](#challenge)

---

## Qu’est-ce que DBT ?
**DBT** (Data Build Tool) est un outil open-source dédié à la **transformation des données** dans un entrepôt de données moderne. Il s’appuie principalement sur du SQL (et du Jinja pour la partie templating) et offre :

- Une **approche développeur** : réutilisabilité, versionnement, tests, gestion des dépendances.  
- Une **puissance de modélisation** : création de tables ou vues matérialisées directement dans le data warehouse.  
- Une **structuration du travail** : organisation des transformations dans des dossiers (modèles, macros, tests, etc.).  

DBT se décline en deux versions :
- **DBT Cloud** : version hébergée, avec interface graphique et services managés.  
- **DBT Core** : version gratuite et locale, installable via `pip`.  

Dans cette fiche, nous allons nous concentrer sur **DBT Core**, qui s’exécute en local sur votre machine et se connecte à un entrepôt de données (MySQL, PostgreSQL, BigQuery, Snowflake, etc.).

---

## Installation de DBT
### 1. Pré-requis
- **Python** doit être installé (DBT Core est un package Python).  
- Un adaptateur DBT spécifique (ex. `dbt-mysql`, `dbt-postgres`) pour communiquer avec votre base de données.

### 2. Création d’un environnement virtuel
```bash
python -m venv env-pokemon-dbt
```
- Sur **MacOS / Linux** :
  ```bash
  source env-pokemon-dbt/bin/activate
  ```
- Sur **Windows** :
  ```bash
  .\env-pokemon-dbt\Scripts\activate
  ```

### 3. Installation de DBT Core et de l’adaptateur MySQL
```bash
pip install dbt-core dbt-mysql
```
Vous pouvez ensuite vérifier que DBT est bien installé :
```bash
dbt --version
```
Le terminal devrait afficher une version similaire à :
```
installed version: 1.X.X
Your version of dbt is up to date!
```

### 4. Initialisation du projet DBT
Pour **créer un nouveau projet** DBT, tapez :
```bash
dbt init
```
Répondez ensuite aux questions posées, notamment :
- **Nom du projet**  
- **Type de base de données** (ici MySQL)

Une fois validé, un nouveau dossier est créé avec des fichiers et sous-dossiers DBT.

---

## Base de données Pokémon : préparation
Avant de configurer DBT, créons (ou alimentons) une base de données **MySQL** contenant des données Pokémon. Pour l’exemple, nous allons :

1. Créer la base MySQL `my_pokemon_db`.
2. Importer des fichiers CSV fictifs contenant des infos sur des Pokémon, des dresseurs, et des combats.

### Exemple d’import avec SQLAlchemy
```python
import pandas as pd
from sqlalchemy import create_engine
from sqlalchemy_utils import database_exists, create_database

# Paramètres de connexion MySQL
nom_utilisateur = "pikachu"
mot_de_passe = "thunderbolt"
hote = "localhost"
port = 3306
base = "my_pokemon_db"

# URL de connexion
DATABASE_URI = f"mysql+pymysql://{nom_utilisateur}:{mot_de_passe}@{hote}:{port}/{base}"

# Création de l'engine
engine = create_engine(DATABASE_URI)

# Création de la base si elle n'existe pas
if not database_exists(engine.url):
    create_database(engine.url)

# Noms des tables CSV à importer
liste_tables = ["pokemon", "trainers", "battles", "items"]

for table in liste_tables:
    # Fichiers CSV hypotétiques (ou sur GitHub)
    csv_url = f"https://mon-domaine-perso.com/data/raw_{table}.csv"
    df = pd.read_csv(csv_url)
    df.to_sql(f"raw_{table}", engine, if_exists="replace", index=False)
```
> **Note** : Adaptez `csv_url`, `pikachu`, et `thunderbolt` selon votre configuration réelle.  

---

## Configuration DBT (profiles.yml)
DBT a besoin de connaître les informations de connexion à votre base de données. Un fichier `profiles.yml` est généralement créé à l’emplacement suivant :

- **Windows** : `C:/Users/<VotreNom>/.dbt/profiles.yml`
- **Mac/Linux** : `~/.dbt/profiles.yml`

Exemple minimal :
```yaml
dbt_pokemon:  # Nom de votre profil
  target: dev
  outputs:
    dev:
      type: mysql
      server: localhost
      port: 3306
      database: my_pokemon_db
      schema: my_pokemon_db
      username: pikachu
      password: thunderbolt
      driver: MySQL ODBC 8.0 ANSI Driver
```
Veillez à aligner ces valeurs avec celles de votre moteur MySQL (identifiants, nom de base, etc.).  

---

## Structure d’un projet DBT :

Une fois votre projet créé avec `dbt init`, vous retrouvez un ensemble de dossiers :

| Dossier/Fichier       | Description                                                                                  |
|-----------------------|----------------------------------------------------------------------------------------------|
| **dbt_project.yml**   | Fichier de configuration principal (paramètres, stratégies de compilation, etc.).           |
| **models/**           | Dossier contenant les modèles SQL (transformations).                                        |
| **macros/**           | Dossier pour les macros (fonctions Jinja réutilisables).                                    |
| **tests/**            | Dossier pour les tests personnalisés (vérification de la cohérence des données).            |
| **analyses/**         | Fichiers SQL pour des analyses ponctuelles (ne crée pas de tables).                         |
| **snapshots/**        | Fichiers pour capturer l’évolution d’une table (historisation).                             |
| **seeds/**            | Fichiers CSV intégrés tels quels dans la base (ex. référentiels statiques).                 |
| **logs/**             | Dossier contenant les logs lors des exécutions de DBT (run, test, etc.).                    |

### Exemple : un modèle DBT (models/pokemon_transform.sql)
```sql
{{ config(materialized='table') }}

SELECT
    raw_pokemon.id,
    UPPER(raw_pokemon.nom) as pokemon_nom,
    raw_pokemon.type_principal,
    raw_pokemon.niveau_capture,
    raw_trainers.trainer_name AS dresseur_initial
FROM {{ ref('raw_pokemon') }} raw_pokemon
LEFT JOIN {{ ref('raw_trainers') }} raw_trainers
    ON raw_pokemon.dresseur_id = raw_trainers.id
```
- `{{ ref('raw_pokemon') }}` fait référence à la table `raw_pokemon` déjà existante dans la base (créée ou gérée par DBT).  
- `materialized='table'` signifie que ce modèle génère une table matérielle dans la base.  

---

# Ressources Supplémentaires
- [Documentation Officielle DBT](https://docs.getdbt.com/)  
- [Jinja Templates](https://jinja.palletsprojects.com/) – Pour comprendre la syntaxe de templating utilisée par DBT.  
- [Référence sur SQL](https://dev.mysql.com/doc/) – Documentation MySQL.  
- [Concepts ELT/ETL](https://www.pokepedia.fr/) – Pour plus d’idées sur des données liées à Pokémon (ou tout autre thème fantaisiste).
