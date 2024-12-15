# Mise en Place d'un Modèle de Machine Learning - Préparation des Données

## Introduction

La préparation des données est une étape cruciale dans la mise en place d'un modèle de machine learning. Elle implique plusieurs techniques qui permettent de rendre les données prêtes à être utilisées pour l'apprentissage d'un modèle. Ces étapes incluent le choix des variables pertinentes, l'encodage des données catégorielles, la normalisation et la standardisation des données numériques, ainsi que d'autres ajustements spécifiques pour maximiser les performances du modèle. Cette fiche technique propose une méthodologie complète pour préparer les données avant d’entraîner un modèle, en suivant une approche détaillée et structurée.

### Contexte d’utilisation

Cette fiche s’adresse aux débutants en machine learning. Elle détaille chaque étape de la préparation des données, avec des explications simples et des exemples de code à copier dans un notebook Jupyter (`.ipynb`), permettant de prédire des valeurs à partir des données préparées.

### Objectif

Le but de cette fiche est de fournir une trame complète permettant de préparer les données, de les encoder et de les rendre prêtes pour l’entraînement d’un modèle de machine learning supervisé (régression linéaire simple). Les concepts de normalisation, standardisation et encodage des variables catégorielles seront abordés avec des exemples pratiques.

---

## 1. Importation des Données

### Objectif

Avant de commencer à travailler sur les données, il est essentiel de les importer et d'effectuer une exploration rapide pour en comprendre la structure.

### Étape

Commencer par importer les bibliothèques nécessaires et charger les données.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Charger le jeu de données
df = pd.read_csv('nom_du_fichier.csv')

# Afficher les premières lignes pour un aperçu
df.head()
```

**Explication :**
- `pandas` est utilisé pour manipuler les données sous forme de DataFrame.
- `matplotlib` et `seaborn` permettent de visualiser les données.
- Le fichier `.csv` doit être remplacé par le chemin réel du fichier.
  
**Ce qu'il faut observer :**
- Vérifier la présence de valeurs manquantes.
- Identifier les types de données pour chaque colonne (numériques, catégorielles, etc.).

---

## 2. Nettoyage des Données

### Objectif

Les données brutes contiennent souvent des valeurs manquantes, des doublons ou des erreurs. Il est essentiel de nettoyer ces données pour éviter qu'elles ne faussent l'apprentissage du modèle.

### Étapes

#### 2.1 Vérification des valeurs manquantes

```python
# Vérifier les valeurs manquantes
df.isnull().sum()
```

**Explication :** Cette fonction permet de savoir combien de valeurs manquantes il y a par colonne. Les valeurs manquantes doivent être traitées avant de passer à l'étape suivante.

#### 2.2 Traitement des valeurs manquantes

Il existe plusieurs façons de gérer les valeurs manquantes :
- Suppression des lignes ou colonnes concernées.
- Remplissage par la moyenne, la médiane, ou d'autres valeurs.

Exemple de remplissage avec la moyenne (pour les données numériques) :

```python
df['colonne_numerique'] = df['colonne_numerique'].fillna(df['colonne_numerique'].mean())
```

---

## 3. Choix des Colonnes Pertinentes

### Objectif

Sélectionner les colonnes les plus pertinentes pour le modèle, c'est-à-dire celles qui ont un lien direct avec la variable cible.

### Étapes

#### 3.1 Identification des variables explicatives et de la variable cible

Par exemple, si l'objectif est de prédire le prix d'une maison (variable cible), les colonnes comme la superficie, le nombre de chambres, l'année de construction peuvent être pertinentes.

#### 3.2 Suppression des colonnes inutiles

Si certaines colonnes ne contiennent pas d'informations utiles (identifiants, colonnes redondantes), elles doivent être supprimées.

```python
df = df.drop(['colonne_à_supprimer'], axis=1)
```

---

## 4. Préparation des Données pour l'Apprentissage

### Objectif

Les modèles de machine learning ont besoin de données numériques et encodées pour fonctionner. Il faut donc convertir les données catégorielles et normaliser ou standardiser les variables numériques.

### 4.1 Normalisation et Standardisation des Valeurs Numériques

Les valeurs numériques doivent souvent être mises à une échelle commune. La **normalisation** transforme les données entre 0 et 1, tandis que la **standardisation** les transforme pour qu'elles aient une moyenne de 0 et un écart type de 1.

#### Normalisation

```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
df['colonne_numerique'] = scaler.fit_transform(df[['colonne_numerique']])
```

#### Standardisation

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
df['colonne_numerique'] = scaler.fit_transform(df[['colonne_numerique']])
```

**Explication :**
- **MinMaxScaler** : Pour amener les données dans une plage [0, 1].
- **StandardScaler** : Pour normaliser les données autour de 0 avec un écart type de 1.

#### Quand utiliser quoi ?
- Utiliser la **normalisation** lorsque les variables numériques doivent être dans un intervalle spécifique, comme pour les algorithmes basés sur la distance (ex. KNN, SVM).
- Utiliser la **standardisation** lorsque les algorithmes supposent une distribution normale des données (ex. régression linéaire).

### 4.2 Encodage des Variables Catégorielles

Les variables catégorielles doivent être converties en valeurs numériques pour être utilisées par les modèles.

#### Utilisation de `get_dummies`

```python
df_encoded = pd.get_dummies(df, drop_first=True)
```

**Explication :**
- Cette méthode crée des variables binaires pour chaque catégorie de la variable (par exemple, une variable "couleur" avec trois catégories : "rouge", "vert", "bleu" sera transformée en trois colonnes binaires).
- `drop_first=True` permet d'éviter la colinéarité en supprimant une catégorie.

### 4.3 Application de la Fonction d'Encodage Global

Une fonction générique pour normaliser, standardiser et encoder les données :

```python
from sklearn.preprocessing import StandardScaler, MinMaxScaler

def pretraitement(df):
    # Normalisation/Standardisation
    scaler = StandardScaler()  # Choisir entre MinMaxScaler() et StandardScaler()
    numerical_columns = df.select_dtypes(include=['float64', 'int64']).columns
    df[numerical_columns] = scaler.fit_transform(df[numerical_columns])
    
    # Encodage des variables catégorielles
    df = pd.get_dummies(df, drop_first=True)
    
    return df

df_encodé = pretraitement(df)
```

---

## 5. Entraînement du Modèle de Machine Learning

### Objectif

Une fois les données préparées, il est temps de les diviser en ensembles d’entraînement et de test, puis d’entraîner un modèle.

### Étapes

#### 5.1 Séparation des données en features (X) et cible (y)

```python
X = df_encodé.drop('target', axis=1)
y = df_encodé['target']
```

#### 5.2 Division des données en ensembles d’entraînement et de test

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

#### 5.3 Entraînement du modèle de régression linéaire

```python
from sklearn.linear_model import LinearRegression

model = LinearRegression()
model.fit(X_train, y_train)
```

**Explication :**
- Le modèle de régression linéaire est utilisé ici, mais d'autres modèles peuvent être envisagés en fonction du problème.
- `.fit()` entraîne le modèle sur les données d'entraînement.

---

## 6. Prédictions et Évaluation du Modèle

### Objectif

Après l'entraînement du modèle, il faut tester sa capacité à prédire des valeurs sur de nouvelles données.

### Étapes

#### 6.1 Prédictions

```python
y_pred = model.predict(X_test)
```

#### 6.2 Évaluation des performances du modèle

```python
from sklearn.metrics import mean_squared_error, r2_score

# Calcul de l'erreur quadratique moyenne et du R²
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

print(f'MSE: {mse}')
print(f'R²: {r2}')
```

**Explication :**
- Le **MSE (Mean Squared Error)** mesure la différence entre les valeurs prédites et réelles. Plus le MSE est faible, meilleur est le modèle.
- Le **R²** évalue la proportion de la variance des données expliquée par le modèle.

---

## Conclusion

La préparation des données est une étape fondamentale avant d'entraîner un modèle de machine learning. Cette fiche fournit une trame étape par étape pour effectuer les tâches courantes de nettoyage, d'encodage et de normalisation des données, avec des exemples de code permettant de préparer les données pour un modèle de régression linéaire simple. Chaque étape est expliquée avec un objectif clair, et le code fourni peut être copié directement dans un notebook Jupyter.

### Ressources utiles
- [Documentation scikit-learn](https://scikit-learn.org/stable/)
- [Tutoriel Machine Learning - Coursera](https://www.coursera.org/learn/machine-learning)
