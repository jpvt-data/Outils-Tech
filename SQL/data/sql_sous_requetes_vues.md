# Sous-requêtes et Vues en SQL

## Introduction

Dans le cadre de l'utilisation de SQL, il est fréquent de devoir exécuter des requêtes complexes qui nécessitent l'enchaînement de plusieurs instructions. Ces requêtes peuvent devenir longues et difficiles à lire si elles sont directement écrites dans une seule ligne de code. Pour rendre ces requêtes plus lisibles et plus faciles à maintenir, on peut utiliser des **sous-requêtes** et des **vues**. Ces outils permettent de structurer les requêtes et de diviser des instructions complexes en sous-parties logiques, simplifiant ainsi leur compréhension et leur réutilisation.

Ce document détaille les concepts de **sous-requêtes** et de **vues** en SQL, fournit des exemples concrets avec des données sur les Pokémon, et explique chaque étape de leur mise en œuvre. Ce guide s'adresse aux utilisateurs débutants qui souhaitent comprendre ces outils et les utiliser efficacement dans leurs requêtes SQL.

## Sous-requêtes

### Qu'est-ce qu'une sous-requête ?

Une **sous-requête** est une requête SQL imbriquée à l'intérieur d'une autre requête. Elle est délimitée par des parenthèses et est toujours exécutée avant la requête principale. Le résultat de la sous-requête est ensuite utilisé dans la requête principale. Les sous-requêtes peuvent être utilisées dans les clauses `WHERE`, `FROM`, ou même `SELECT`.

### Règles importantes des sous-requêtes

- Une sous-requête doit toujours être entourée de parenthèses.
- Elle peut renvoyer une valeur unique (une seule ligne et une seule colonne) ou plusieurs valeurs (plusieurs lignes et plusieurs colonnes).
- Les sous-requêtes sont souvent utilisées pour filtrer ou regrouper des résultats en fonction des valeurs retournées par la sous-requête.

### Exemple de sous-requête dans la clause `WHERE`

Imaginons une base de données contenant des informations sur les Pokémon, avec une table `pokemons` comportant les champs `id`, `nom`, `type`, et `attaque`. La sous-requête suivante permet de sélectionner les Pokémon ayant une attaque supérieure à la moyenne des attaques des Pokémon de type "Feu".

```sql
SELECT nom, type, attaque
FROM pokemons
WHERE attaque > (
    SELECT AVG(attaque)
    FROM pokemons
    WHERE type = 'Feu'
);
```

**Explication du code :**

- La sous-requête `(SELECT AVG(attaque) FROM pokemons WHERE type = 'Feu')` calcule la moyenne des attaques des Pokémon de type "Feu".
- Cette moyenne est ensuite utilisée dans la requête principale pour filtrer les Pokémon dont l'attaque est supérieure à cette moyenne.

### Utiliser une sous-requête dans la clause `FROM`

Les sous-requêtes peuvent également être utilisées dans la clause `FROM` pour traiter des ensembles de données avant de les utiliser dans une requête principale.

```sql
SELECT p.nom, p.type, t.attack_avg
FROM pokemons p
JOIN (
    SELECT type, AVG(attaque) AS attack_avg
    FROM pokemons
    GROUP BY type
) t ON p.type = t.type;
```

**Explication du code :**

- La sous-requête dans la clause `FROM` calcule la moyenne des attaques pour chaque type de Pokémon.
- Ensuite, la requête principale joint ces résultats avec la table `pokemons` pour afficher le nom, le type et l'attaque moyenne des Pokémon.

### Ressources pour approfondir les sous-requêtes

- [GeeksforGeeks - SQL Subquery](https://www.geeksforgeeks.org/sql-subquery)
- [LearnSQL - Types de sous-requêtes](https://learnsql.com/blog/sql-subquery-types)
- [SQLTutorial - Exemples de sous-requêtes](https://www.sqltutorial.org/sql-subquery)

## Vues

### Qu'est-ce qu'une vue ?

Une **vue** est une table virtuelle créée à partir d'une requête SQL. Contrairement aux sous-requêtes qui sont exécutées à chaque appel, une vue stocke la requête et peut être réutilisée comme une table normale. Les vues permettent de simplifier les requêtes complexes en offrant une abstraction de la logique métier.

### Création d'une vue

Pour créer une vue, on utilise la commande `CREATE VIEW` suivie du nom de la vue, puis de la requête qui génère la vue. Une fois créée, la vue peut être utilisée comme une table dans d'autres requêtes SQL.

### Exemple de création de vue

Imaginons une table `pokemons` et une table `types` qui contient les types des Pokémon. La vue suivante calcule le nombre de Pokémon par type.

```sql
CREATE VIEW count_pokemon_per_type AS (
    SELECT type, COUNT(id) AS num_pokemons
    FROM pokemons
    GROUP BY type
);
```

**Explication du code :**

- La vue `count_pokemon_per_type` est créée en calculant le nombre de Pokémon pour chaque type.
- Cette vue permet de simplifier des requêtes ultérieures qui auraient besoin de cette information, sans devoir recalculer le nombre de Pokémon à chaque fois.

### Utilisation d'une vue

Une fois la vue créée, il est possible de l'utiliser dans des requêtes comme une table normale.

```sql
SELECT * FROM count_pokemon_per_type;
```

Cette requête va afficher tous les types de Pokémon avec le nombre de Pokémon correspondants.

### Modifier une vue

Pour modifier une vue, on doit d'abord la supprimer avec la commande `DROP VIEW` puis la recréer avec les nouvelles instructions.

```sql
DROP VIEW IF EXISTS count_pokemon_per_type;
CREATE VIEW count_pokemon_per_type AS (
    SELECT type, COUNT(id) AS num_pokemons, AVG(attaque) AS avg_attack
    FROM pokemons
    GROUP BY type
);
```

### Supprimer une vue

Pour supprimer une vue, on utilise la commande `DROP VIEW`.

```sql
DROP VIEW count_pokemon_per_type;
```

### Ressources pour approfondir les vues

- [SQLTutorial - Vues SQL](https://www.sqltutorial.org/sql-views/)
- [W3Schools - Créer et manipuler des vues](https://www.w3schools.com/sql/sql_view.asp)

## Conclusion

Les sous-requêtes et les vues sont des outils puissants pour organiser et simplifier des requêtes complexes en SQL. Les sous-requêtes permettent d'exécuter des requêtes imbriquées pour filtrer ou transformer les résultats, tandis que les vues offrent une abstraction de logique métier, facilitant ainsi la réutilisation et la maintenance des requêtes. Utiliser ces techniques dans des bases de données comme celle des Pokémon permet d'effectuer des analyses détaillées tout en maintenant une structure claire et compréhensible des requêtes.
