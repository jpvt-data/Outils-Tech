[⬅ Page Précédente](../README.md)

# DAX - La fonction `CALCULATE`

## Introduction

La fonction `CALCULATE` en DAX (Data Analysis Expressions) est un outil puissant pour modifier le contexte de calcul d'une mesure ou d'une expression. En manipulant ce contexte, il devient possible de personnaliser les calculs afin d’obtenir des résultats plus spécifiques et pertinents pour des analyses plus fines, comme les comparaisons temporelles, les filtrages géographiques ou catégoriels, etc.

### Objectif de cette fiche

Cette fiche vise à expliquer comment utiliser la fonction `CALCULATE` pour :

- Modifier le contexte de calcul avec des filtres spécifiques.
- Appliquer des fonctions temporelles pour l'analyse de données.
- Calculer des mesures conditionnelles en utilisant des variables intermédiaires.

Elle sera utile lorsque des calculs doivent être effectués sur un sous-ensemble spécifique de données, comme les ventes d'un produit dans une région donnée ou l'analyse des performances sur une période spécifique.

---

## Structure de la fonction `CALCULATE`

La fonction `CALCULATE` se compose de deux parties principales :

1. **Expression à évaluer** : C’est le calcul de base qui sera modifié par les filtres spécifiés.
2. **Filtres à appliquer** : Ce sont les conditions qui modifient ou restreignent le contexte de calcul.

### Syntaxe de base

```DAX
CALCULATE (
    expression,    // Expression à évaluer (par exemple, somme, moyenne, etc.)
    filter1,       // Filtre à appliquer
    filter2,       // Autre filtre
    ...
)
```

---

## Exemples d'utilisation de la fonction `CALCULATE`

### 1. Calcul du total des ventes pour un Pokémon spécifique

Prenons l'exemple des Pokémon et supposons que nous souhaitons calculer le total des dégâts infligés par un Pokémon spécifique (par exemple, **Dracaufeu**) sur l'ensemble de ses combats.

```DAX
Total_Ventes_Dracaufeu = 
CALCULATE (
    SUMX (
        Combats,  // Table contenant les informations des combats
        Combats[Degats]  // Colonne des dégâts
    ),
    Combats[Pokemon] = "Dracaufeu"  // Filtre pour le Pokémon Dracaufeu
)
```

**Explication** : 
- `SUMX(Combats, Combats[Degats])` calcule la somme des dégâts infligés dans la table `Combats`.
- Le filtre `Combats[Pokemon] = "Dracaufeu"` restreint cette somme aux combats où le Pokémon est Dracaufeu.

### 2. Comparaison des ventes de **Dracaufeu** en 2020 par rapport à 2021

Pour analyser l’évolution des ventes du Pokémon **Dracaufeu** d’une année à l’autre, nous appliquons un double filtre : un pour le Pokémon et un autre pour l’année.

```DAX
Ventes_2020_Dracaufeu = 
CALCULATE (
    SUMX (
        Combats,
        Combats[Degats]  // Somme des dégâts infligés
    ),
    Combats[Pokemon] = "Dracaufeu",  // Filtre sur Dracaufeu
    YEAR(Combats[DateCombat]) = 2020  // Filtre sur l'année 2020
)
```

### 3. Calcul des ventes en ignorant certains filtres

La fonction `ALL` permet de supprimer un filtre existant, ce qui peut être utile si vous souhaitez calculer une mesure globale sans tenir compte des filtres appliqués à certaines colonnes.

Exemple : Calcul de la part de marché de **Dracaufeu** parmi tous les Pokémon, sans tenir compte des autres filtres de la table des Pokémon.

```DAX
Part_Vente_Dracaufeu = 
CALCULATE (
    DIVIDE (
        [Total_Ventes_Dracaufeu],  // Mesure des ventes de Dracaufeu
        CALCULATE (
            [Total_Ventes],  // Total des ventes pour tous les Pokémon
            ALL(Pokemon)  // Supprime tous les filtres appliqués à la table Pokémon
        )
    )
)
```

**Explication** :
- `ALL(Pokemon)` retire tous les filtres appliqués à la table `Pokemon`, permettant de calculer le total des ventes de tous les Pokémon sans filtre.
- Le calcul du pourcentage de Dracaufeu par rapport à ce total est effectué via la fonction `DIVIDE`.

---

## Fonctions complémentaires de modification de contexte

### 1. `KEEPFILTERS` : Conserver les filtres existants

La fonction `KEEPFILTERS` permet de conserver les filtres déjà présents tout en ajoutant de nouveaux filtres.

```DAX
Ventes_2022_2023_Dracaufeu = 
CALCULATE (
    [Total_Ventes_Dracaufeu],
    KEEPFILTERS( YEAR(Combats[DateCombat]) IN {2022, 2023} )  // Ajoute un filtre sur les années 2022 et 2023
)
```

**Explication** : 
- Ce calcul permet de maintenir tous les filtres existants dans le modèle tout en ajoutant un filtre pour ne prendre en compte que les années 2022 et 2023.

### 2. `ALLEXCEPT` : Conserver les filtres sur certaines colonnes

L'utilisation de `ALLEXCEPT` permet de supprimer tous les filtres sauf ceux sur des colonnes spécifiées.

```DAX
Ventes_Par_Type_Pokemon = 
CALCULATE (
    [Total_Ventes],
    ALLEXCEPT ( Pokemon, Pokemon[Type] )  // Supprime tous les filtres sauf ceux sur la colonne Type
)
```

---

## Fonctions de **Time Intelligence**

Les fonctions de **Time Intelligence** permettent d'effectuer des calculs liés aux périodes temporelles, comme comparer des valeurs d'un mois ou d'une année précédente.

### Exemple : Comparaison des dégâts infligés au mois précédent

```DAX
Degats_Mois_Precedent = 
CALCULATE (
    SUMX (
        Combats,
        Combats[Degats]  // Somme des dégâts infligés
    ),
    PREVIOUSMONTH(Combats[DateCombat])  // Filtre pour le mois précédent
)
```

**Explication** : 
- `PREVIOUSMONTH(Combats[DateCombat])` filtre les combats pour ne retenir que ceux qui ont eu lieu le mois précédent par rapport à la date actuelle.

---

## Fonction `VAR` et `RETURN`

Pour rendre le code plus lisible, on peut définir des variables intermédiaires avec la fonction `VAR` et retourner le résultat final avec `RETURN`.

### Exemple : Calcul du pourcentage des dégâts infligés par **Dracaufeu**

```DAX
Pourcentage_Degats_Dracaufeu = 
VAR total_degats = SUMX(Combats, Combats[Degats])  // Total des dégâts infligés
VAR total_degats_dracaufeu = CALCULATE(
    SUMX(Combats, Combats[Degats]),
    Combats[Pokemon] = "Dracaufeu"  // Filtre pour Dracaufeu
)
RETURN 
total_degats_dracaufeu / total_degats  // Retourne le pourcentage des dégâts de Dracaufeu
```

---

## Conclusion

La fonction `CALCULATE` est un élément central dans l'utilisation de DAX pour personnaliser le contexte de calcul dans Power BI. Elle permet non seulement de calculer des mesures conditionnelles mais aussi d'appliquer des fonctions temporelles et de manipuler le contexte d'évaluation à l'aide de filtres.

---

## Ressources complémentaires

- [Documentation Microsoft DAX](https://learn.microsoft.com/en-us/dax/)
- [YouTube - Guy in a Cube](https://www.youtube.com/@GuyInACube)

[⬅ Page Précédente](../README.md)