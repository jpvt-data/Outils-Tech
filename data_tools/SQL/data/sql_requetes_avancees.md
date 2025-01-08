[⬅ Page Précédente](../README.md)

# SQL - Requêtes Avancées

## Introduction

Les requêtes SQL avancées permettent de réaliser des analyses plus complexes et de travailler efficacement avec des bases de données volumineuses. Ces techniques sont souvent utilisées dans le cadre de la manipulation de données structurées, de l'analyse de grandes quantités de données, ou pour répondre à des besoins spécifiques, comme le calcul de moyennes mobiles ou la segmentation des données. Cette fiche explique plusieurs concepts avancés en SQL, comme les vues, les fonctions de fenêtrage et la création de "buckets", et fournit des exemples pratiques pour illustrer leur utilisation.

## Vue (VIEW)

Une **vue** est une requête SQL enregistrée qui fonctionne comme une table virtuelle. Elle permet de simplifier des requêtes complexes en les transformant en éléments réutilisables. Lorsqu'une vue est créée, elle peut être utilisée dans d'autres requêtes comme une table normale.

**Création d'une vue** :
```sql
CREATE VIEW VuePokemons AS
SELECT Nom, Type, Attaque1, Attaque2 
FROM Pokemons
WHERE Type = 'Eau';
```
Dans cet exemple, la vue `VuePokemons` contient une sélection de Pokémons de type "Eau" avec leurs deux premières attaques. Chaque fois que cette vue est appelée, elle renvoie les données filtrées. 

**Utilisation d'une vue** :
```sql
SELECT * FROM VuePokemons;
```
Cela permet de récupérer directement les données filtrées sans avoir à réécrire la condition à chaque fois.

**Pourquoi utiliser une vue ?**  
Les vues simplifient les requêtes complexes et permettent de centraliser des opérations de filtrage ou d'agrégation, ce qui améliore la lisibilité du code.

---

## Fonction Fenêtre (Window Function)

Les **fonctions de fenêtre** sont des fonctions analytiques qui permettent de faire des calculs sur un ensemble de lignes spécifié (fenêtre) tout en conservant les lignes de données individuelles. Cela permet de réaliser des agrégations sans avoir besoin de regrouper les données.

**Exemple d'utilisation de SUM() OVER()** :
```sql
SELECT Nom, Attaque1, 
       SUM(Puissance) OVER() AS TotalPuissance
FROM Pokemons;
```
Ici, la somme des puissances d'attaque de tous les Pokémons est calculée, mais chaque ligne conserve sa propre valeur.

**Pourquoi utiliser les fonctions de fenêtre ?**  
Les fonctions de fenêtre sont utiles lorsque vous souhaitez appliquer des calculs sur un sous-ensemble de données sans réduire le nombre de lignes. Elles sont couramment utilisées dans les analyses financières, les classements, ou les calculs de moyennes mobiles.

---

## La Fonction LAG()

La fonction **LAG()** permet d'accéder à la ligne précédente dans un ensemble de données, ce qui est très utile pour comparer des valeurs successives ou calculer des différences.

**Exemple d'utilisation de LAG()** :
```sql
SELECT Date, Nom, 
       LAG(Puissance) OVER(ORDER BY Date) AS PuissancePrecedente
FROM Evolutions;
```
Dans cet exemple, pour chaque Pokémon, la fonction `LAG()` renvoie la puissance d'attaque de la ligne précédente (dans l'ordre chronologique des évolutions).

**Pourquoi utiliser LAG() ?**  
Cela permet de comparer une valeur avec celle de la ligne précédente, ce qui est utile pour calculer des variations ou observer des tendances.

---

## Création de "Buckets"

Les **"buckets"** (ou regroupements) permettent de diviser un ensemble de données en catégories basées sur des critères définis. Cela permet de segmenter des données pour une analyse plus ciblée.

**Exemple de création de "buckets" pour l'âge des Pokémon** :
```sql
SELECT Nom, 
       CASE
           WHEN Niveau < 20 THEN 'Niveau faible'
           WHEN Niveau >= 20 AND Niveau < 50 THEN 'Niveau intermédiaire'
           ELSE 'Niveau élevé'
       END AS GroupeNiveau
FROM Pokemons;
```
Dans cet exemple, les Pokémons sont regroupés en trois catégories en fonction de leur niveau. Les valeurs sont regroupées à l'aide de la fonction `CASE`.

**Pourquoi utiliser des "buckets" ?**  
Les "buckets" sont utiles pour segmenter les données en fonction de critères significatifs, ce qui permet une analyse plus détaillée et spécifique des sous-groupes de données.

---

## MAX() OVER()

La fonction **MAX() OVER()** permet de calculer la valeur maximale d'une colonne dans un ensemble de lignes défini par la fenêtre.

**Exemple d'utilisation de MAX() OVER()** :
```sql
SELECT Nom, Attaque1, 
       MAX(Puissance) OVER() AS PuissanceMaximale
FROM Pokemons;
```
Ici, la puissance maximale de toutes les attaques des Pokémons est calculée pour chaque ligne, mais chaque Pokémon conserve sa propre valeur.

**Pourquoi utiliser MAX() OVER() ?**  
Cela permet de comparer chaque valeur avec la valeur maximale dans l'ensemble des données, ce qui est utile pour les analyses comparatives.

---

## AVG() OVER()

La fonction **AVG() OVER()** permet de calculer la moyenne des valeurs dans un ensemble de lignes défini par la fenêtre.

**Exemple d'utilisation de AVG() OVER()** :
```sql
SELECT Nom, Attaque2, 
       AVG(Puissance) OVER() AS PuissanceMoyenne
FROM Pokemons;
```
Cela calcule la moyenne des puissances d'attaque pour chaque Pokémon tout en conservant chaque ligne individuelle.

**Pourquoi utiliser AVG() OVER() ?**  
Cela permet de calculer des moyennes globales tout en conservant les données individuelles, ce qui est utile pour voir la répartition des valeurs par rapport à la moyenne.

---

## PERCENT_RANK()

La fonction **PERCENT_RANK()** attribue un rang percentuel à chaque ligne dans un ensemble de données, en fonction de l'ordre de tri.

**Exemple d'utilisation de PERCENT_RANK()** :
```sql
SELECT Nom, Puissance, 
       PERCENT_RANK() OVER(ORDER BY Puissance DESC) AS RangPercentile
FROM Pokemons;
```
Dans cet exemple, chaque Pokémon se voit attribuer un rang percentile par rapport à la puissance de ses attaques.

**Pourquoi utiliser PERCENT_RANK() ?**  
Cette fonction est utile pour attribuer des rangs en pourcentage, ce qui permet de comparer les positions relatives des valeurs dans un ensemble de données.

---

## NTILE()

La fonction **NTILE()** permet de diviser les données en plusieurs "buckets" égaux (quantiles).

**Exemple d'utilisation de NTILE() pour diviser en quartiles** :
```sql
SELECT Nom, Puissance, NTILE(4) OVER(ORDER BY Puissance DESC) AS Quartile
FROM Pokemons;
```
Ici, les Pokémons sont répartis en quatre groupes égaux en fonction de la puissance de leurs attaques.

**Pourquoi utiliser NTILE() ?**  
Cela permet de diviser un ensemble de données en groupes égaux, ce qui est utile pour des analyses statistiques comme les quartiles ou les percentiles.

---

## Conclusion

Les requêtes SQL avancées permettent d'analyser et de manipuler des données de manière plus approfondie. Grâce aux fonctions de fenêtrage, aux vues et à la création de "buckets", il est possible d'effectuer des analyses plus complexes tout en maintenant la lisibilité et la réutilisabilité du code SQL. Ces techniques sont essentielles pour les Data Analysts qui travaillent avec des bases de données larges et complexes.

[⬅ Page Précédente](../README.md)