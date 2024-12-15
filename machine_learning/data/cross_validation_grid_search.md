## Machine Learning - Cross-validation et Grid-search

### Introduction

La performance d'un modèle de machine learning est directement liée aux données utilisées pour son entraînement et sa validation. Un petit changement dans ces données peut modifier significativement les résultats. Ainsi, il est essentiel de s'assurer que les scores obtenus reflètent une performance générale et non un artefact des données sélectionnées. Cette fiche explore les notions de validation croisée (cross-validation) et de recherche systématique d'hyperparamètres (Grid-Search), des outils clés pour évaluer et optimiser les modèles. Nous appliquerons ces concepts à des exemples concrets.

### Objectifs

- Comprendre la validation croisée et son rôle.
- Utiliser la validation croisée dans Scikit-Learn.
- Différencier les concepts de paramètre et d'hyperparamètre.
- Mettre en pratique Grid-Search pour optimiser les hyperparamètres.

### Validation croisée : du `train_test_split` au K-fold

La validation croisée est une technique statistique permettant de diviser un jeu de données en plusieurs sous-ensembles ("folds") pour évaluer les performances d'un modèle de manière plus robuste. Contrairement au simple `train_test_split`, qui sépare les données en un jeu d'entraînement et un jeu de validation une seule fois, la validation croisée répète ce processus sur plusieurs partitions.

#### Exemple de K-folds

Prenons un jeu de données d'iris et appliquons une régression logistique :

```python
from sklearn.model_selection import cross_val_score
from sklearn.linear_model import LogisticRegression
from sklearn.datasets import load_iris

# Charger les données Iris
iris = load_iris()
X, y = iris.data, iris.target

# Cross-validation à 5 folds
scores = cross_val_score(LogisticRegression(), X, y, cv=5)
print(scores)
print(f"Score moyen : {scores.mean():.3f}")
```

- Le jeu de données est divisé en 5 sous-ensembles.
- Le modèle est entraîné sur 4 sous-ensembles et validé sur le 5ᵉ.
- Ce processus est répété pour chaque partition, et une moyenne des scores est calculée.

#### Avantages

- **Fiabilité** : Limiter les biais dus à un unique découpage.
- **Évaluation généralisée** : Fournit une meilleure estimation de la performance réelle.

#### Paramètres importants

- `cv` : Nombre de folds. Par défaut, à 5 dans Scikit-Learn.
- `scoring` : Permet de spécifier la métrique utilisée pour l'évaluation (précision, rappel, F1-score, etc.).

### Paramètres et hyperparamètres

#### Paramètres

Les paramètres sont déterminés à partir des données lors de l'entraînement. Par exemple, dans une régression linéaire, les coefficients de la droite de régression sont des paramètres calculés pour minimiser l'erreur.

#### Hyperparamètres

Les hyperparamètres sont fixés avant l'entraînement. Ils influencent la structure et le comportement global du modèle. Par exemple, dans une régression logistique, le paramètre de régularisation `C` est un hyperparamètre.

### Optimisation des hyperparamètres avec Grid-Search

Grid-Search est une méthode systématique permettant d'explorer l'espace des hyperparamètres et d'identifier la meilleure combinaison. Chaque combinaison est évaluée avec validation croisée.

#### Exemple pratique : Choisir le meilleur modèle pour les données Iris

Nous comparons deux modèles : un classificateur KNN et une SVM (Support Vector Machine). Nous allons optimiser leurs hyperparamètres.

```python
from sklearn.model_selection import GridSearchCV
from sklearn.neighbors import KNeighborsClassifier
from sklearn.svm import SVC
from sklearn.datasets import load_iris

# Charger les données
iris = load_iris()
X, y = iris.data, iris.target

# Modèles et grilles d'hyperparamètres
models = [KNeighborsClassifier(), SVC()]
param_grids = [
    {'n_neighbors': [3, 5, 7, 9]},
    {'kernel': ['linear', 'rbf'], 'C': [0.1, 1, 10, 100]},
]

# Grid-Search avec validation croisée
for model, param_grid in zip(models, param_grids):
    gs = GridSearchCV(estimator=model, param_grid=param_grid, cv=5)
    gs.fit(X, y)
    print(f"Meilleur score pour {model.__class__.__name__}: {gs.best_score_:.3f}")
    print(f"Meilleurs paramètres pour {model.__class__.__name__}: {gs.best_params_}")
```

- **KNN** : Nous testons différents nombres de voisins.
- **SVM** : Nous explorons deux types de kernel et des valeurs variées pour le paramètre de régularisation `C`.

#### Résultats attendus

- Le meilleur modèle est celui qui maximise le score moyen avec la validation croisée.
- Les paramètres optimaux sont affichés pour chaque modèle.

#### Points d’attention

1. **Coût en temps de calcul** : Grid-Search teste de nombreuses combinaisons, ce qui peut être long sur de grands ensembles de données.
2. **Grille raisonnable** : Ne pas surcharger la grille avec trop de valeurs pour chaque hyperparamètre.

### Liens entre Grid-Search et cross-validation

La validation croisée est intégrée dans Grid-Search via le paramètre `cv`. Elle assure que chaque combinaison d’hyperparamètres est évaluée sur plusieurs partitions des données, augmentant la fiabilité des résultats.

#### Exemple : Optimisation d'une Random Forest

```python
from sklearn.model_selection import GridSearchCV
from sklearn.ensemble import RandomForestClassifier

# Grille d'hyperparamètres
param_grid = {
    'n_estimators': [100, 200],
    'max_depth': [10, 20, None],
}

# Modèle Random Forest
model = RandomForestClassifier()
gs = GridSearchCV(estimator=model, param_grid=param_grid, cv=5)
gs.fit(X, y)

print(f"Meilleur score : {gs.best_score_:.3f}")
print(f"Meilleurs paramètres : {gs.best_params_}")
```

### Conclusion

La validation croisée et Grid-Search sont des outils essentiels pour améliorer la fiabilité des modèles et optimiser leurs hyperparamètres. En les combinant avec des données concrètes, il est possible de produire des modèles robustes et performants, adaptés aux besoins spécifiques des projets.

