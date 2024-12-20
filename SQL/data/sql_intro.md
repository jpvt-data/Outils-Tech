# SQL - Introduction et Bases de données relationnelles

## Introduction

SQL (Structured Query Language) est un langage standardisé utilisé pour interagir avec les bases de données relationnelles. Ce langage permet de créer, modifier, gérer et interroger les données contenues dans une base. SQL est utilisé dans des applications variées, comme l'analyse de données, la gestion des utilisateurs et le développement d'applications.

## Qu'est-ce qu'une base de données relationnelle (SGBDR) ?

Une **base de données relationnelle** est un système de gestion de base de données (SGBD) qui stocke les données sous forme de tables reliées entre elles par des **relations** (liens logiques). Ces bases de données sont organisées en tables, chacune représentant une entité (comme un utilisateur, un produit, etc.) et chaque table est composée de lignes (enregistrements) et de colonnes (attributs).

Les **SGBDR** (Systèmes de Gestion de Bases de Données Relationnelles) utilisent des relations entre les tables et des règles basées sur des modèles relationnels. Ils permettent de gérer efficacement les données grâce à des fonctionnalités telles que les requêtes SQL, l'intégrité référentielle, les transactions, et les contraintes d'intégrité.

Les SGBDR les plus utilisés sont :
- **MySQL**
- **PostgreSQL**
- **SQLite**
- **Microsoft SQL Server**
- **Oracle Database**

Ces systèmes permettent d’organiser, manipuler et interroger des bases de données à l'aide de commandes SQL.

## Logiciels couramment utilisés pour travailler avec SQL

Pour exécuter des requêtes SQL, plusieurs outils sont utilisés pour interagir avec les bases de données relationnelles :

- **MySQL Workbench** : Interface graphique pour travailler avec des bases MySQL. [Site officiel](https://dev.mysql.com/downloads/workbench/)
- **pgAdmin** : Outil de gestion pour PostgreSQL. [Site officiel](https://www.pgadmin.org/)
- **SQLite Studio** : Outil léger pour gérer des bases SQLite. [Site officiel](https://sqlitestudio.pl/)
- **DBeaver** : Client universel pour plusieurs bases de données. [Site officiel](https://dbeaver.io/)

Ces outils permettent de créer, manipuler et interroger des bases de données avec une interface conviviale.

Voici la section manquante pour compléter ta fiche sur les **syntaxes de base en SQL**, incluant l'explication des éléments essentiels à connaître pour bien utiliser SQL.

---

## Syntaxes de base en SQL

En SQL, chaque commande doit suivre une certaine syntaxe pour être correctement interprétée et exécutée par un SGBD (Système de Gestion de Bases de Données). Voici les règles et éléments de syntaxe les plus importants :

### **Le point-virgule (;)** :
- Le point-virgule est utilisé pour marquer la fin d'une commande SQL. 
- Bien qu'il ne soit pas toujours obligatoire, il est fortement recommandé d'utiliser le point-virgule pour signaler la fin d'une requête, surtout lorsqu'il y a plusieurs requêtes à exécuter dans un même script ou dans des outils comme MySQL Workbench.

    Exemple :
    ```sql
    SELECT * FROM pokemons;
    ```

### **Majuscules et minuscules** :
- Les commandes SQL (comme `SELECT`, `INSERT`, `CREATE`, etc.) sont **insensibles à la casse**, mais il est d'usage de les écrire en **majuscule** pour une meilleure lisibilité. 
- Par contre, les **noms de tables et de colonnes** sont sensibles à la casse dans certains systèmes de gestion de bases de données (comme PostgreSQL), alors il est préférable de les écrire de manière cohérente.

    Exemple :
    ```sql
    SELECT nom FROM pokemons;
    ```

### **Les espaces** :
- Les espaces sont importants pour séparer les mots-clés, les colonnes, les valeurs, etc. Cependant, SQL ignore les espaces supplémentaires. Il est donc recommandé de bien espacer les différentes parties d'une requête pour une meilleure lisibilité.

    Exemple :
    ```sql
    SELECT nom, type1 FROM pokemons WHERE type1 = 'Feu';
    ```

### **Les commentaires** :
- Vous pouvez ajouter des commentaires dans votre code SQL pour expliquer certaines parties de la requête ou pour désactiver temporairement du code.
- Un commentaire sur une seule ligne commence par `--`. 
- Un commentaire sur plusieurs lignes est délimité par `/*` pour ouvrir et `*/` pour fermer.

    Exemple :
    ```sql
    -- Ceci est un commentaire sur une seule ligne
    SELECT nom FROM pokemons;

    /*
    Ceci est un commentaire
    sur plusieurs lignes
    */
    ```

### **Les chaînes de caractères** :
- Les valeurs de type texte doivent être entourées de guillemets simples `'`. 
- Il est important de ne pas utiliser de guillemets doubles pour les chaînes de caractères.

    Exemple :
    ```sql
    SELECT * FROM pokemons WHERE nom = 'Bulbizarre';
    ```

### **Les parenthèses** :
- Les parenthèses sont utilisées pour délimiter les valeurs dans des instructions comme `INSERT INTO` ou pour structurer les expressions dans les clauses `WHERE`, `ORDER BY`, etc.
- Elles sont également nécessaires lors de la définition des colonnes d'une table dans la commande `CREATE TABLE`.

    Exemple :
    ```sql
    CREATE TABLE pokemons (
        id INT PRIMARY KEY,
        nom VARCHAR(50)
    );
    ```

### **Les alias** :
- Les alias permettent de donner des noms temporaires aux tables ou aux colonnes pour faciliter la lecture des requêtes. On utilise `AS` pour définir un alias.

    Exemple :
    ```sql
    SELECT nom AS pokemon, type1 AS premier_type FROM pokemons;
    ```

### **Les types de données** :
- Les colonnes des tables doivent être associées à un type de données spécifique, tel que `INT` pour un entier, `VARCHAR` pour une chaîne de caractères de longueur variable, ou `DATE` pour une date.
- Il est important de respecter ces types pour assurer une bonne gestion des données.

    Exemple :
    ```sql
    CREATE TABLE pokemons (
        id INT PRIMARY KEY,
        nom VARCHAR(50),
        type1 VARCHAR(20)
    );
    ```

---

### Tableau récapitulatif des éléments de syntaxe

| Élément de syntaxe | Description | Exemple |
|--------------------|-------------|---------|
| Point-virgule `;`   | Fin d'une commande SQL | `SELECT * FROM pokemons;` |
| Majuscules/minuscules | Utilisation de majuscules pour les commandes SQL | `SELECT` |
| Espaces | Séparation des éléments de la requête | `SELECT nom FROM pokemons;` |
| Commentaires | Ajouter des explications dans le code | `-- Ceci est un commentaire` |
| Guillemets simples `'` | Délimitation des chaînes de caractères | `SELECT * FROM pokemons WHERE nom = 'Pikachu';` |
| Parenthèses `()` | Délimitation des valeurs ou expressions | `CREATE TABLE pokemons (id INT);` |
| Alias `AS` | Renommer des tables ou colonnes temporairement | `SELECT nom AS pokemon FROM pokemons;` |
| Types de données | Définir les types de colonnes dans les tables | `id INT, nom VARCHAR(50)` |

---

## Création d'une base de données Pokémon

Avant d’exécuter des requêtes SQL, nous devons configurer une base de données. Voici un exemple de création d’une base fictive appelée `pokemon_db` avec une table principale `pokemons`.

### Création de la table `pokemons`

Voici la commande SQL pour créer la table des Pokémon dans une base de données relationnelle :

```sql
CREATE TABLE pokemons (
    id INT PRIMARY KEY,
    nom VARCHAR(50),
    type1 VARCHAR(20),
    type2 VARCHAR(20),
    points_de_vie INT,
    attaque INT,
    defense INT,
    vitesse INT,
    generation INT
);
```

**Explications :**
- `id` : Identifiant unique pour chaque Pokémon, de type entier. Il s'agit d'une **clé primaire**.
- `nom` : Nom du Pokémon, chaîne de caractères.
- `type1` et `type2` : Types principaux et secondaires du Pokémon (par exemple, Plante, Feu, etc.).
- `points_de_vie`, `attaque`, `defense`, `vitesse` : Statistiques du Pokémon.
- `generation` : La génération à laquelle le Pokémon appartient.

### Clés primaires et secondaires

- **Clé primaire** : Une **clé primaire** est une colonne ou un ensemble de colonnes qui identifie de manière unique chaque enregistrement dans une table. Dans notre exemple, la colonne `id` est une clé primaire. Elle garantit qu'aucun deux Pokémon ne peuvent avoir le même identifiant dans cette table. Une clé primaire ne peut pas avoir de valeurs NULL et doit être unique.
  
- **Clé étrangère (ou secondaire)** : Une **clé étrangère** est une colonne dans une table qui crée une relation avec une clé primaire d’une autre table. Elle permet de maintenir l’intégrité référentielle, c’est-à-dire d’assurer que les relations entre les tables sont cohérentes. Par exemple, si nous avions une table `types` qui listait tous les types de Pokémon, une colonne `type1_id` dans la table `pokemons` pourrait être une clé étrangère qui fait référence à la clé primaire `id` de la table `types`.

#### Exemple d'ajout d'une clé étrangère :

```sql
CREATE TABLE types (
    id INT PRIMARY KEY,
    nom VARCHAR(20)
);

CREATE TABLE pokemons (
    id INT PRIMARY KEY,
    nom VARCHAR(50),
    type1_id INT,
    type2_id INT,
    points_de_vie INT,
    attaque INT,
    defense INT,
    vitesse INT,
    generation INT,
    FOREIGN KEY (type1_id) REFERENCES types(id),
    FOREIGN KEY (type2_id) REFERENCES types(id)
);
```

Ici, `type1_id` et `type2_id` dans la table `pokemons` sont des clés étrangères qui référencent la table `types`.

### Insertion des données

Nous insérons des Pokémon dans la table à l'aide de la commande `INSERT INTO` :

```sql
INSERT INTO pokemons (id, nom, type1, type2, points_de_vie, attaque, defense, vitesse, generation)
VALUES
(1, 'Bulbizarre', 'Plante', 'Poison', 45, 49, 49, 45, 1),
(2, 'Salamèche', 'Feu', NULL, 39, 52, 43, 65, 1),
(3, 'Carapuce', 'Eau', NULL, 44, 48, 65, 43, 1),
(4, 'Pikachu', 'Électrik', NULL, 35, 55, 40, 90, 1);
```

### Visualisation des données

Pour afficher toutes les données de la table, nous utilisons la requête suivante :

```sql
SELECT * FROM pokemons;
```

**Résultat attendu :**
| id | nom       | type1  | type2  | points_de_vie | attaque | defense | vitesse | generation |
|----|-----------|--------|--------|---------------|---------|---------|---------|------------|
| 1  | Bulbizarre | Plante | Poison | 45            | 49      | 49      | 45      | 1          |
| 2  | Salamèche | Feu    | NULL   | 39            | 52      | 43      | 65      | 1          |
| 3  | Carapuce  | Eau    | NULL   | 44            | 48      | 65      | 43      | 1          |
| 4  | Pikachu   | Électrik | NULL  | 35            | 55      | 40      | 90      | 1          |

## Requêtes fondamentales en SQL

### Sélectionner des colonnes spécifiques

```sql
SELECT nom, type1, type2 FROM pokemons;
```

**Pourquoi ?** Cela permet de réduire la quantité de données affichées, en ne sélectionnant que les colonnes pertinentes.

### Filtrer les données avec `WHERE`

```sql
SELECT * FROM pokemons
WHERE type1 = 'Feu';
```

**Pourquoi ?** La clause `WHERE` permet de filtrer les résultats selon des critères spécifiques.

### Trier les résultats avec `ORDER BY`

```sql
SELECT nom, vitesse FROM pokemons
ORDER BY vitesse DESC;
```

**Pourquoi ?** Le tri des résultats permet d'analyser les données dans un ordre particulier, ici par la vitesse des Pokémon.

### Agréger les données avec `GROUP BY`

```sql
SELECT type1, COUNT(*) AS nombre_pokemons
FROM pokemons
GROUP BY type1;
```

**Pourquoi ?** `GROUP BY` est utilisé pour regrouper les données et appliquer des fonctions d’agrégation comme `COUNT`, `SUM`, ou `AVG`.

## Tableau synthèse des syntaxes de base SQL

| Commande SQL     | Description                                   | Exemple                                    |
|------------------|-----------------------------------------------|-------------------------------------------|
| `CREATE TABLE`   | Créer une nouvelle table                     | `CREATE TABLE pokemons (...);`           |
| `INSERT INTO`    | Insérer des données dans une table           | `INSERT INTO pokemons VALUES (...);`     |
| `SELECT`         | Sélectionner des colonnes spécifiques         | `SELECT nom, type1 FROM pokemons;`       |
| `WHERE`          | Filtrer les données                          | `SELECT * FROM pokemons WHERE type1='Feu';` |
| `ORDER BY`       | Trier les résultats                          | `SELECT * FROM pokemons ORDER BY vitesse DESC;` |
| `GROUP BY`       | Regrouper les données pour agrégation        | `SELECT type1, COUNT(*) FROM pokemons GROUP BY type1;` |

## Liens utiles

- [Documentation officielle de MySQL](https://dev.mysql.com/doc/)
- [Introduction à SQL - W3Schools](https://www.w3schools.com/sql/)
- [Exercices pratiques SQL](https://www.sql-ex.fr/)
