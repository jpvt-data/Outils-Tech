# ETL/ELT – DBT Docs

## Introduction
Après avoir organisé, testé et validé la qualité de vos données dans un projet DBT, la prochaine étape consiste à **documenter** vos modèles, colonnes et sources. DBT offre une fonctionnalité de **documentation interactive** qui facilite la compréhension globale du projet et la visualisation des liens entre les différentes transformations.  

Grâce à la commande `dbt docs`, vous pouvez générer un **site web** local qui présente l’architecture de vos pipelines, y compris les modèles de staging, les tables intermédiaires et les tests de qualité.  

---

## Objectifs
- **Comprendre** l’importance de la documentation dans un projet DBT.  
- **Générer** une documentation interactive via `dbt docs generate` et `dbt docs serve`.  
- **Enrichir** la documentation avec des descriptions de modèles, de colonnes et de sources.  
- **Visualiser** le *lineage* (les liens de dépendance) entre vos transformations de données.

---

## Sommaire
1. [Génération de la documentation](#génération-de-la-documentation)  
2. [Ajouter des descriptions aux modèles et aux sources](#ajouter-des-descriptions-aux-modèles-et-aux-sources)

---

## Génération de la documentation
Une fois que vos **fichiers YAML** (et éventuels fichiers Markdown) sont bien renseignés en descriptions, lancez la commande :  
```bash
dbt docs generate
```
DBT va alors :  
- Scanner l’ensemble de vos modèles (`.sql`) et configurations (`.yml`).  
- Extraire toutes les descriptions, les dépendances, les tests associés, etc.  
- Compiler ces informations en un **paquet** (un ensemble de fichiers HTML, JSON, etc.).

Ensuite, pour **consulter** la documentation sous forme d’un site web local :  
```bash
dbt docs serve
```
DBT démarre un petit serveur. Dans votre **navigateur**, vous pourrez alors explorer :  
- Les **modèles** (tables ou vues) créés par DBT,  
- Les **colonnes** et leurs descriptions,  
- Les **tests** associés (not_null, unique…),  
- Les **sources** (tables brutes) et leurs commentaires,  
- Le **lineage** (graphique) montrant comment les modèles s’enchaînent.

---

## Ajouter des descriptions aux modèles et aux sources
Pour tirer pleinement parti de DBT Docs, il est crucial d’enrichir vos fichiers `.yml` avec des **descriptions** détaillées. DBT rendra ces informations visibles dans l’interface.

### 1. Exemples pour les modèles
Imaginons un modèle `stg_pokemon` (staging des Pokémon) et un autre `stg_trainers` (staging des Dresseurs).

**Fichier `stg_pokemon.yml` :**
```yaml
version: 2

models:
  - name: stg_pokemon
    description: "Données Pokémon nettoyées et standardisées, une ligne par Pokémon."
    columns:
      - name: pokemon_id
        description: "Identifiant unique du Pokémon (renommé depuis la source brute)."
      - name: pokemon_name
        description: "Nom officiel du Pokémon, normalisé (majuscule)."
      - name: type_principal
        description: "Type élémentaire principal (Eau, Feu, Plante, etc.)."
```
> **Note** : Les descriptions apparaîtront dans la section “Columns” de DBT Docs, ce qui facilite la consultation.

### 2. Exemples pour les sources
Les **sources** se définissent dans un fichier `sources.yml`. On peut, par exemple, pointer sur un schéma `my_pokemon_db` hébergeant les tables brutes `raw_pokemon` et `raw_trainers`.  

**Fichier `pokemon_sources.yml` :**
```yaml
version: 2

sources:
  - name: poke_world
    schema: my_pokemon_db
    description: "Base de données brute des Pokémon et des dresseurs."
    tables:
      - name: raw_pokemon
        description: "Table brute listant chaque Pokémon capturé ou référencé."
      - name: raw_trainers
        description: "Table brute listant les dresseurs, leur région et leurs badges."
```
Lorsqu’on visualise la source `poke_world` dans DBT Docs, on y verra les deux tables brutes, leurs noms et les descriptions fournies.

### 3. Référencer un fichier Markdown
Pour des descriptions plus longues, vous pouvez créer un fichier Markdown séparé et l’appeler depuis votre `.yml` :

**Fichier `doc_store_id.md` :**
```markdown
{% docs store_id_description %}
Cette colonne identifie le PokéStop ou la boutique Pokémon (Store ID).
Le Store ID fait référence à la table `stores`.
Il est utilisé pour relier les achats, les objets disponibles, etc.
{% enddocs %}
```
Puis dans votre YAML :
```yaml
- name: store_id
  description: "{{ doc('store_id_description') }}"
  tests:
    - not_null
```
Lors de la génération de la documentation, DBT inclura le contenu du Markdown à la place de `{{ doc('store_id_description') }}`.

---

## Conclusion
Avec **DBT Docs**, vous obtenez une **vue interactive** de l’ensemble de votre pipeline de données : modèles, sources, tests, descriptions, etc. Ce système de documentation :
- **Facilite** la collaboration entre équipes (chacun peut comprendre le rôle des champs et tables).  
- **Améliore** la maintenabilité (les modifications sont centralisées dans les fichiers `.yml` et `.md`).  
- **Rend** la structure de votre projet plus **transparente** et plus lisible.  

En intégrant des **descriptions** soignées dans tous vos modèles et en maintenant à jour vos fichiers sources, vous assurez la **pérennité** et la **clarté** de vos pipelines de données, qu’il s’agisse du monde Pokémon ou de tout autre univers !
