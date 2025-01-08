[⬅ Page Précédente](../README.md)

# Machine Learning Pipeline : GridSearch & Randomized Search

## Introduction

Lors de l'entraînement d'un modèle de Machine Learning, il est crucial de trouver les meilleurs hyperparamètres pour optimiser la performance du modèle. Les hyperparamètres sont des paramètres définis avant l'entraînement du modèle, tels que le nombre de voisins dans un modèle K-Nearest Neighbors (KNN) ou le taux d'apprentissage dans un réseau de neurones. 

Il existe différentes méthodes pour trouver ces valeurs optimales, et parmi celles-ci, **GridSearchCV** et **RandomizedSearchCV** sont les plus courantes. Ces méthodes permettent d'effectuer une recherche systématique sur un ensemble de paramètres afin de déterminer les meilleurs pour un modèle donné. Cette fiche détaillée explique ces deux techniques et leur utilisation avec la bibliothèque **Scikit-Learn**.

## Objectifs

- **Comprendre la notion de GridSearch** et son fonctionnement.
- **Utiliser GridSearch et RandomizedSearch** pour optimiser les hyperparamètres d'un modèle de Machine Learning.

### Quand utiliser cette méthode ?

L'utilisation de **GridSearchCV** ou **RandomizedSearchCV** est particulièrement utile dans les situations suivantes :

1. Lors de l'entraînement de modèles sur des jeux de données complexes, où les paramètres influencent significativement la performance.
2. Lorsque plusieurs hyperparamètres doivent être ajustés, et que les combinaisons sont nombreuses.
3. Pour éviter un ajustement manuel des paramètres, ce qui peut être fastidieux et subjectif.

## GridSearchCV : Recherche exhaustive des paramètres

### Fonctionnement

**GridSearchCV** réalise une recherche exhaustive sur un espace de hyperparamètres défini. Cela signifie qu'il essaie toutes les combinaisons possibles de valeurs données pour chaque paramètre.

### Étapes

1. **Définir un dictionnaire des hyperparamètres** à tester. Chaque clé correspond à un paramètre, et la valeur associée est une liste des valeurs possibles pour ce paramètre.
2. **Initialiser l'objet GridSearchCV** en précisant le modèle à utiliser et le dictionnaire des hyperparamètres.
3. **Exécuter la recherche** en appelant la méthode `fit()` de GridSearchCV, qui entraînera le modèle pour chaque combinaison de paramètres.
4. **Analyser les résultats** pour connaître les meilleures combinaisons de paramètres en fonction du score de validation croisée.

### Exemple de code avec GridSearchCV

Dans cet exemple, on utilise **KNeighborsClassifier** et on optimise le paramètre `n_neighbors`.

```python
from sklearn.model_selection import GridSearchCV
from sklearn.neighbors import KNeighborsClassifier
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split

# Charger un jeu de données d'exemple
X, y = load_iris(return_X_y=True)

# Définir un dictionnaire des hyperparamètres à tester
param_grid = {'n_neighbors': [1, 10, 50, 100]}

# Initialiser GridSearchCV avec le modèle et le dictionnaire des hyperparamètres
grid_search = GridSearchCV(KNeighborsClassifier(), param_grid)

# Diviser les données en ensemble d'entraînement et de test
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Entraîner le modèle avec GridSearchCV
grid_search.fit(X_train, y_train)

# Afficher les meilleurs paramètres et le score associé
print("Best score:", grid_search.best_score_)
print("Best parameters:", grid_search.best_params_)
```

#### Explication du code

1. **Chargement du jeu de données** : Ici, on utilise le jeu de données Iris pour l'exemple. Il est importé via `load_iris()`.
2. **Paramètres à tester** : Le dictionnaire `param_grid` contient le paramètre `n_neighbors` à tester avec différentes valeurs.
3. **GridSearchCV** : On initialise l'objet `grid_search` avec le modèle de classification KNN et le dictionnaire d'hyperparamètres. GridSearch va tester chaque valeur de `n_neighbors` et évaluer leur performance.
4. **Résultats** : Après l'entraînement, les meilleurs paramètres (`best_params_`) et le score obtenu (`best_score_`) sont affichés.

### Cross-validation dans GridSearchCV

Par défaut, **GridSearchCV** applique une validation croisée à 5 folds (5 divisions des données pour l'évaluation), ce qui permet de tester la robustesse du modèle.

### Résultats détaillés

Après l'exécution, on peut examiner les résultats détaillés en accédant à l'attribut `cv_results_`. Cela contient des informations sur le temps de formation, le score moyen de test, etc.

```python
print(grid_search.cv_results_)
```

#### Analyse des résultats

Les principaux résultats à observer sont :
- `mean_test_score` : le score moyen pour chaque combinaison de paramètres.
- `params` : les combinaisons de paramètres testées.
- `rank_test_score` : le rang des combinaisons de paramètres en fonction du score.

### Ajouter plusieurs hyperparamètres

On peut tester plusieurs hyperparamètres en même temps. Par exemple, dans le cas du **KNeighborsClassifier**, on pourrait vouloir tester à la fois le nombre de voisins (`n_neighbors`) et le type de poids (`weights`).

```python
param_grid = {'n_neighbors': [1, 10, 50, 100], 'weights': ['uniform', 'distance']}
grid_search = GridSearchCV(KNeighborsClassifier(), param_grid)
grid_search.fit(X_train, y_train)
```

### RandomizedSearchCV : Recherche aléatoire

Lorsque le nombre de paramètres à tester devient très important, **GridSearchCV** peut prendre trop de temps pour s'exécuter. Dans ce cas, **RandomizedSearchCV** est une alternative qui permet de tester un nombre limité de combinaisons aléatoires d'hyperparamètres.

#### Fonctionnement

Au lieu de tester toutes les combinaisons possibles, **RandomizedSearchCV** sélectionne un nombre fixe de combinaisons aléatoires à tester. Cela réduit le temps d'exécution tout en offrant une bonne approximation des meilleurs paramètres.

### Exemple de code avec RandomizedSearchCV

```python
from sklearn.model_selection import RandomizedSearchCV
from sklearn.neighbors import KNeighborsClassifier

# Définir un dictionnaire des hyperparamètres
param_dist = {'n_neighbors': range(2, 101), 'weights': ['uniform', 'distance']}

# Initialiser RandomizedSearchCV avec le modèle et le dictionnaire des hyperparamètres
random_search = RandomizedSearchCV(KNeighborsClassifier(), param_dist, n_iter=15)

# Entraîner le modèle
random_search.fit(X_train, y_train)

# Afficher les meilleurs paramètres et le score associé
print("Best score:", random_search.best_score_)
print("Best parameters:", random_search.best_params_)
```

#### Explication du code

- `param_dist` définit une plage de valeurs pour `n_neighbors` entre 2 et 100, ainsi que deux options pour `weights`.
- `n_iter=15` indique que RandomizedSearchCV va tester 15 combinaisons aléatoires.
- Après l'entraînement, les meilleurs résultats sont affichés.

### Conclusion

- **GridSearchCV** est très utile pour une recherche exhaustive des meilleurs hyperparamètres lorsque le nombre de combinaisons est raisonnable.
- **RandomizedSearchCV** permet d'optimiser rapidement les paramètres lorsque le nombre de possibilités est élevé, en testant un échantillon aléatoire de combinaisons.

## Ressources

- [Documentation officielle GridSearchCV](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html)
- [Documentation officielle RandomizedSearchCV](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.RandomizedSearchCV.html)

[⬅ Page Précédente](../README.md)