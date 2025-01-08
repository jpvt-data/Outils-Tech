[⬅ Page Précédente](../README.md)

# SQL - Manipulation des données

## Introduction

Manipuler les données dans une base de données est une compétence essentielle pour travailler avec des informations structurées.

Cette fiche explique comment ajouter, modifier et supprimer des données dans une base SQL. Ces opérations sont indispensables lors de la gestion d'une base de données, que ce soit pour l'extension d'une base existante ou pour mettre à jour les informations. 

## 1. Ajouter des données (INSERT INTO)

L'insertion de nouvelles données dans une table d'une base SQL se fait avec la commande `INSERT INTO`. Cette commande permet d'ajouter une ou plusieurs lignes à une table en spécifiant les valeurs à insérer dans les colonnes correspondantes.

### Syntaxe de la commande

```sql
INSERT INTO <table> (col1, col2, col3, ...)
VALUES (valeur1, valeur2, valeur3, ...);
```

### Exemple

Imaginons une base de données contenant une table `pokemons` avec les colonnes suivantes : `id` (auto-incrémenté), `nom`, `type`, `attaque`, et `niveau`.

Pour ajouter un Pokémon dans la base, une requête pourrait ressembler à ceci :

```sql
INSERT INTO pokemons (nom, type, attaque, niveau)
VALUES ('Dracaufeu', 'Feu/Vol', 250, 36);
```

Ici, on insère un Pokémon nommé "Dracaufeu" avec un type "Feu/Vol", une attaque de 250 et un niveau de 36. La valeur de `id` est générée automatiquement par la base de données, car elle est définie comme une clé primaire auto-incrémentée.

Il est aussi possible d'ajouter plusieurs Pokémon en une seule requête :

```sql
INSERT INTO pokemons (nom, type, attaque, niveau)
VALUES 
  ('Florizarre', 'Plante/Poison', 150, 32),
  ('Pikachu', 'Électrique', 100, 25),
  ('Golem', 'Sol/Roche', 200, 45);
```

### Explication

- **Pourquoi insérer ces données ?** Chaque ligne représente un Pokémon avec ses caractéristiques, ce qui permettra ensuite de manipuler ces informations (par exemple, les afficher, les modifier ou les analyser).
- **Que se passe-t-il si on oublie des valeurs ?** Si certaines colonnes ont des valeurs par défaut définies, elles seront automatiquement attribuées si elles ne sont pas spécifiées.

## 2. Modifier des données (UPDATE)

La commande `UPDATE` permet de modifier des enregistrements existants dans une table. Il est essentiel de toujours utiliser la clause `WHERE` pour éviter de modifier toutes les lignes de la table.

### Syntaxe de la commande

```sql
UPDATE <table>
SET colonne1 = valeur1, colonne2 = valeur2, ...
WHERE <condition>;
```

### Exemple pratique

Imaginons que l'attaque du Pokémon "Dracaufeu" soit trop faible et qu'on veuille l'augmenter. Voici comment procéder :

```sql
UPDATE pokemons
SET attaque = 300
WHERE nom = 'Dracaufeu';
```

Dans cet exemple, on met à jour l'attaque du Pokémon "Dracaufeu" en lui attribuant une valeur de 300.

### Explication

- **Pourquoi utiliser `WHERE` ?** La clause `WHERE` est indispensable pour cibler uniquement les lignes que l'on souhaite modifier. Sans `WHERE`, toutes les lignes de la table seraient affectées.
- **Modification de plusieurs colonnes ?** Il est possible de mettre à jour plusieurs colonnes à la fois en les séparant par des virgules.

## 3. Supprimer des données (DELETE)

La commande `DELETE` permet de supprimer une ou plusieurs lignes d'une table. Comme pour la commande `UPDATE`, il est crucial d'utiliser la clause `WHERE` pour éviter la suppression de toutes les données.

### Syntaxe de la commande

```sql
DELETE FROM <table>
WHERE <condition>;
```

### Exemple pratique

Supposons qu'un Pokémon nommé "Pikachu" ait été ajouté par erreur et doit être supprimé de la base :

```sql
DELETE FROM pokemons
WHERE nom = 'Pikachu';
```

Dans cet exemple, on supprime uniquement le Pokémon "Pikachu" de la table.

### Explication

- **Attention à la suppression sans `WHERE` !** Si tu oublies la clause `WHERE`, toutes les lignes de la table seront supprimées, ce qui est irréversible sans une sauvegarde.
- **Supprimer plusieurs lignes ?** Il est également possible de supprimer plusieurs lignes avec une condition plus générale. Par exemple, pour supprimer tous les Pokémon de niveau inférieur à 20 :

```sql
DELETE FROM pokemons
WHERE niveau < 20;
```

## 4. Vider une table (TRUNCATE)

Si l'on souhaite supprimer toutes les lignes d'une table sans supprimer sa structure, la commande `TRUNCATE` peut être utilisée. Elle est plus rapide que `DELETE` et réinitialise l'auto-incrémentation des clés primaires.

### Syntaxe de la commande

```sql
TRUNCATE TABLE <table>;
```

### Exemple pratique

```sql
TRUNCATE TABLE pokemons;
```

Cela videra complètement la table `pokemons`, en supprimant toutes les données mais en laissant la structure de la table intacte.

### Explication

- **Différence avec `DELETE` ?** `TRUNCATE` est plus rapide car elle ne génère pas de logs pour chaque ligne supprimée, contrairement à `DELETE`. Cependant, elle ne permet pas d’utiliser la clause `WHERE` pour supprimer sélectivement des données.

## Tableau récapitulatif des commandes SQL

| Commande    | Fonction                            | Syntaxe générale                                         | Exemple avec Pokémon                                |
|-------------|-------------------------------------|----------------------------------------------------------|-----------------------------------------------------|
| `INSERT`    | Ajouter de nouvelles données        | `INSERT INTO table (col1, col2, ...) VALUES (val1, val2, ...);` | `INSERT INTO pokemons (nom, type, attaque) VALUES ('Mewtwo', 'Psychique', 250);` |
| `UPDATE`    | Modifier des données existantes    | `UPDATE table SET col1 = val1 WHERE condition;`          | `UPDATE pokemons SET attaque = 300 WHERE nom = 'Dracaufeu';` |
| `DELETE`    | Supprimer des données               | `DELETE FROM table WHERE condition;`                     | `DELETE FROM pokemons WHERE nom = 'Pikachu';`      |
| `TRUNCATE`  | Vider une table sans supprimer sa structure | `TRUNCATE TABLE table;`                                  | `TRUNCATE TABLE pokemons;`                         |

## Conclusion

La manipulation des données dans SQL est une compétence de base pour tout travail avec des bases de données. Les commandes `INSERT`, `UPDATE`, `DELETE` et `TRUNCATE` sont fondamentales pour gérer efficacement les données. L'exemple des Pokémon permet de mieux comprendre comment ces commandes peuvent être utilisées dans un contexte concret et réaliste. Pour aller plus loin, il est essentiel de bien comprendre l'impact de chaque opération, notamment l'importance de la clause `WHERE` pour cibler les bonnes lignes.

Pour plus d'informations, consulter les ressources suivantes :
- [Documentation SQL sur W3Schools](https://www.w3schools.com/sql/)
- [SQL pour les bases de données Pokémon](https://www.pokemon.com)

[⬅ Page Précédente](../README.md)
