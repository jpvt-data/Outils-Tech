# ETL/ELT – DBT Seeds

## Introduction
En complément des **modèles** et des **sources**, DBT offre la possibilité d’importer directement des tables statiques grâce aux **seeds**. Ces seeds sont de simples fichiers CSV placés dans le dossier `seeds/`, puis chargés et versionnés avec votre code. Ils permettent d’inclure des listes, des tableaux de référence ou encore des données externes (comme des règles de catégorisation) sans dépendre d’une autre base ou d’un autre service.

---

## Objectifs
- **Comprendre** l’importance des seeds pour gérer des données statiques dans un projet DBT.  
- **Configurer** un seed (fichier CSV) et l’importer dans le data warehouse.  
- **Utiliser** ces données statiques dans des modèles DBT, pour des analyses ou des transformations.

---

## Sommaire
1. [Qu’est-ce qu’un seed ?](#quest-ce-quun-seed-)
2. [Configuration et utilisation des seeds](#configuration-et-utilisation-des-seeds)
3. [Exécution des seeds](#exécution-des-seeds)

---

## Qu’est-ce qu’un seed ?
Un **seed** est un fichier CSV placé dans le dossier `seeds/` de votre projet DBT, qui peut être **automatiquement importé** dans votre entrepôt de données. Vous pouvez alors manipuler ces données comme s’il s’agissait de n’importe quelle autre table, que ce soit pour des analyses, des jointures ou des tests.

### Exemples de cas d’usage
- **Codes ISO** de pays (pour normaliser les adresses).  
- **Taux de conversion** monétaires (mise à jour périodique).  
- **Catégories de Pokémon** (par exemple, Plante, Feu, Eau, etc.).  
- **Règles business** (seuils, classifieurs).

---

## Configuration et utilisation des seeds
### 1. Créer un fichier CSV
Dans votre dossier `seeds/`, placez un fichier CSV, par exemple `pokemon_types.csv`, contenant :

```csv
type_key,description
GRASS,"Correspond aux Pokémon de type Plante"
FIRE,"Correspond aux Pokémon de type Feu"
WATER,"Correspond aux Pokémon de type Eau"
```

### 2. Lancer la commande `dbt seed`
Depuis la racine de votre projet DBT :
```bash
dbt seed
```
DBT va importer chaque fichier CSV du dossier `seeds/` dans votre base de données.  
Le nom de la table créée (ou mise à jour) correspondra au nom du fichier (sans l’extension).  
Dans cet exemple, vous obtiendrez une table `pokemon_types`.

### 3. Paramétrer la matérialisation ou d’autres options
Comme pour les modèles, vous pouvez **spécifier** la matérialisation (`table` ou `view`) ou d’autres paramètres dans votre `dbt_project.yml`. Par exemple :

```yaml
seeds:
  my_dbt_project:
    +materialized: table
    +quote_columns: true
```

*(Paramètres facultatifs, adaptables à vos besoins.)*

---

## Exécution des seeds
### 1. Utiliser la table seed dans un modèle
Une fois importée, la table `pokemon_types` peut être référencée comme n’importe quel autre objet DBT :

```sql
WITH types_data AS (
    SELECT *
    FROM {{ ref('pokemon_types') }}
)

SELECT *
FROM types_data
```
Ainsi, vous pouvez **joindre** ou **croiser** ces données statiques à d’autres tables transformées par DBT.

### 2. Commandes utiles
- `dbt seed --select pokemon_types` : n’exécuter que le seed nommé `pokemon_types`.  
- `dbt seed --full-refresh` : recharger complètement le seed, même si la table existe déjà.  

---

## Conclusion
Les **DBT seeds** offrent une solution simple et élégante pour **intégrer des données statiques** à votre projet. En stockant ces tables sous forme de CSV versionnés aux côtés de votre code, vous gagnez en **traçabilité**, en **collaboration** (mise à jour partagée) et en **maintenabilité**.  

Que vous gériez des listes de références Pokémon ou d’autres ensembles de données fixes, les seeds se révèlent très utiles pour centraliser et documenter ces informations au sein d’un même écosystème DBT. Combinez-les avec vos modèles et vos sources pour obtenir un pipeline de données complet, transparent et robuste !
