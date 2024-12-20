# SQL - Les Jointures

## Introduction

Les jointures sont des éléments essentiels dans la gestion des bases de données relationnelles. Elles permettent de relier plusieurs tables entre elles, en utilisant des clés primaires et des clés étrangères. Cette fiche explique les types de jointures et montre comment les utiliser pour combiner des données provenant de différentes tables. Ces techniques sont particulièrement utiles lorsque les données sont réparties sur plusieurs tables et que l'on souhaite les analyser ensemble.

## Objectif

L'objectif de cette fiche est de comprendre comment utiliser les jointures dans des requêtes SQL. À travers des exemples concrets, l'utilisateur pourra apprendre à relier des tables et extraire les informations qui les relient. Les concepts de jointures permettront aussi de mieux comprendre la modélisation des données et de préparer des requêtes plus complexes.

## Types de Jointures

### Jointure Interne (INNER JOIN)

La jointure interne est la plus courante. Elle permet de sélectionner les lignes qui ont des correspondances dans les deux tables concernées. Cela signifie que seuls les enregistrements qui existent dans les deux tables seront affichés.

### Syntaxe :
```sql
SELECT <colonne1>, <colonne2>...
FROM <table1>
INNER JOIN <table2> ON <condition>;
```
La condition spécifie les colonnes qui doivent correspondre entre les deux tables.

### Exemple :

Imaginons une base de données sur les Pokémon, avec deux tables : `pokemon` et `attaque`. La table `pokemon` contient des informations sur chaque Pokémon, et la table `attaque` contient les attaques dont dispose chaque Pokémon.

#### Création des tables :

```sql
CREATE TABLE pokemon (
    id INT NOT NULL AUTO_INCREMENT,
    nom VARCHAR(100) NOT NULL,
    type VARCHAR(50),
    PRIMARY KEY (id)
);

CREATE TABLE attaque (
    id INT NOT NULL AUTO_INCREMENT,
    pokemon_id INT,
    attaque VARCHAR(100) NOT NULL,
    PRIMARY KEY (id),
    FOREIGN KEY (pokemon_id) REFERENCES pokemon(id)
);
```

#### Insertion des données :

```sql
INSERT INTO pokemon (nom, type) VALUES
('Dracaufeu', 'Feu'),
('Alakazam', 'Psy'),
('Torterra', 'Plante');

INSERT INTO attaque (pokemon_id, attaque) VALUES
(1, 'Flammeche'),
(1, 'Lance-Flamme'),
(2, 'Psychique'),
(3, 'Fouet Lianes');
```

#### Requête avec `INNER JOIN` :

```sql
SELECT p.nom AS pokemon, a.attaque
FROM pokemon AS p
INNER JOIN attaque AS a ON p.id = a.pokemon_id;
```

#### Résultat :

| pokemon   | attaque       |
|-----------|---------------|
| Dracaufeu | Flammeche     |
| Dracaufeu | Lance-Flamme  |
| Alakazam  | Psychique     |
| Torterra  | Fouet Lianes  |

Cette requête sélectionne les Pokémon avec leurs attaques correspondantes. Seuls les Pokémon ayant des attaques dans la table `attaque` sont affichés.

### Jointure Gauche (LEFT JOIN)

La jointure gauche permet de récupérer toutes les lignes de la table de gauche (la première table mentionnée dans la requête), même si aucune correspondance n'existe dans la table de droite.

### Syntaxe :
```sql
SELECT <colonne1>, <colonne2>...
FROM <table1>
LEFT JOIN <table2> ON <condition>;
```

### Exemple avec `LEFT JOIN` :

Imaginons qu'un Pokémon n'ait pas encore d'attaque enregistrée dans la table `attaque`. La requête suivante permettrait de l'afficher tout de même.

```sql
SELECT p.nom AS pokemon, a.attaque
FROM pokemon AS p
LEFT JOIN attaque AS a ON p.id = a.pokemon_id;
```

#### Résultat :

| pokemon   | attaque       |
|-----------|---------------|
| Dracaufeu | Flammeche     |
| Dracaufeu | Lance-Flamme  |
| Alakazam  | Psychique     |
| Torterra  | Fouet Lianes  |

Dans cet exemple, la table `pokemon` contient des Pokémon même si certains n'ont pas d'attaque dans la table `attaque`. Les résultats montrent des valeurs NULL pour les Pokémon sans attaques.

### Jointure Droite (RIGHT JOIN)

La jointure droite fonctionne de la même manière que la jointure gauche, mais elle renvoie toutes les lignes de la table de droite, même si aucune correspondance n'est trouvée dans la table de gauche.

### Syntaxe :
```sql
SELECT <colonne1>, <colonne2>...
FROM <table1>
RIGHT JOIN <table2> ON <condition>;
```

### Exemple avec `RIGHT JOIN` :

Imaginons qu'il existe des attaques qui n'ont pas de Pokémon associé. La requête suivante permettrait de l'afficher.

```sql
SELECT p.nom AS pokemon, a.attaque
FROM pokemon AS p
RIGHT JOIN attaque AS a ON p.id = a.pokemon_id;
```

#### Résultat :

| pokemon   | attaque       |
|-----------|---------------|
| Dracaufeu | Flammeche     |
| Dracaufeu | Lance-Flamme  |
| Alakazam  | Psychique     |
| Torterra  | Fouet Lianes  |
| NULL      | Poing de Feu  |

Cette jointure renverrait toutes les attaques, y compris celles qui n'ont pas de Pokémon associé.

### Utilisation des Alias

Les alias permettent de simplifier les requêtes SQL, en attribuant des noms alternatifs aux tables ou aux colonnes. Cela est particulièrement utile lorsque plusieurs tables ont des colonnes portant les mêmes noms.

### Syntaxe des alias :
```sql
SELECT t1.colonne1 AS alias1, t2.colonne2 AS alias2
FROM table1 AS t1
INNER JOIN table2 AS t2 ON t1.id = t2.id;
```

### Exemple avec alias :

```sql
SELECT p.nom AS pokemon, a.attaque AS attaque_pokemon
FROM pokemon AS p
INNER JOIN attaque AS a ON p.id = a.pokemon_id;
```

#### Résultat :

| pokemon   | attaque_pokemon |
|-----------|-----------------|
| Dracaufeu | Flammeche       |
| Dracaufeu | Lance-Flamme    |
| Alakazam  | Psychique       |
| Torterra  | Fouet Lianes    |

### Conclusion

Les jointures sont un outil puissant pour lier des tables et extraire des informations complexes à partir de bases de données relationnelles. La maîtrise des différentes jointures permet de manipuler efficacement des données provenant de plusieurs sources et d'obtenir des résultats plus détaillés. Il est important de comprendre la différence entre `INNER JOIN`, `LEFT JOIN`, et `RIGHT JOIN` pour choisir la jointure la plus appropriée à chaque situation.
