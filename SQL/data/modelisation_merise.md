## Bases de la modélisation des données (méthode Merise)

### Introduction

Avant de créer une base de données, il est essentiel de bien réfléchir à la structure des données à gérer. Cela passe par une étape primordiale : la modélisation des données. La modélisation permet de définir la façon dont les informations seront organisées et reliées au sein de la base de données. Cette étape est cruciale pour assurer la cohérence et la pérennité des données.

Le processus de modélisation s'appuie sur des méthodologies, et l’une des plus anciennes et des plus connues est la méthode Merise, utilisée depuis les années 70. Elle aide à organiser les données de manière logique, en identifiant les entités, leurs attributs, et leurs relations. Dans cette fiche, nous aborderons les principes fondamentaux de cette méthode, en nous concentrant sur trois étapes clés : **le Modèle Conceptuel de Données (MCD)**, **le Modèle Logique de Données (MLD)** et **le Modèle Physique de Données (MPD)**.

### 1. Modèle Conceptuel de Données (MCD) : le schéma Entité-Relation

Le **Modèle Conceptuel de Données** (MCD) est une représentation abstraite des données. Il se base sur un schéma appelé **entité-relation**, qui sert à décrire les entités, leurs attributs, et les relations entre elles.

#### Les entités

Les entités sont des objets ou concepts qui possèdent des attributs et qui ont une existence propre au sein du système. Par exemple, dans une base de données Pokémon, des entités pourraient être **Pokémon**, **Entraîneur**, ou **Bataille**. Chaque entité a des attributs qui décrivent ses caractéristiques. Par exemple :

- **Pokémon** : nom, type, génération, niveau.
- **Entraîneur** : nom, âge, région.
- **Bataille** : date, lieu, résultat.

Une entité doit également avoir un **identifiant unique**, souvent appelé **clé primaire**, permettant de l’identifier de manière unique au sein du système. Dans notre exemple, chaque Pokémon aura un identifiant unique, comme un numéro **Pokédex**.

##### Exemple d’entité **Pokémon** :

| Attribut         | Description             |
|------------------|-------------------------|
| id_pokemon       | Identifiant unique      |
| nom              | Nom du Pokémon          |
| type             | Type du Pokémon (e.g., feu, eau, plante) |
| génération       | Génération du Pokémon (e.g., 1ère génération) |
| niveau           | Niveau d’évolution      |

#### Les relations

Les relations décrivent les interactions entre les entités. Par exemple, un **Entraîneur** peut posséder plusieurs **Pokémons**, et un **Pokémon** peut appartenir à plusieurs **Entraîneurs** (si le Pokémon est échangé).

Les relations peuvent être représentées par des **verbes d’action** qui lient les entités.

Par exemple :

- **Entraîneur** - possède - **Pokémon** (un entraîneur possède plusieurs Pokémon)
- **Pokémon** - participe - **Bataille** (un Pokémon peut participer à plusieurs batailles)

#### Les cardinalités

Les cardinalités indiquent combien d'occurrences d'une entité peuvent être liées à une occurrence d’une autre entité.

Par exemple :

- Un **Entraîneur** peut posséder plusieurs **Pokémons** (cardinalité 1 à N).
- Un **Pokémon** peut participer à plusieurs **Batailles** (cardinalité N à N).

Ces cardinalités sont cruciales pour déterminer comment les entités interagiront entre elles.

### 2. Modèle Logique de Données (MLD) : tables et champs

Le **Modèle Logique de Données** (MLD) consiste à traduire le MCD en tables et en champs spécifiques à une base de données relationnelle. À ce stade, chaque entité devient une table, chaque attribut devient un champ dans la table, et les relations sont traduites en clés étrangères.

#### Transformation des entités en tables

Dans un MLD, chaque entité du MCD devient une table. Par exemple, l'entité **Pokémon** devient une table **Pokémon** dans la base de données. Les attributs de l’entité deviennent les colonnes de la table.

#### Transformation des relations en clés étrangères

Les relations entre les entités sont représentées par des **clés étrangères** dans les tables. Par exemple, si un **Entraîneur** possède plusieurs **Pokémons**, la table **Pokémon** inclura un champ **id_entraîneur** comme clé étrangère, pointant vers l'entité **Entraîneur**.

##### Exemple MLD pour la relation entre **Entraîneur** et **Pokémon** :

| Table **Entraîneur** |            | Table **Pokémon** |
|----------------------|------------|-------------------|
| id_entraîneur (PK)   | Nom        | id_pokemon (PK)   |
| nom                  | Âge        | nom               |
| âge                  | Région     | type              |
|                      |            | génération        |
|                      |            | niveau            |
|                      |            | id_entraîneur (FK)|

### 3. Modèle Physique de Données (MPD) : la base de données réelle

Le **Modèle Physique de Données** (MPD) est la dernière étape où le modèle logique est ajusté pour tenir compte des contraintes matérielles et des performances. Cela inclut la gestion des index, des partitions, et des optimisations spécifiques à un système de gestion de base de données (SGBD).

### Les types de relations dans une base de données

#### One-to-One (1-1)

Une relation **One-to-One** signifie qu’une occurrence d’une entité est liée à une seule occurrence d’une autre entité. Par exemple, un **Pokémon** peut avoir une **carte spéciale**, et chaque **carte spéciale** est liée à un unique **Pokémon**.

#### One-to-Many (1-N)

Une relation **One-to-Many** est courante dans les bases de données relationnelles. Par exemple, un **Entraîneur** peut posséder plusieurs **Pokémons**, mais chaque **Pokémon** ne peut appartenir qu’à un seul **Entraîneur**.

#### Many-to-Many (N-N)

Une relation **Many-to-Many** indique que plusieurs occurrences d’une entité peuvent être liées à plusieurs occurrences d’une autre entité. Par exemple, un **Pokémon** peut participer à plusieurs **Batailles**, et chaque **Bataille** peut impliquer plusieurs **Pokémons**. Ce type de relation nécessite une **table de jointure** pour associer les entités.

### Conclusion

La modélisation de données avec la méthode Merise permet de structurer et d’organiser les informations de manière cohérente avant leur implémentation dans une base de données. Elle repose sur trois étapes : le MCD (schéma Entité-Relation), le MLD (transformation en tables et champs), et le MPD (optimisation physique pour le SGBD). Une bonne compréhension de ces étapes permet de créer des bases de données efficaces et adaptées aux besoins des utilisateurs.

### Liens utiles

- [IBM Data Modeling](https://www.ibm.com/topics/data-modeling)
