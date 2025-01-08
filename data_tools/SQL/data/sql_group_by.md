[⬅ Page Précédente](../README.md)

# SQL - Utilisation de GROUP BY

## Introduction

L'optimisation des requêtes SQL passe souvent par l'agrégation des données, c'est-à-dire la capacité à regrouper des enregistrements et à effectuer des calculs sur ces groupes. La fonction **GROUP BY** permet de regrouper les lignes de données en fonction d'une ou plusieurs colonnes et de calculer des valeurs agrégées (comme le nombre, la somme, la moyenne) sur ces groupes. Cette fonctionnalité est essentielle lorsque l’on souhaite obtenir des résumés de données ou des statistiques sur des ensembles d'éléments qui partagent des caractéristiques communes.

L'objectif de cette fiche est de comprendre comment utiliser la clause **GROUP BY** et les fonctions d'agrégation en SQL. Ce processus est particulièrement utile lors de l'analyse de données liées à des catégories ou des groupes, comme l’analyse des Pokémon par type, génération ou autres critères spécifiques.

## Quand utiliser GROUP BY ?

Le **GROUP BY** est utilisé pour regrouper les lignes de données ayant une même valeur dans une ou plusieurs colonnes spécifiées. C'est utile dans des cas comme :

- Comptabiliser le nombre de Pokémon par type.
- Calculer la moyenne des points de vie des Pokémon par génération.
- Obtenir le total des attaques utilisées par chaque type de Pokémon.

### Exemple d’utilisation typique

Imaginons une base de données contenant des informations sur des Pokémon, leurs types, attaques, et stats de combat. Supposons que l'on souhaite savoir combien de Pokémon existent pour chaque type (e.g., Feu, Eau, Plante, etc.).

## Requêtes de base avec GROUP BY

### Création d'une base de données de Pokémon

Avant d'exécuter des requêtes **GROUP BY**, il est nécessaire de disposer d'une base de données adéquate. Voici un exemple de structure simple des tables pour un jeu de données Pokémon :

```sql
CREATE DATABASE pokemon_db;

USE pokemon_db;

CREATE TABLE pokemon(
    id INT NOT NULL AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    type VARCHAR(50),
    generation INT,
    PRIMARY KEY (id)
);

CREATE TABLE attack(
    id INT NOT NULL AUTO_INCREMENT,
    pokemon_id INT,
    attack_name VARCHAR(100),
    power INT,
    PRIMARY KEY (id),
    FOREIGN KEY (pokemon_id) REFERENCES pokemon(id)
);

INSERT INTO pokemon (name, type, generation) VALUES
('Charmander', 'Fire', 1),
('Squirtle', 'Water', 1),
('Bulbasaur', 'Grass', 1),
('Pikachu', 'Electric', 1),
('Magikarp', 'Water', 1),
('Golem', 'Rock', 1);

INSERT INTO attack (pokemon_id, attack_name, power) VALUES
(1, 'Flamethrower', 90),
(2, 'Hydro Pump', 110),
(3, 'Vine Whip', 45),
(4, 'Thunderbolt', 90),
(5, 'Splash', 0),
(6, 'Earthquake', 100);
```

### Comptabiliser les Pokémon par type

La première utilisation de **GROUP BY** consiste à regrouper les Pokémon par type et à compter combien de Pokémon existent pour chaque type.

```sql
SELECT type, COUNT(*) AS nb_pokemon
FROM pokemon
GROUP BY type;
```

**Explication :**

- `COUNT(*)` est une fonction d'agrégation qui compte le nombre de lignes dans chaque groupe.
- `GROUP BY type` regroupe les Pokémon en fonction de leur type (e.g., Feu, Eau, etc.).
  
**Résultat attendu :**

| type    | nb_pokemon |
|---------|------------|
| Fire    | 1          |
| Water   | 2          |
| Grass   | 1          |
| Electric| 1          |
| Rock    | 1          |

## Utiliser HAVING avec GROUP BY

Il est possible de filtrer les groupes obtenus à l’aide de la clause **HAVING**. Cela permet d’effectuer des filtrages sur les résultats agrégés, contrairement à **WHERE**, qui filtre les lignes avant l’agrégation.

### Exemple avec HAVING : Pokémon ayant plus de 1 attaque

```sql
SELECT p.name, COUNT(a.id) AS nb_attacks
FROM pokemon p
LEFT JOIN attack a ON p.id = a.pokemon_id
GROUP BY p.id
HAVING nb_attacks > 1;
```

**Explication :**

- `LEFT JOIN` permet de joindre les informations sur les attaques pour chaque Pokémon.
- `COUNT(a.id)` compte le nombre d’attaques associées à chaque Pokémon.
- `HAVING nb_attacks > 1` filtre les Pokémon qui ont plus d’une attaque.

**Résultat attendu :**

| name      | nb_attacks |
|-----------|------------|
| Charmander| 1          |
| Squirtle  | 1          |
| Bulbasaur | 1          |
| Pikachu   | 1          |
| Golem     | 1          |

## Résumé des fonctions d'agrégation courantes

| Fonction        | Description                                                       | Exemple |
|-----------------|-------------------------------------------------------------------|---------|
| `COUNT(*)`      | Compte le nombre d'éléments dans le groupe                        | `COUNT(*)` |
| `SUM(colonne)`  | Somme des valeurs d'une colonne                                   | `SUM(power)` |
| `AVG(colonne)`  | Moyenne des valeurs d'une colonne                                 | `AVG(power)` |
| `MIN(colonne)`  | Valeur minimale d'une colonne                                     | `MIN(power)` |
| `MAX(colonne)`  | Valeur maximale d'une colonne                                     | `MAX(power)` |

## Cas d'utilisation dans le monde Pokémon

Voici quelques exemples supplémentaires pour illustrer l'utilisation de **GROUP BY** dans l'analyse des Pokémon :

1. **Calculer la moyenne des points de vie des Pokémon par génération :**

```sql
SELECT generation, AVG(life_points) AS avg_life_points
FROM pokemon
GROUP BY generation;
```

2. **Obtenir le type de Pokémon ayant la plus grande attaque moyenne :**

```sql
SELECT type, AVG(attack_power) AS avg_attack
FROM pokemon p
JOIN attack a ON p.id = a.pokemon_id
GROUP BY type
ORDER BY avg_attack DESC
LIMIT 1;
```

## Conclusion

La clause **GROUP BY** est un outil puissant pour regrouper et analyser des données dans SQL. Elle est fréquemment utilisée pour obtenir des résumés statistiques ou des agrégations, et est souvent couplée avec des fonctions d'agrégation comme **COUNT**, **SUM**, **AVG**, et d’autres. L’ajout de **HAVING** permet de filtrer les résultats après l’agrégation, offrant une flexibilité supplémentaire pour affiner les requêtes.

Pour aller plus loin, il est recommandé de pratiquer avec des jeux de données complexes, comme celui des Pokémon, pour comprendre la puissance des agrégations SQL dans un contexte réel.

## Ressources complémentaires

- [Fonctions SQL sur sql.sh](https://sql.sh/fonctions)
- [Tutoriel GROUP BY sur sql.sh](https://sql.sh/cours/group-by)
- [Tutoriel HAVING sur sql.sh](https://sql.sh/cours/having)

### Exemple vidéo sur l'utilisation de GROUP BY et HAVING
[Regarder la vidéo](https://www.youtube.com/watch?v=aLs8bvkeAFo)

[⬅ Page Précédente](../README.md)
