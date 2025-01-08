[⬅ Page Précédente](../README.md)

# Récupérer des informations dans une base de données

## Introduction

Les bases de données sont des outils puissants pour organiser et gérer des informations; il est essentiel de savoir les interroger efficacement.  

## Objectif

Apprendre à récupérer, filtrer, et trier des données dans une base SQL en utilisant les commandes de base telles que `SELECT`, `WHERE`, `ORDER BY`, et `LIMIT`. Ces compétences sont essentielles pour interagir avec des bases de données dans des projets de data analytics, que ce soit pour des applications de gestion, d'analyse, ou de reporting.

---

## Structure de la commande SELECT

### 1. Sélectionner des données avec SELECT

La commande `SELECT` permet de récupérer des informations spécifiques depuis une table d'une base de données. Voici la syntaxe de base :

```sql
SELECT <champs> FROM <table>;
```

- `<champs>` : correspond aux colonnes que l'on souhaite récupérer. Si l'on veut toutes les colonnes, on utilise `*`.
- `<table>` : désigne la table dans laquelle se trouvent les données.

Exemple avec une table Pokémon :

```sql
SELECT * FROM pokemon;
```

Cette commande permet de récupérer toutes les colonnes de la table `pokemon`.

Si tu veux uniquement le nom et le type des Pokémon :

```sql
SELECT name, type FROM pokemon;
```

### 2. Utilisation des alias (AS)

Les alias servent à renommer temporairement une colonne pour simplifier la lecture des résultats. Par exemple :

```sql
SELECT name AS pokemon_name, type AS pokemon_type FROM pokemon;
```

Cela permet de renommer les colonnes `name` et `type` en `pokemon_name` et `pokemon_type`, respectivement, dans les résultats.

---

## Filtrage des données avec la clause WHERE

La clause `WHERE` permet de filtrer les résultats en fonction de critères spécifiques. Elle peut inclure des conditions simples ou complexes.

### Exemple simple : filtrer par type de Pokémon

Imaginons que tu veuilles récupérer tous les Pokémon de type "Feu" :

```sql
SELECT name, type FROM pokemon WHERE type = 'Feu';
```

### Conditions avancées : combinaison avec AND, OR

On peut combiner plusieurs conditions avec les opérateurs `AND` et `OR`. Par exemple, pour récupérer les Pokémon de type "Feu" et "Eau" :

```sql
SELECT name, type FROM pokemon WHERE type = 'Feu' OR type = 'Eau';
```

### Filtrer avec des opérateurs de comparaison

On peut aussi utiliser des opérateurs de comparaison comme `>`, `<`, `>=`, `<=`, `=`, `!=`, etc. Exemple pour récupérer les Pokémon de niveau supérieur à 50 :

```sql
SELECT name, level FROM pokemon WHERE level > 50;
```

### Filtrer avec LIKE

Si l'on souhaite filtrer par une correspondance partielle, on utilise le mot-clé `LIKE`. Par exemple, pour récupérer les Pokémon dont le nom commence par "Salam" :

```sql
SELECT name FROM pokemon WHERE name LIKE 'Salam%';
```

### Exemple avancé : filtrer sur plusieurs conditions

```sql
SELECT name, type, level FROM pokemon WHERE type = 'Feu' AND level >= 50;
```

Cela retournera tous les Pokémon de type "Feu" dont le niveau est supérieur ou égal à 50.

---

## Trier les résultats avec ORDER BY

La clause `ORDER BY` permet de trier les résultats selon les colonnes spécifiées, soit en ordre croissant (`ASC`), soit décroissant (`DESC`).

### Exemple de tri simple : trier par niveau de Pokémon

```sql
SELECT name, level FROM pokemon ORDER BY level DESC;
```

Cette commande trie les Pokémon par niveau, du plus élevé au plus bas.

### Tri sur plusieurs colonnes

Il est aussi possible de trier sur plusieurs colonnes. Par exemple, pour trier par type puis par niveau de manière décroissante :

```sql
SELECT name, type, level FROM pokemon ORDER BY type ASC, level DESC;
```

Cela trie les Pokémon par type en ordre croissant, et pour les Pokémon ayant le même type, par niveau décroissant.

---

## Limiter le nombre de résultats avec LIMIT

La clause `LIMIT` permet de limiter le nombre de résultats retournés par une requête.

### Exemple simple : limiter les résultats

```sql
SELECT name FROM pokemon LIMIT 5;
```

Cela retournera uniquement les 5 premiers Pokémon.

### Limiter avec OFFSET : Pagination

La clause `OFFSET` permet de définir à partir de quel résultat commencer la sélection. Par exemple, pour récupérer 5 Pokémon après les 10 premiers :

```sql
SELECT name FROM pokemon LIMIT 5 OFFSET 10;
```

Cela récupérera les Pokémon 11 à 15.

---

## Cas d'utilisation et exemple pratique

Imaginons que tu as une base de données de Pokémon et que tu souhaites récupérer certains Pokémon en fonction de critères comme le type, le niveau, ou encore la génération. Voici un exemple complet de requêtes SQL que tu pourrais utiliser pour obtenir des informations utiles dans un projet d'analyse de données.

### Récupérer les Pokémon de type "Eau" et de niveau supérieur à 30, triés par niveau croissant :

```sql
SELECT name, type, level 
FROM pokemon 
WHERE type = 'Eau' AND level > 30
ORDER BY level ASC;
```

### Obtenir les 3 premiers Pokémon de type "Feu" avec un niveau supérieur ou égal à 50 :

```sql
SELECT name, type, level 
FROM pokemon 
WHERE type = 'Feu' AND level >= 50
ORDER BY level DESC 
LIMIT 3;
```

---

## Conclusion

Les commandes SQL `SELECT`, `WHERE`, `ORDER BY`, et `LIMIT` sont essentielles pour interroger une base de données et récupérer les informations pertinentes. Elles permettent de filtrer, trier, et limiter les résultats pour répondre à des besoins spécifiques.

---

### Ressources supplémentaires

- [Cheat Sheet SQL](http://www.sql-tutorial.net/SQL-Cheat-Sheet.pdf)
- [Cours complet sur SELECT](https://sql.sh/cours/select/)
- [Tutoriel sur la clause WHERE](https://sql.sh/cours/where)
- [Tutoriel sur ORDER BY](https://sql.sh/cours/order-by)
- [Tutoriel sur LIMIT et OFFSET](https://sql.sh/cours/limit)

[⬅ Page Précédente](../README.md)