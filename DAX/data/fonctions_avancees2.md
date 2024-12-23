# DAX – Fonctions avancées (Partie 2)

## Introduction

Cette fiche explore les fonctions avancées en DAX, indispensables pour gérer efficacement les relations entre tables et optimiser les analyses dans Power BI. Ces concepts permettent de manipuler les données avec précision, de créer des relations personnalisées, et d'effectuer des jointures complexes pour enrichir les rapports.

Les thèmes abordés incluent :

- La gestion des relations (à l’aide des fonctions RELATED, RELATEDTABLE, USERELATIONSHIP et CROSSFILTER).
- Les opérations de jointures (CROSSJOIN, UNION, EXCEPT, INTERSECT).
- L’amélioration de la représentation graphique des données.

## Gestion des relations entre tables

### RELATED

**Définition** :
La fonction `RELATED` permet de récupérer une valeur unique à partir d’une table liée. Elle est utilisée pour enrichir une table en ajoutant des colonnes calculées contenant des informations de tables connexes.

**Syntaxe** :
```DAX
RELATED(<colonneàlien>)
```

**Exemple** :
Ajouter les types des Pokémons à la table des ventes :

```DAX
VentesAvecTypes =
ADDCOLUMNS(
    Ventes,
    "TypePokemon", RELATED(Pokemons[TypePrincipal])
)
```

Cette expression crée une nouvelle table, `VentesAvecTypes`, contenant une colonne supplémentaire `TypePokemon` qui correspond au type principal du Pokémon associé à chaque vente.

---

### RELATEDTABLE

**Définition** :
`RELATEDTABLE` retourne une table complète liée dans le contexte évalué. Idéale pour créer des agrégations ou obtenir des listes de valeurs associées.

**Syntaxe** :
```DAX
RELATEDTABLE(<tableàlien>)
```

**Exemple** :
Ajout de colonnes enrichies pour afficher les attaques disponibles et les générations des Pokémons vendus :

```DAX
VentesEnrichies =
ADDCOLUMNS(
    Ventes,
    "Attaques", CONCATENATEX(RELATEDTABLE(Attaques), Attaques[NomAttaque], ", "),
    "Génération", MAXX(RELATEDTABLE(Pokemons), Pokemons[Generation])
)
```

Résultats des colonnes :

- `Attaques` : Liste des attaques disponibles pour chaque Pokémon vendu.
- `Génération` : Génération la plus récente associée à chaque vente.

| VenteID | Attaques               | Génération |
|---------|------------------------|--------------|
| 1       | Charge, Ball'Ombre    | 3            |
| 2       | Hydrocanon, Surf      | 2            |

---

### USERELATIONSHIP

**Définition** :
Permet d’utiliser temporairement une relation inactive entre deux colonnes. Pratique pour basculer entre plusieurs relations possibles dans le modèle.

**Syntaxe** :
```DAX
USERELATIONSHIP(table1[colonne1], table2[colonne2])
```

**Exemple** :
Calculer les ventes par date de capture des Pokémons, au lieu de la date de commande :

```DAX
VentesParDateCapture =
CALCULATE(
    SUMX(Ventes, Ventes[Quantité] * Ventes[Prix]),
    USERELATIONSHIP(Ventes[DateCapture], Dates[Date])
)
```

---

### CROSSFILTER

**Définition** :
Modifie la direction du filtre entre deux tables dans une relation existante.

**Syntaxe** :
```DAX
CROSSFILTER(table1[colonne1], table2[colonne2], CrossFilterType)
```

**Exemple** :
Changer la propagation du filtre entre Pokémons et leurs attaques :

```DAX
CALCULATE(
    COUNTROWS(Pokemons),
    CROSSFILTER(Pokemons[PokemonID], Attaques[PokemonID], Both)
)
```

| CrossFilterType | Effet                  |
|-----------------|------------------------|
| None            | Aucun filtre croisé  |
| Both            | Filtre bidirectionnel |
| Single          | Filtre unidirectionnel|

---

## Jointures de tables en DAX

### CROSSJOIN

**Définition** :
Retourne le produit cartésien de deux tables, combinant toutes les lignes possibles.

**Syntaxe** :
```DAX
CROSSJOIN(table1, table2)
```

**Exemple** :
Lister toutes les combinaisons entre Pokémons et leurs types secondaires disponibles :

```DAX
Combinaisons = CROSSJOIN(Pokemons, TypesSecondaires)
```

---

### UNION

**Définition** :
Combine deux tables en une seule en empilant leurs lignes.

**Syntaxe** :
```DAX
UNION(table1, table2)
```

**Exemple** :
Fusionner deux listes d’événements de capture :

```DAX
EvenementsFusionnés = UNION(Evenements2019, Evenements2020)
```

---

### EXCEPT

**Définition** :
Retourne les lignes présentes dans la première table mais pas dans la seconde.

**Syntaxe** :
```DAX
EXCEPT(table1, table2)
```

**Exemple** :
Afficher les Pokémons qui étaient présents en 2019 mais pas en 2020 :

```DAX
NonRevenus = EXCEPT(Pokemons2019, Pokemons2020)
```

---

### INTERSECT

**Définition** :
Retourne les lignes communes entre deux tables.

**Syntaxe** :
```DAX
INTERSECT(table1, table2)
```

**Exemple** :
Lister les Pokémons disponibles à la fois en 2019 et 2020 :

```DAX
PokemonsCommuns = INTERSECT(Pokemons2019, Pokemons2020)
```

---

## Représentation graphique des données avec DAX

L’utilisation des fonctions DAX avancées améliore la présentation visuelle des rapports en évitant la surcharge d’informations et en mettant en avant les indicateurs pertinents. Créer des KPI personnalisés, optimiser les relations entre tables et ajouter des étiquettes enrichies sur les graphiques garantit une meilleure compréhension des données.

## Ressources
- [Documentation officielle Microsoft DAX](https://learn.microsoft.com/fr-fr/power-bi/)
- [Forum Power BI communautaire](https://community.powerbi.com/)

