#  ETL/ELT – DBT Models

## Introduction
Dans la précédente quête consacrée à DBT, nous avons abordé l’initialisation d’un projet et la découverte de ses différentes composantes.  
Nous allons à présent nous intéresser au cœur de DBT : le dossier `models`. Il contient les fichiers SQL définissant les **transformations de données** appliquées dans le data warehouse. Ces transformations permettent de rendre les données brutes plus exploitables, en les nettoyant et en les enrichissant.

Dans DBT, chaque “modèle” (fichier `.sql`) peut être matérialisé sous forme de **vue** ou de **table**. Par ailleurs, on organise souvent le dossier `models` en **sous-dossiers** (staging, marts, etc.) afin de clarifier le rôle de chaque transformation.

---

## Objectifs
- **Comprendre** l’importance des modèles dans un projet DBT.  
- **Structurer** le dossier `models` en fonction des besoins (staging, analyses, etc.).  
- **Créer** des vues et tables matérialisées via des fichiers SQL.  
- **Documenter** et **tester** les modèles pour assurer la qualité des transformations.  
- **Mettre en pratique** le concept de *staging* pour préparer les données brutes avant l’analyse finale.

---

## Sommaire
1. [Organisation des modèles](#organisation-des-modèles)  
2. [Exemple de modèle dans DBT](#exemple-de-modèle-dans-dbt)  
3. [Vérification du modèle](#vérification-du-modèle)

---

## Organisation des modèles
Il est recommandé de répartir vos fichiers SQL (les modèles) en sous-dossiers pour faciliter la maintenance et la collaboration. Plusieurs approches existent :

- **Par domaine fonctionnel** (ex. : `pokemons`, `trainers`, `battles`).  
- **Par type de transformation** (`staging`, `intermediate`, `mart`).  
- **Par équipe** (ex. : `data_engineering_team`, `analytics_team`).  

Par exemple, si vous travaillez essentiellement sur l’univers Pokémon, vous pourrez créer un dossier `staging` pour la préparation des données brutes (`raw_pokemon`, `raw_trainers`, etc.), et un dossier `marts` où vous placerez les tables finales destinées aux analyses complexes (regroupement de stats, rapports, etc.).

---

## Exemple de modèle dans DBT
Imaginons que nous ayons une base de données MySQL contenant des tables brutes du monde Pokémon : `raw_pokemon`, `raw_trainers`, `raw_battles`, etc. Dans le cadre de l’étape de *staging*, on souhaite créer un modèle qui renomme ou filtre certaines colonnes et prépare les données pour la suite du workflow.

### 1. Créer le dossier `staging`
Dans votre projet DBT, supprimez ou renommez le dossier `example` (fourni par défaut) et remplacez-le par un dossier `staging`.  

### 2. Définir les sources
Créez (ou modifiez) un fichier `sources.yml` dans ce dossier `staging`, par exemple :

```yaml
version: 2

sources:
  - name: pokemon_data
    schema: my_dbt_db
    tables:
      - name: raw_pokemon
      - name: raw_trainers
```

**Explications** :
- `version: 2` : version actuelle du schéma YAML pour DBT.  
- `sources` : section listant les différentes **sources de données**.  
- `name: pokemon_data` : identifiant de la source (ex. “pokemon_data”).  
- `schema: my_dbt_db` : indique le schéma (ou base) où se trouvent les tables brutes.  
- `tables` : liste des tables brutes que vous comptez transformer (`raw_pokemon`, `raw_trainers`, etc.).

### 3. Créer un modèle de staging
Toujours dans le dossier `staging`, créez un fichier `stg_pokemon.sql` :

```sql
WITH source AS (
    SELECT *
    FROM {{ source('pokemon_data', 'raw_pokemon') }}
),

renamed AS (
    SELECT
        id AS pokemon_id,
        UPPER(name) AS pokemon_name,
        type_principal
    FROM source
)

SELECT * FROM renamed
```

#### Explication
1. **CTE `source`** : récupère toutes les colonnes de `raw_pokemon`.  
2. **CTE `renamed`** : renomme certaines colonnes (ex. `id` → `pokemon_id`) et modifie la casse (`UPPER(name)`).  
3. **SELECT final** : expose le résultat du *staging* (c’est ce qu’on appellera le modèle `stg_pokemon`).

### 4. Documenter le modèle
Pour documenter ce modèle, créez un fichier `stg_pokemon.yml` dans le même dossier :

```yaml
version: 2

models:
  - name: stg_pokemon
    columns:
      - name: pokemon_id
      - name: pokemon_name
      - name: type_principal
```

Cette documentation liste simplement les colonnes du modèle. Par la suite, vous pourrez ajouter des descriptions pour apporter plus de contexte.

### 5. Configurer l’emplacement et la matérialisation
Dans votre `dbt_project.yml`, vous pouvez spécifier qu’à l’intérieur du dossier `staging`, tous les modèles seront des **vues** :

```yaml
models:
  my_dbt_project:
    staging:
      +materialized: view
```

Ainsi, tout fichier SQL contenu dans `models/staging/` sera transformé en **vue** dans la base, ce qui est pratique pour le *staging*. Pour les analyses plus poussées, vous pourrez utiliser `+materialized: table` afin de créer de vraies tables (ex. dans un dossier `marts`).

---

## Vérification du modèle
Une fois vos fichiers créés (`sources.yml`, `stg_pokemon.sql`, `stg_pokemon.yml`), vous pouvez lancer :

```bash
dbt run
```

Cela exécutera **tous les modèles** de votre projet. Si vous ne souhaitez exécuter que le modèle `stg_pokemon`, tapez :

```bash
dbt run --select stg_pokemon
```

### Options de sélection
- **Inclure dépendances amont** : `dbt run --select +stg_pokemon`  
- **Inclure dépendances aval** : `dbt run --select stg_pokemon+`  
- **Inclure les deux** : `dbt run --select +stg_pokemon+`  

Ces options permettent de gérer les dépendances entre modèles et d’exécuter uniquement la partie de la “chaîne” de transformations qui vous intéresse.

### Résultat
Si tout va bien, vous verrez une sortie indiquant la création d’une vue (ou table) nommée `stg_pokemon` dans votre base de données MySQL. Dans un client MySQL (Workbench, DBeaver, etc.), vous retrouverez cette vue dans le schéma configuré, prête à servir d’entrée pour d’autres modèles (par exemple, pour calculer des agrégations, regrouper des types de Pokémon, etc.).

---

## Conclusion
Le dossier `models` de DBT est l’élément **central** où vous définissez les transformations SQL. Grâce à une organisation par sous-dossiers (staging, marts, etc.) et une documentation `.yml`, vous rendez vos transformations plus lisibles et plus faciles à maintenir.  
En utilisant les vues pour le *staging* et les tables pour les analyses finales, vous optimisez la performance et la clarté de vos projets data.  

Vous êtes désormais prêt·e à mettre en pratique ces concepts et à créer des *pipelines* de transformation plus complexes, en associant plusieurs modèles et en exploitant au mieux les possibilités de DBT pour la qualité et l’automatisation de vos flux de données Pokémon (ou tout autre univers !).
