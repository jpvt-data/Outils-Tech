# DAX - Fonctions Avancées (Partie 1)

## Introduction

Les fonctions avancées en DAX (Data Analysis Expressions) permettent d'exploiter toute la puissance de Power BI pour filtrer, transformer, et modéliser des données de manière précise. Cette fiche explique comment utiliser des fonctions de filtrage et de création de tables virtuelles pour résoudre des problématiques d'analyse de données complexes. Les exemples s'appuient sur des jeux de données fictifs autour de cartes et ventes de Pokémon pour illustrer concrètement les concepts.

## Contexte

Ces fonctions sont utilisées dans les cas suivants :
- Analyser des sous-ensembles de données selon des critères précis.
- Créer des tables calculées ou des tables virtuelles pour les visualisations.
- Manipuler des colonnes et des relations dans des modèles complexes.

## Fonctions de Filtrage

### 1. FILTER

Permet de restreindre les lignes d'une table selon des conditions précises.

**Syntaxe** :
```DAX
FILTER(table, condition1, condition2, ...)
```

**Exemple : Filtrer les cartes Pokémon rares vendues dans un magasin spécifique**
```DAX
Cartes_Rares_Magasin5 = FILTER(Ventes,
                               Ventes[Type] = "Rare" &&
                               Ventes[MagasinID] = 5)
```

Cet exemple crée une table contenant uniquement les cartes rares vendues dans le magasin 5.

**Exemple avancé : Filtrer selon une condition liée à une autre table**
```DAX
Total_Ventes_Rares_200Plus =
CALCULATE(
    SUM(Ventes[Montant]),
    FILTER(
        RELATEDTABLE(Produits),
        Produits[Prix] > 200 && Produits[Rareté] = "Légendaire"
    )
)
```
Cet exemple calcule le total des ventes pour les cartes légendaires dont le prix est supérieur à 200. La fonction `RELATEDTABLE` relie les tables `Ventes` et `Produits`.

---

### 2. VALUES

Retourne une table contenant les valeurs distinctes d'une colonne.

**Syntaxe** :
```DAX
VALUES(table[column])
```

**Exemple : Extraire les types de cartes disponibles**
```DAX
Types_Cartes = VALUES(Produits[Type])
```
Crée une table contenant les différents types de cartes présents dans la table `Produits`.

**Exemple : Utilisation avec CALCULATE pour des filtres dynamiques**
```DAX
Ventes_Pour_Types_Select =
CALCULATE(
    SUM(Ventes[Montant]),
    Produits[Type] IN VALUES(Produits[Type])
)
```
Cette mesure calcule la somme des ventes uniquement pour les types de cartes actuellement sélectionnés dans un filtre.

---

### 3. DISTINCT

Retourne une table contenant des lignes uniques d'une colonne.

**Syntaxe** :
```DAX
DISTINCT(table[column])
```

**Exemple : Identifier les magasins uniques ayant vendu des cartes**
```DAX
Magasins_Uniques = DISTINCT(Ventes[MagasinID])
```
Crée une table contenant les identifiants des magasins ayant effectué des ventes.

**Différence entre VALUES et DISTINCT**

| Fonction   | Prend en compte les filtres ? |
|------------|-------------------------------|
| VALUES     | Oui                           |
| DISTINCT   | Non                           |

---

## Tables Virtuelles avec CALCULATETABLE

### CALCULATETABLE

Crée une table à partir d'une table existante en appliquant des filtres spécifiques.

**Syntaxe** :
```DAX
CALCULATETABLE(
    table_expression,
    filter1,
    filter2, ...
)
```

**Exemple : Créer une table pour les ventes supérieures à 1000 Pokédollars pour des cartes épiques**
```DAX
Ventes_Epiques_1000Plus =
CALCULATETABLE(
    Ventes,
    Ventes[Montant] > 1000 &&
    RELATED(Produits[Type]) = "Épique"
)
```
Cette table contient uniquement les ventes de cartes épiques dont le montant dépasse 1000 Pokédollars.

---

## Fonctions pour Organiser les Données

### SUMMARIZE

Permet de regrouper des données et d'ajouter des colonnes calculées.

**Syntaxe** :
```DAX
SUMMARIZE(
    table,
    column1,
    column2,
    ...,
    ["Nom_Colonne", expression]
)
```

**Exemple : Regrouper les ventes par type de carte et magasin**
```DAX
Ventes_Par_Type_Magasin =
SUMMARIZE(
    Ventes,
    Produits[Type],
    Ventes[MagasinID],
    "Total_Ventes", SUM(Ventes[Montant])
)
```

---

### ADDCOLUMNS

Ajoute des colonnes calculées à une table existante.

**Syntaxe** :
```DAX
ADDCOLUMNS(
    table,
    "Nom_Colonne1", expression1,
    "Nom_Colonne2", expression2,
    ...
)
```

**Exemple : Ajouter une colonne pour la taxe sur les ventes**
```DAX
Ventes_Avec_Taxe =
ADDCOLUMNS(
    Ventes,
    "Taxe", Ventes[Montant] * 0.2
)
```
Ajoute une colonne calculée pour la taxe de 20 % à la table des ventes.

---

## Résumé

Cette fiche introduit des fonctions essentielles pour manipuler et analyser les données dans Power BI. En combinant les filtres, les tables virtuelles, et les transformations, il devient possible de créer des analyses avancées adaptées à des besoins précis. Ces outils permettent d'extraire des informations stratégiques à partir de grands volumes de données.

## Ressources

- [Documentation Microsoft DAX](https://learn.microsoft.com/en-us/dax/)
- [Guide Power BI - Fonctions Avancées](https://docs.microsoft.com/fr-fr/power-bi/)

