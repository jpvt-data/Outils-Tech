# Machine Learning : Régression Linéaire Multiple avec Python (Scikit-Learn)

## Introduction

La régression linéaire multiple est une méthode utilisée en machine learning pour prédire une variable cible (y) en fonction de plusieurs variables explicatives (X). Contrairement à la régression linéaire simple, qui se base sur une seule variable explicative, la régression linéaire multiple permet de modéliser des relations complexes entre une variable cible et plusieurs variables indépendantes. 

L'objectif de cette fiche technique est de guider l'utilisateur, étape par étape, à travers l'implémentation d'une régression linéaire multiple à l'aide de Python et de la bibliothèque Scikit-Learn. La régression linéaire multiple est une méthode supervisée, ce qui signifie qu'elle repose sur des données d'apprentissage étiquetées, avec une variable cible (y) que l'on cherche à prédire à partir des variables explicatives (X).

Cette approche est couramment utilisée pour des tâches comme la prédiction des prix immobiliers, des résultats financiers, ou encore la prédiction de performances dans divers domaines d'activité. Elle permet de mieux comprendre l'impact de chaque variable explicative sur la variable cible.

## Quand utiliser la régression linéaire multiple ?

La régression linéaire multiple est idéale lorsque plusieurs facteurs influencent un phénomène que l'on souhaite prédire. Par exemple, dans le cadre de l'immobilier, la prédiction du prix d'une maison pourrait dépendre de plusieurs facteurs comme la superficie, le nombre de chambres, l'année de construction, etc. Cette méthode permet de capturer ces relations complexes et d’obtenir des prédictions basées sur plusieurs variables.

### Exemple d'application
Supposons que l'on veuille prédire le prix d'une maison en fonction de sa superficie, de son nombre de chambres et de sa proximité avec des écoles. Le prix de la maison serait la variable cible (y), tandis que la superficie, le nombre de chambres et la proximité à l'école seraient les variables explicatives (X).

## Étapes pour effectuer une régression linéaire multiple

### 1. Importer les bibliothèques nécessaires

Avant de commencer, il est important d'importer les bibliothèques nécessaires pour effectuer une régression linéaire multiple. Voici les bibliothèques que l'on va utiliser :

```python
import pandas as pd
import numpy as np
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error
```

**Explication :**

- `pandas` : pour manipuler les données sous forme de DataFrame.
- `numpy` : pour effectuer des calculs mathématiques.
- `LinearRegression` : pour créer et entraîner le modèle de régression linéaire.
- `train_test_split` : pour séparer les données en ensembles d'entraînement et de test.
- `mean_squared_error` : pour évaluer la performance du modèle.

### 2. Charger et préparer les données

Imaginons un DataFrame `df` contenant les variables explicatives et la variable cible. Voici comment charger et préparer les données :

```python
df = pd.read_csv("data.csv")  # Charger les données depuis un fichier CSV

# Supposons que les colonnes soient : 'superficie', 'chambres', 'proximite_ecole', 'prix'
X = df[['superficie', 'chambres', 'proximite_ecole']]  # Variables explicatives
y = df['prix']  # Variable cible
```

**Explication :**

- `df[['superficie', 'chambres', 'proximite_ecole']]` : sélectionne les colonnes utilisées comme variables explicatives.
- `df['prix']` : sélectionne la colonne cible (ici le prix de la maison).

### 3. Séparer les données en ensembles d'entraînement et de test

Avant de former le modèle, il est essentiel de diviser les données en deux ensembles : un pour entraîner le modèle et un autre pour tester sa performance.

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

**Explication :**

- `train_test_split` : divise les données en un ensemble d’entraînement (80%) et un ensemble de test (20%).
- `test_size=0.2` : 20% des données seront utilisées pour tester le modèle.
- `random_state=42` : assure que la division des données est reproductible à chaque exécution du code.

### 4. Créer et entraîner le modèle de régression linéaire

Maintenant que les données sont prêtes, on peut créer un modèle de régression linéaire et l’entraîner sur les données d'entraînement.

```python
model = LinearRegression()
model.fit(X_train, y_train)
```

**Explication :**

- `LinearRegression()` : crée un objet de régression linéaire.
- `model.fit(X_train, y_train)` : entraîne le modèle sur l’ensemble d’entraînement.

### 5. Examiner les coefficients du modèle

Une fois le modèle entraîné, on peut examiner les coefficients des variables explicatives. Ces coefficients indiquent l'importance de chaque variable dans la prédiction de la variable cible.

```python
print("Coefficients :", model.coef_)
print("Intercept :", model.intercept_)
```

**Explication :**

- `model.coef_` : affiche les coefficients de chaque variable explicative.
- `model.intercept_` : affiche l’interception (ou ordonnée à l’origine) du modèle, c’est-à-dire la valeur de y lorsque toutes les variables explicatives sont nulles.

### 6. Faire des prédictions

Une fois le modèle formé, il peut être utilisé pour prédire de nouvelles valeurs en fonction de nouvelles entrées de données.

```python
predictions = model.predict(X_test)
print(predictions)
```

**Explication :**

- `model.predict(X_test)` : prédit les valeurs de y en utilisant les variables explicatives de l'ensemble de test `X_test`.

### 7. Évaluer la performance du modèle

Une manière courante d’évaluer la performance d’un modèle de régression est d’utiliser l’erreur quadratique moyenne (MSE).

```python
mse = mean_squared_error(y_test, predictions)
print("Mean Squared Error:", mse)
```

**Explication :**

- `mean_squared_error(y_test, predictions)` : calcule l’erreur quadratique moyenne entre les valeurs réelles `y_test` et les valeurs prédites `predictions`.
- Un MSE plus faible indique une meilleure précision du modèle.

### Exemple complet de régression linéaire multiple :

Voici un exemple complet avec des données fictives :

```python
import pandas as pd
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error

# Exemple de données fictives
data = {'superficie': [50, 60, 80, 100, 120],
        'chambres': [2, 3, 3, 4, 5],
        'proximite_ecole': [1, 0, 1, 0, 1],
        'prix': [150000, 180000, 220000, 250000, 280000]}

df = pd.DataFrame(data)

X = df[['superficie', 'chambres', 'proximite_ecole']]
y = df['prix']

# Séparation des données
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Création et entraînement du modèle
model = LinearRegression()
model.fit(X_train, y_train)

# Affichage des coefficients et de l'intercept
print("Coefficients :", model.coef_)
print("Intercept :", model.intercept_)

# Prédictions sur l'ensemble de test
predictions = model.predict(X_test)
print("Prédictions :", predictions)

# Évaluation du modèle
mse = mean_squared_error(y_test, predictions)
print("Mean Squared Error:", mse)
```

### Conclusion

La régression linéaire multiple est un outil puissant pour la prédiction basée sur plusieurs variables. Grâce à Scikit-Learn, il est simple de créer un modèle, d'examiner ses coefficients, de faire des prédictions et d'évaluer sa performance. Ce type de modèle est largement utilisé dans divers domaines où plusieurs facteurs influencent une variable cible, comme dans l'immobilier, la finance, la santé, etc.

### Ressources supplémentaires

- [Régression linéaire multiple - Explication vidéo](https://www.youtube.com/watch?v=zITIFTsivN8)
- [Machine Learning avec Scikit-Learn - Documentation officielle](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html)
