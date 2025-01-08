[⬅ Page Précédente](../README.md)

# Introduction à DAX

DAX (Data Analysis Expressions) est un langage de formules développé par Microsoft pour effectuer des calculs sur des données dans Power BI. Il permet de créer des mesures et des colonnes calculées afin d'analyser et de manipuler les données dans des rapports dynamiques. DAX est un outil essentiel pour transformer des données brutes en informations pertinentes, en tirant parti de la modélisation des données.

## Contexte d'utilisation

Le langage DAX est utilisé principalement dans Power BI pour créer des calculs complexes et des analyses avancées. Il est utilisé en combinaison avec un modèle de données, où les données sont organisées en tables de faits et en tables de dimensions. Dans cette fiche, l'objectif est de comprendre les bases de DAX, son intégration dans le processus d'analyse de données et ses bonnes pratiques d'utilisation.

### Quand utiliser DAX ?
DAX est utilisé dans les cas suivants :
- Pour créer des mesures personnalisées qui ne peuvent pas être directement calculées à partir des données brutes.
- Pour effectuer des calculs qui doivent être ajustés en fonction des filtres appliqués dans les rapports (par exemple, calculer le total des ventes par catégorie de produit).
- Pour simplifier l’analyse de données complexes à travers des agrégations, des filtres dynamiques et des calculs conditionnels.

## Modélisation des données et le Schéma en Étoile

Avant de se lancer dans l'utilisation de DAX, il est crucial de comprendre la **modélisation des données**. La structure recommandée dans Power BI est le **schéma en étoile**. Ce modèle simplifie la gestion des relations entre les données et permet des analyses efficaces.

### Qu'est-ce qu'un schéma en étoile ?

Dans un schéma en étoile, une **table de faits** est entourée de **tables de dimensions**. 

- **Table de faits** : contient des données numériques ou quantifiables (par exemple, des ventes, des coûts).
- **Tables de dimensions** : contiennent des données descriptives permettant de segmenter ou d'analyser les données de la table de faits selon différents critères (par exemple, produit, client, date).

### Exemple de schéma en étoile

Imaginons une entreprise qui souhaite analyser ses ventes. Le modèle en étoile pourrait ressembler à ceci :

```
           +---------+
           | Produit |
           +---------+
                |
                |
+--------+     +--------+     +---------+
| Clients|<--->|  Ventes |<--->|  Date   |
+--------+     +--------+     +---------+
                |
           +---------+
           | Magasin |
           +---------+
```

- La **table de faits** ici est `Ventes`, qui contient les informations de transactions : `quantité`, `prix`, `revenu`, etc.
- Les **tables de dimensions** sont : `Produit`, `Client`, `Date`, et `Magasin`, qui détaillent respectivement les produits vendus, les informations des clients, la date de la transaction, et les magasins où les ventes ont eu lieu.

Les relations sont de type **one-to-many** (un à plusieurs), où chaque enregistrement de la table de dimension peut être associé à plusieurs enregistrements dans la table de faits. Par exemple, un produit peut être associé à plusieurs ventes.

### Bonnes pratiques de modélisation
- **Utiliser un schéma en étoile** : Cela simplifie la gestion des données et permet des analyses plus faciles.
- **Privilégier des relations unidirectionnelles** : Cela signifie que les filtres appliqués sur une table de dimension (par exemple, le produit) affecteront les mesures dans la table de faits.
- **Limiter les données** : Ne charger que les données nécessaires pour éviter la surcharge du modèle.

## Contextes en DAX : Filtre et Ligne

En DAX, il est important de comprendre deux types de **contextes** : le **contexte de filtre** et le **contexte de ligne**. Ces deux éléments influencent directement les résultats des mesures DAX.

### Contexte de Filtre
Le **contexte de filtre** définit les données qui seront prises en compte pour un calcul. Cela correspond aux filtres appliqués dans le rapport Power BI ou lors de la définition d'une mesure. Par exemple, si une mesure DAX calcule le total des ventes, l'ajout d'un filtre sur la catégorie de produit ajustera ce calcul en fonction de la catégorie sélectionnée.

#### Exemple de Contexte de Filtre
Supposons que nous ayons une table de `Ventes` avec les colonnes suivantes : `Produit`, `Quantité`, `Revenu`.

**Code DAX :**  
```dax
Total_Revenu = SUM(Ventes[Revenu])
```

- Si un filtre est appliqué pour afficher uniquement les ventes de `Pokémon Feunard`, la mesure `Total_Revenu` calculera la somme des revenus uniquement pour ce produit, en excluant tous les autres Pokémon.

### Contexte de Ligne
Le **contexte de ligne** se réfère à la manière dont DAX effectue des calculs pour chaque ligne individuellement dans une table. Par exemple, si une table contient des informations sur chaque vente, DAX peut calculer un montant total pour chaque ligne (par exemple, le revenu généré par une vente spécifique).

#### Exemple de Contexte de Ligne
Imaginons une table `Ventes` avec les colonnes `Produit`, `Coût Unitaire`, et `Quantité`.

**Code DAX :**  
```dax
Revenu_Produit = Ventes[Coût Unitaire] * Ventes[Quantité]
```

- DAX calculera le revenu pour chaque ligne en multipliant le coût unitaire par la quantité pour chaque vente spécifique. Le calcul est effectué ligne par ligne, ce qui donne un résultat unique pour chaque vente.

## Mise en Pratique avec un Exemple Concret

### Objectif
L'objectif est de créer une mesure DAX qui calcule le total des revenus pour un produit spécifique dans un rapport Power BI. Cette mesure doit être influencée par les filtres appliqués dans le rapport, comme la sélection d'un produit ou d'une catégorie.

### Étapes :

1. **Chargement des données** :
   Importer la table `Ventes` contenant les informations des ventes, ainsi que la table `Produit` contenant les détails des produits.

2. **Création d'une mesure DAX pour le revenu** :
   Créer une mesure qui calcule le total des revenus pour un produit sélectionné.

**Code DAX :**  
```dax
Total_Revenu_Pokemon = SUM(Ventes[Revenu])
```

3. **Application du filtre produit** :
   Ajouter un filtre dans le rapport pour sélectionner un produit spécifique (par exemple, `Pokémon Feunard`).

### Explication :
- La mesure `Total_Revenu_Pokemon` calcule le revenu total pour toutes les ventes présentes dans la table `Ventes`.
- Lorsqu'un filtre est appliqué dans le rapport Power BI pour afficher uniquement les ventes de `Pokémon Feunard`, la mesure ajuste le calcul pour ne prendre en compte que les ventes de ce Pokémon.

## Conclusion

DAX est un langage puissant pour effectuer des calculs avancés dans Power BI. Maîtriser la modélisation des données, ainsi que les contextes de filtre et de ligne, est essentiel pour créer des rapports dynamiques et analytiques. Les exemples pratiques et les bonnes pratiques décrites ici permettent de poser les bases solides nécessaires pour commencer à exploiter pleinement la puissance de DAX dans Power BI.

## Ressources
- [Documentation officielle de DAX](https://docs.microsoft.com/fr-fr/dax/)
- [Modélisation des données dans Power BI](https://docs.microsoft.com/fr-fr/power-bi/guidance/star-schema)

[⬅ Page Précédente](../README.md)