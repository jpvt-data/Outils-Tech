[⬅ Page Précédente](../README.md)

# DAX - Les fonctions basiques

## Introduction

Les fonctions DAX (Data Analysis Expressions) permettent de réaliser des calculs dans Power BI. Ce langage est fondamental pour créer des mesures et des colonnes calculées à partir des données importées. DAX propose plusieurs types de fonctions qui permettent de manipuler des données numériques, catégoriser, filtrer ou encore effectuer des transformations de format. Cette fiche détaille les fonctions basiques les plus utilisées : les fonctions scalaires, itératives, logiques, d'information, de conversion, ainsi que d'agrégation. Ces fonctions servent à effectuer des calculs, des vérifications, ou à transformer les données pour les visualiser de manière optimale dans des rapports.

### Objectif

Comprendre et utiliser les fonctions basiques de DAX pour effectuer des calculs simples sur les données. Ces fonctions peuvent être utilisées lors de l'analyse des KPIs, dans des dashboards interactifs ou pour simplifier la préparation des données avant la visualisation.

---

## Fonctions scalaires

Les fonctions scalaires retournent un seul résultat, c'est-à-dire une valeur unique, pour chaque appel de fonction. Elles sont souvent utilisées pour des calculs simples comme des sommes, des moyennes ou des comptages.

### 1. Fonctions d'agrégation

Les fonctions d'agrégation permettent de résumer les données sur une colonne spécifique. Voici quelques fonctions courantes :

#### **DISTINCTCOUNT**
La fonction `DISTINCTCOUNT` retourne le nombre de valeurs distinctes dans une colonne donnée.

```DAX
nombre_pokemon = DISTINCTCOUNT(Pokemon[Nom])
```

Dans cet exemple, cette mesure permet de compter le nombre de Pokémon uniques dans la table `Pokemon`.

#### **COUNTROWS**
La fonction `COUNTROWS` compte le nombre de lignes dans une table ou une table filtrée.

```DAX
nombre_pokemon = COUNTROWS(Pokemon)
```

Ici, elle retourne le nombre total de Pokémon présents dans la table `Pokemon`.

#### **SUM**
La fonction `SUM` additionne les valeurs d'une colonne.

```DAX
total_points_attaque = SUM(Pokemon[PointsAttaque])
```

Cette mesure additionne les points d'attaque de tous les Pokémon dans la table `Pokemon`.

#### Autres fonctions d'agrégation :

- `MIN` : Retourne la valeur minimale d'une colonne.
- `MAX` : Retourne la valeur maximale d'une colonne.
- `AVERAGE` : Retourne la moyenne des valeurs d'une colonne.

Ces fonctions sont utilisées de manière similaire à `SUM`, mais selon le besoin de l'analyse.

---

### 2. Fonctions d'arrondi

Les fonctions d'arrondi permettent de modifier le format des nombres pour les afficher de manière plus lisible.

#### **ROUND**
La fonction `ROUND` permet d’arrondir un nombre à un nombre spécifique de décimales.

```DAX
moyenne_points_attaque = ROUND(AVERAGE(Pokemon[PointsAttaque]), 2)
```

Ici, cette mesure calcule la moyenne des points d'attaque des Pokémon, puis arrondit cette moyenne à deux décimales.

#### Autres fonctions d'arrondi :

- `FLOOR` : Arrondit un nombre à l'entier inférieur le plus proche.
- `CEILING` : Arrondit un nombre à l'entier supérieur le plus proche.
- `ROUNDUP` : Arrondit toujours au chiffre supérieur.

Ces fonctions peuvent être utilisées lorsque des chiffres arrondis sont préférables pour l'affichage ou l'analyse.

---

## Fonctions itératives

Les fonctions itératives sont utilisées pour appliquer une fonction d'agrégation sur une expression, ligne par ligne, au lieu de le faire sur une colonne entière. Elles parcourent chaque ligne d’une table et appliquent un calcul défini.

### **SUMX**
La fonction `SUMX` permet de réaliser un calcul sur chaque ligne d’une table, puis de faire la somme des résultats.

```DAX
total_impact_attaque = SUMX(
    Pokemon, 
    Pokemon[PointsAttaque] * Pokemon[Niveau]
)
```

Dans cet exemple, la fonction calcule le total de l'impact d'attaque de chaque Pokémon, en multipliant ses points d'attaque par son niveau. Ensuite, elle additionne ces résultats pour obtenir une valeur totale.

### Autres fonctions itératives :

- `MINX` : Retourne la valeur minimale après application d'une expression.
- `MAXX` : Retourne la valeur maximale après application d'une expression.
- `AVERAGEX` : Retourne la moyenne après application d’une expression.

Ces fonctions permettent de réaliser des calculs plus complexes qui prennent en compte plusieurs variables par ligne.

---

## Fonctions d'information

Les fonctions d'information permettent de vérifier l’état des données, comme vérifier si une cellule est vide ou si une valeur est un nombre.

### 1. **ISBLANK**
La fonction `ISBLANK` vérifie si une valeur est vide.

```DAX
check_impact_attaque = ISBLANK([total_impact_attaque])
```

Cette mesure retourne `TRUE` si la mesure `total_impact_attaque` est vide, et `FALSE` sinon. Cela permet d'éviter des erreurs dans les visualisations en cas de données manquantes.

### 2. **ISNUMBER**
La fonction `ISNUMBER` vérifie si une valeur est un nombre.

```DAX
check_nombre_pokemon = ISNUMBER([nombre_pokemon])
```

Ici, la fonction vérifie si la mesure `nombre_pokemon` retourne un nombre. Si ce n’est pas le cas, une erreur sera renvoyée.

### Autres fonctions d'information :

- `ISEMPTY` : Vérifie si une table ou une colonne est vide.
- `ISERROR` : Vérifie si une valeur est une erreur.
- `ISTEXT` : Vérifie si une valeur est du texte.

---

## Fonctions de conversion

Les fonctions de conversion permettent de changer le type de données d'une valeur, ou d'afficher une valeur dans un format spécifique.

### **FORMAT**
La fonction `FORMAT` permet de convertir une valeur en texte dans un format spécifique.

```DAX
prix_pokemon_format = FORMAT([prix_pokemon], "Currency")
```

Ici, la fonction `FORMAT` convertit la mesure `prix_pokemon` en format monétaire.

### Autres fonctions de conversion :

- `CONVERT` : Convertit une valeur d'un type à un autre.
- `TRUNC` : Tronque un nombre à un nombre spécifié de décimales.
- `TEXT` : Formate une valeur comme du texte selon un format spécifié.

---

## Fonctions logiques

Les fonctions logiques permettent de créer des conditions dans les mesures, en fonction desquelles une valeur peut être retournée ou une autre action effectuée.

### 1. **IF**
La fonction `IF` permet de créer une condition : si une condition est vraie, une valeur est retournée, sinon une autre valeur est renvoyée.

```DAX
classe_pokemon = IF(
    [total_points_attaque] > 100, 
    "Fort", 
    "Faible"
)
```

Dans cet exemple, si les points d'attaque d'un Pokémon sont supérieurs à 100, la mesure retourne "Fort", sinon elle retourne "Faible".

### 2. **SWITCH**
La fonction `SWITCH` permet d'évaluer plusieurs conditions et de retourner une valeur selon la condition qui est remplie.

```DAX
classe_pokemon_2 = SWITCH(
    TRUE(), 
    [total_points_attaque] > 100, "Très fort", 
    [total_points_attaque] >= 50 && [total_points_attaque] <= 100, "Moyen", 
    "Faible"
)
```

Ici, la fonction évalue plusieurs conditions et renvoie une classe en fonction des points d'attaque d'un Pokémon. Si les points sont supérieurs à 100, la classe sera "Très fort", si entre 50 et 100, "Moyen", et "Faible" sinon.

---

## Conclusion

Les fonctions DAX permettent de réaliser une large gamme de calculs sur les données dans Power BI, en particulier pour l'analyse des KPIs. Cette fiche présente les fonctions basiques nécessaires pour effectuer des calculs simples mais puissants, allant de l'agrégation à la manipulation de formats et conditions. Ces connaissances sont essentielles pour structurer les analyses de données et rendre les rapports interactifs et clairs.

[⬅ Page Précédente](../README.md)