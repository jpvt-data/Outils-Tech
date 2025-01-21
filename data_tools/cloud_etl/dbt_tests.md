# ETL/ELT – DBT Tests

## Introduction
Dans un projet DBT, la **qualité des données** est cruciale pour des analyses fiables. Après avoir organisé et construit nos modèles (voir la fiche précédente sur les DBT models), il est essentiel de mettre en place des **tests** pour valider la cohérence et l’exactitude de nos transformations.

Cette fiche va vous présenter les différents types de tests que DBT met à disposition, et vous montrer comment les configurer et les exécuter afin de garantir la **fiabilité** de vos données, qu’il s’agisse de Pokémon ou de toute autre thématique.

---

## Objectifs
- **Comprendre** l’importance des tests dans un projet DBT.  
- **Découvrir** les types de tests fournis par DBT (intégrés et personnalisés).  
- **Configurer** et exécuter ces tests pour valider vos transformations.  
- **Mettre en place** des tests sur mesure pour des besoins spécifiques.

---

## Sommaire
1. [Types de tests DBT](#types-de-tests-dbt)  
   1.1. [Tests intégrés (built-in)](#tests-intégrés-built-in)  
   1.2. [Tests personnalisés](#tests-personnalisés)  
2. [Exécution des tests](#exécution-des-tests)

---

## Types de tests DBT

### 1. Tests intégrés (built-in)
DBT propose une série de tests intégrés qu’il suffit de **déclarer** dans le fichier YAML associé à un modèle. Ces tests vérifient automatiquement certains critères sur des colonnes. Parmi les plus utilisés :

- **unique** : vérifie que chaque valeur d’une colonne est unique.  
- **not_null** : s’assure qu’aucune valeur n’est nulle.  
- **accepted_values** : contrôle que les valeurs d’une colonne appartiennent à un ensemble précis (ex. types de Pokémon : Feu, Eau, Plante…).  
- **relationships** : valide qu’une clé étrangère est présente dans une table référencée (assurer l’intégrité référentielle).

> **Note** : La version DBT Core utilisée peut être plus ancienne pour fonctionner avec `dbt-mysql`. Dans certaines versions plus récentes, la notion de `tests` évolue vers `data_tests`.

#### Exemple (built-in tests)
Supposons que nous ayons un modèle **stg_pokemon** contenant un identifiant de Pokémon et son nom. Dans le fichier `stg_pokemon.yml` :

```yaml
version: 2

models:
  - name: stg_pokemon
    columns:
      - name: pokemon_id
        tests:
          - not_null
          - unique
      - name: pokemon_name
        tests:
          - not_null
```

Ici, DBT va vérifier pour la colonne `pokemon_id` qu’elle ne contient **aucune** valeur nulle et qu’elle est **unique**. Pour `pokemon_name`, DBT s’assure qu’aucun nom ne soit vide ou manquant.

---

### 2. Tests personnalisés
Vous pouvez également créer vos **propres tests** en SQL, placés dans le dossier `tests/`. Ces tests permettent d’écrire des requêtes spécifiques à vos règles métier (Pokémon dans le bon range de niveaux, absence de dates incorrectes, etc.).

#### Exemple (test personnalisé)
Imaginons un modèle `stg_battles` listant des combats de Pokémon, dont la colonne `battle_date` ne doit jamais être dans le **futur**. On peut créer un fichier `battles_date_in_the_past.sql` :

```sql
WITH invalid_battles AS (
    SELECT *
    FROM {{ ref('stg_battles') }}
    WHERE battle_date > CURRENT_DATE
)

SELECT COUNT(*)
FROM invalid_battles
HAVING COUNT(*) > 0
```
**Principe** :  
- Cette requête sélectionne toutes les lignes dont la date de combat (`battle_date`) dépasse la date actuelle.  
- Si le résultat renvoie plus de 0 lignes, cela signifie que certaines dates sont invalides (futur), donc le test échoue.

*(Si vous n’avez pas encore le modèle `stg_battles`, créez-le ou adaptez un autre modèle pour illustrer le même type de test.)*

---

## Exécution des tests
Pour **lancer** tous les tests (intégrés et personnalisés) d’un projet DBT :

```bash
dbt test
```

DBT exécutera :
- Les tests déclarés dans les fichiers `.yml` (ex. `not_null`, `unique`, etc.).  
- Les tests SQL personnalisés présents dans le dossier `tests/`.  

En cas d’échec, un rapport détaillé vous indiquera la nature du problème.

### Sélection ciblée
Comme pour les commandes `dbt run`, vous pouvez limiter l’exécution à certains tests :
```bash
# Exécuter uniquement le test battles_date_in_the_past
dbt test --select battles_date_in_the_past
```
Vous pouvez aussi sélectionner un **dossier** (ex. `tests/pokemon_tests/*`), un **tag**, etc.

### Gestion des dépendances
- **Inclure dépendances amont** : `dbt test --select +my_model`  
- **Inclure dépendances aval** : `dbt test --select my_model+`  

*(Utile si vous voulez tester tout le “chaînage” de transformations autour d’un modèle.)*

### Résolution d’erreurs protobuf (sous MySQL)
Sur certaines configurations, vous pourriez rencontrer une **erreur JSON** liée à `protobuf`. Pour la résoudre :
```bash
pip install protobuf==4.25.5
```
Cela installe une version compatible avec votre adaptateur MySQL et évite les échecs de parsing.

---

## Conclusion
Les tests DBT sont essentiels pour maintenir la **qualité** et la **cohérence** de vos données transformées.  
- Les **tests intégrés** (built-in) permettent rapidement de vérifier des contraintes simples (unicité, non-nullité, etc.).  
- Les **tests personnalisés** offrent une flexibilité totale pour valider des règles métier plus complexes.  

Grâce à ces mécanismes, vous garantissez la fiabilité de vos pipelines ETL/ELT, que vous manipuliez des données de combats Pokémon ou toute autre source.  
N’hésitez pas à intégrer ces tests à votre routine de développement : un simple `dbt test` avant un déploiement peut vous éviter de désagréables surprises en production !
