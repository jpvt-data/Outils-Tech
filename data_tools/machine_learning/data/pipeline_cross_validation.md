[⬅ Page Précédente](../README.md)

# Pipeline - Cross-Validation

## Objectifs

- Comprendre la notion de validation croisée (Cross-Validation).
- Savoir utiliser la validation croisée dans Scikit-Learn pour évaluer la performance d'un modèle.

## Introduction

En machine learning, l'évaluation d'un modèle nécessite de tester sa capacité à généraliser sur des données non vues pendant l'entraînement. Une méthode courante pour éviter que le modèle ne soit trop ajusté aux données d'entraînement (overfitting) est la validation croisée (Cross-Validation). Cela consiste à diviser les données en plusieurs sous-ensembles, à entraîner le modèle sur certains d'entre eux et à évaluer sa performance sur les autres. Cette approche permet de mieux évaluer la performance d'un modèle tout en limitant les biais liés à un découpage arbitraire des données.

## Quand utiliser la Cross-Validation ?

La validation croisée est utile lorsque :
- Le jeu de données est limité, rendant les séparations simples entre un jeu d'entraînement et un jeu de test potentiellement non représentatives de la variabilité des données.
- On souhaite avoir une estimation robuste de la performance d'un modèle sans dépendre d'une seule partition des données.
- On veut éviter que les résultats d’évaluation ne soient influencés par un découpage mal choisi.

## Principe de la Cross-Validation

1. **Découpage des données** : On découpe l'ensemble des données en plusieurs sous-ensembles (ou "folds").
2. **Entraînement et évaluation** : À chaque itération, un sous-ensemble est utilisé comme jeu de test, et les autres comme jeu d'entraînement.
3. **Répétition** : Ce processus est répété plusieurs fois (selon le nombre de "folds" choisis), de manière à ce que chaque sous-ensemble serve à la fois de jeu de test et de jeu d'entraînement.
4. **Évaluation** : L’évaluation globale du modèle est obtenue par la moyenne des scores obtenus à chaque itération.

### Exemple visuel :
Supposons que nous ayons un jeu de données avec 5 sous-ensembles égaux. À chaque itération, un sous-ensemble est utilisé pour le test et les 4 autres pour l’entraînement. Ce processus est répété 5 fois, chaque sous-ensemble servant à tour de rôle de jeu de test.

| Iteration | Train (Entraînement) | Test (Validation) |
|-----------|----------------------|-------------------|
| 1         | Fold 2, Fold 3, Fold 4, Fold 5 | Fold 1           |
| 2         | Fold 1, Fold 3, Fold 4, Fold 5 | Fold 2           |
| 3         | Fold 1, Fold 2, Fold 4, Fold 5 | Fold 3           |
| 4         | Fold 1, Fold 2, Fold 3, Fold 5 | Fold 4           |
| 5         | Fold 1, Fold 2, Fold 3, Fold 4 | Fold 5           |

### Pourquoi utiliser la Cross-Validation ?
La validation croisée permet d'évaluer un modèle de manière plus robuste en utilisant différentes partitions des données. Elle permet de :
- **Réduire le biais de validation** : En effectuant plusieurs tests sur des sous-ensembles différents, on évite de dépendre d'une seule division des données.
- **Obtenir une estimation plus fiable** : La moyenne des scores obtenus à chaque itération offre une évaluation plus stable de la performance du modèle.

## Utilisation de la Cross-Validation avec Scikit-Learn

Scikit-learn, une bibliothèque populaire pour le machine learning en Python, propose des fonctions intégrées pour effectuer la validation croisée. L'une des plus courantes est `cross_val_score`, qui permet de réaliser une validation croisée sur un modèle donné.

### Exemple simple de Cross-Validation

Dans cet exemple, nous utilisons une régression logistique pour effectuer une validation croisée sur un jeu de données :

```python
# Importation des bibliothèques nécessaires
from sklearn.model_selection import cross_val_score
from sklearn.linear_model import LogisticRegression
from sklearn.datasets import load_iris

# Chargement du jeu de données Iris
X, y = load_iris(return_X_y=True)

# Application de la cross-validation sur une régression logistique
scores = cross_val_score(LogisticRegression(max_iter=200), X, y, cv=5)

# Affichage des scores pour chaque itération
print("Scores de chaque itération : ", scores)

# Calcul de la moyenne des scores
print("Moyenne des scores : ", scores.mean())
```

### Explication du code :

1. **Importation des bibliothèques** : On importe la fonction `cross_val_score` pour effectuer la validation croisée et le modèle de régression logistique `LogisticRegression` de scikit-learn. On utilise également le jeu de données Iris, un jeu de données standard pour les exemples en machine learning.
   
2. **Chargement des données** : Le jeu de données Iris est chargé avec `load_iris`, et `X` contient les caractéristiques des observations, tandis que `y` contient les labels (classes) associés.

3. **Validation croisée** : La fonction `cross_val_score` effectue la validation croisée sur le modèle de régression logistique. L'argument `cv=5` spécifie que nous allons effectuer une validation croisée avec 5 sous-ensembles (5 folds). Cette fonction retourne un tableau avec les scores obtenus pour chaque itération (fold).

4. **Affichage des résultats** : On affiche les scores de chaque itération, puis la moyenne des scores pour obtenir une estimation globale de la performance du modèle.

### Résultat attendu :

Le résultat sera un tableau avec 5 scores, un pour chaque sous-ensemble du jeu de données, et la moyenne de ces scores pour obtenir une estimation plus fiable.

```
Scores de chaque itération :  [0.96666667 0.96666667 0.96666667 0.96666667 1.        ]
Moyenne des scores :  0.9733333333333334
```

## Personnalisation de la Cross-Validation

Il est possible de personnaliser la validation croisée en ajustant certains paramètres de la fonction `cross_val_score` :

1. **Le modèle** : Vous pouvez utiliser n'importe quel modèle de machine learning disponible dans scikit-learn, comme les classificateurs KNN, les arbres de décision, etc.
   
2. **Le nombre de folds** (`cv`) : Par défaut, `cv=5`, ce qui signifie que le jeu de données sera divisé en 5 sous-ensembles. Vous pouvez changer ce nombre selon vos besoins.

3. **L'argument `scoring`** : Par défaut, `cross_val_score` utilise l'exactitude (accuracy) pour évaluer le modèle. Vous pouvez spécifier un autre critère d'évaluation comme `roc_auc` pour une classification binaire ou `neg_mean_squared_error` pour une régression.

### Exemple avec un autre modèle et un nombre de folds personnalisé :

```python
from sklearn.model_selection import cross_val_score
from sklearn.neighbors import KNeighborsClassifier
from sklearn.datasets import load_iris

# Chargement des données
X, y = load_iris(return_X_y=True)

# Application de la cross-validation sur un classificateur KNN
scores = cross_val_score(KNeighborsClassifier(weights='distance'), X, y, cv=3)

# Affichage des scores
print("Scores de chaque itération : ", scores)
print("Moyenne des scores : ", scores.mean())
```

### Paramètre `cv` :

Dans cet exemple, nous avons défini `cv=3` pour effectuer une validation croisée avec 3 sous-ensembles. Le nombre de folds à utiliser dépend généralement du volume de données et des exigences de calcul.

## Cas d'usage et Limites

La validation croisée est largement utilisée dans des situations où la robustesse de l’évaluation du modèle est essentielle. Elle est utilisée :
- Pour évaluer des modèles en classification et en régression.
- Pour comparer plusieurs modèles entre eux de manière plus fiable.
- Lorsqu'un jeu de données est limité.

Cependant, la validation croisée peut être coûteuse en termes de calcul pour de très grands jeux de données, car elle nécessite de répéter l'entraînement du modèle plusieurs fois. Dans ces cas-là, des approches comme la "validation croisée par k-fold" ou la "validation croisée avec un nombre réduit de folds" peuvent être plus adaptées.

## Ressources supplémentaires
- [Documentation scikit-learn - cross_val_score](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.cross_val_score.html)
- [Exemple d'utilisation sur un jeu de données de vin avec k-NN et cross-validation](http://www.xavierdupre.fr/app/papierstat/helpsphinx/notebooks/wines_knn_cross_val.html)

[⬅ Page Précédente](../README.md)