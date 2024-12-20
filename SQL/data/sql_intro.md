# SQL - Introduction et Bases

## Introduction

SQL (Structured Query Language) est le langage standard pour interagir avec les bases de données relationnelles. Créé dans les années 1970, SQL permet de gérer, manipuler et interroger des bases de données de manière efficace. Il est utilisé dans une grande variété de domaines, notamment pour l'analyse de données, la gestion des utilisateurs, et le développement d'applications.

### Logiciels couramment utilisés pour travailler avec SQL

Pour exécuter des requêtes SQL, plusieurs logiciels et outils sont disponibles :

- **MySQL Workbench** : Interface graphique pour travailler avec des bases MySQL. [Site officiel](https://dev.mysql.com/downloads/workbench/)
- **pgAdmin** : Outil de gestion pour PostgreSQL. [Site officiel](https://www.pgadmin.org/)
- **SQLite Studio** : Outil léger pour gérer des bases SQLite. [Site officiel](https://sqlitestudio.pl/)
- **DBeaver** : Client universel pour bases de données multiples. [Site officiel](https://dbeaver.io/)

Ces outils permettent de créer, manipuler et interroger des bases de données avec une interface conviviale.

### Syntaxe de base de SQL

La syntaxe SQL est simple mais suit des règles strictes :

- Chaque commande SQL doit se terminer par un point-virgule `;`.
- Les mots-clés SQL ne sont pas sensibles à la casse, mais il est d'usage de les écrire en majuscules pour améliorer la lisibilité.
- Les noms de tables et de colonnes sont sensibles à la casse dans certains systèmes de gestion de bases de données (SGBD).

Exemple :

```sql
SELECT nom, type1 FROM pokemons WHERE type1 = 'Feu';
```

## Création de la base de données Pokémon

Avant d'exécuter des requêtes SQL, il est nécessaire de configurer une base de données. Dans cet exemple, une base fictive appelée `pokemon_db` sera utilisée, avec une table principale `pokemons` contenant des informations clés sur les Pokémon.

### Création de la table `pokemons`

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
- `id` : Identifiant unique pour chaque Pokémon.
- `nom` : Nom du Pokémon.
- `type1` et `type2` : Types principaux et secondaires du Pokémon.
- `points_de_vie`, `attaque`, `defense`, `vitesse` : Statistiques principales.
- `generation` : Génération à laquelle le Pokémon appartient.

### Insertion des données

```sql
INSERT INTO pokemons (id, nom, type1, type2, points_de_vie, attaque, defense, vitesse, generation)
VALUES
(1, 'Bulbizarre', 'Plante', 'Poison', 45, 49, 49, 45, 1),
(2, 'Salamèche', 'Feu', NULL, 39, 52, 43, 65, 1),
(3, 'Carapuce', 'Eau', NULL, 44, 48, 65, 43, 1),
(4, 'Pikachu', 'Électrik', NULL, 35, 55, 40, 90, 1);
```

**Explications :**
- `NULL` est utilisé lorsqu’un Pokémon n’a pas de type secondaire.
- Chaque ligne insère un Pokémon avec ses caractéristiques.

### Visualisation des données
Pour afficher toutes les données de la table :

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
Pour afficher uniquement les noms et types des Pokémon :

```sql
SELECT nom, type1, type2 FROM pokemons;
```

**Pourquoi ?** Cela permet de réduire la quantité de données affichées pour se concentrer sur des informations pertinentes.

**Résultat attendu :**
| nom       | type1  | type2  |
|-----------|--------|--------|
| Bulbizarre | Plante | Poison |
| Salamèche | Feu    | NULL   |
| Carapuce  | Eau    | NULL   |
| Pikachu   | Électrik | NULL  |

### Filtrer les données avec `WHERE`
Afficher uniquement les Pokémon de type "Feu" :

```sql
SELECT * FROM pokemons
WHERE type1 = 'Feu';
```

**Pourquoi ?** La clause `WHERE` est utilisée pour appliquer des filtres spécifiques sur les données.

**Résultat attendu :**
| id | nom       | type1 | type2 | points_de_vie | attaque | defense | vitesse | generation |
|----|-----------|-------|-------|---------------|---------|---------|---------|------------|
| 2  | Salamèche | Feu   | NULL  | 39            | 52      | 43      | 65      | 1          |

### Trier les résultats avec `ORDER BY`
Classer les Pokémon par vitesse décroissante :

```sql
SELECT nom, vitesse FROM pokemons
ORDER BY vitesse DESC;
```

**Pourquoi ?** L’ordre des résultats peut être important pour analyser les données.

**Résultat attendu :**
| nom       | vitesse |
|-----------|---------|
| Pikachu   | 90      |
| Salamèche | 65      |
| Carapuce  | 43      |
| Bulbizarre | 45     |

### Agréger les données avec `GROUP BY`
Compter le nombre de Pokémon par type principal :

```sql
SELECT type1, COUNT(*) AS nombre_pokemons
FROM pokemons
GROUP BY type1;
```

**Pourquoi ?** `GROUP BY` est utile pour regrouper les données et appliquer des fonctions d’agrégation comme `COUNT`, `SUM`, ou `AVG`.

**Résultat attendu :**
| type1    | nombre_pokemons |
|----------|-----------------|
| Plante   | 1               |
| Feu      | 1               |
| Eau      | 1               |
| Électrik | 1               |

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
