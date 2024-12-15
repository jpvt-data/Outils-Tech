# Train-Test Split en Machine Learning

## Introduction
Dans l'apprentissage automatique, l'une des étapes cruciales de la création et de l'évaluation d'un modèle consiste à diviser les données en plusieurs ensembles, notamment un ensemble d'entraînement et un ensemble de test. L'objectif de cette séparation est d'éviter que le modèle ne "mémorise" les données d'entraînement, ce qui pourrait entraîner une mauvaise généralisation sur de nouvelles données. Cette technique est particulièrement importante pour assurer la robustesse du modèle, en permettant une évaluation réaliste de ses performances sur des données non vues pendant l'entraînement.

Le processus de séparation des données en "train" et "test" est connu sous le nom de **Train-Test Split**.

## Objectifs
✅ Comprendre la nécessité de diviser les données en ensembles d'entraînement et de test.  
✅ Apprendre à utiliser la fonction `train_test_split` de scikit-learn.  
✅ Appréhender l'importance de la validation croisée et du mélange aléatoire des données.  

## Quand utiliser cette méthode ?
Le Train-Test Split est utilisé chaque fois qu'un modèle est construit en machine learning. Il permet de s'assurer que le modèle est testé sur un jeu de données distinct de celui qu'il a utilisé pour apprendre, ce qui permet d'éviter le sur-apprentissage (overfitting).

## Le concept du Train-Test Split
Lorsqu'on crée un modèle de machine learning, il est essentiel de diviser les données en deux parties principales :
1. **Ensemble d'entraînement** (train set) : utilisé pour entraîner le modèle.
2. **Ensemble de test** (test set) : utilisé pour évaluer la performance du modèle.

Cette séparation garantit que les résultats du modèle sont représentatifs de sa capacité à généraliser à de nouvelles données. Une règle courante consiste à utiliser environ 70-80% des données pour l'entraînement et 20-30% pour le test.

### Pourquoi diviser les données ?
Sans cette division, le modèle pourrait simplement "mémoriser" les données d'entraînement, ce qui l'amènerait à obtenir de très bons résultats sur ces mêmes données, mais de mauvais résultats lorsqu'il est confronté à de nouvelles données. Cela constitue le problème du **sur-ajustement (overfitting)**.

### Le mélange aléatoire des données
Avant de diviser les données en ensembles d'entraînement et de test, il est important de "mélanger" ou de "randomiser" les données. Cela permet de garantir que les échantillons d'entraînement et de test sont représentatifs de l'ensemble des données et non biaisés par des patterns chronologiques ou autres structures cachées dans les données.

## Étapes du Train-Test Split avec Python
Voici les étapes pour utiliser la méthode `train_test_split` de la bibliothèque scikit-learn. Le processus est simple et très efficace.

### 1. Importation des bibliothèques nécessaires
Commencer par importer les bibliothèques nécessaires pour réaliser le train-test split. On aura principalement besoin de `train_test_split` de scikit-learn, ainsi que de pandas pour manipuler les données :

```python
import pandas as pd
from sklearn.model_selection import train_test_split
```

### 2. Charger les données
Les données doivent être sous forme de DataFrame, généralement avec pandas. Voici un exemple de chargement d'un jeu de données fictif dans un DataFrame :

```python
# Exemple de jeu de données
data = {'Feature1': [1, 2, 3, 4, 5], 
        'Feature2': [10, 20, 30, 40, 50], 
        'Target': [100, 200, 300, 400, 500]}

df = pd.DataFrame(data)
```

### 3. Séparer les variables explicatives (X) et la variable cible (y)
Avant de diviser les données, il faut séparer les variables explicatives (X) de la variable cible (y). 

```python
X = df[['Feature1', 'Feature2']]  # Variables explicatives
y = df['Target']  # Variable cible
```

### 4. Appliquer le Train-Test Split
Une fois les variables séparées, il est temps d'appliquer `train_test_split` pour diviser les données. Par défaut, cette fonction va mélanger les données avant de les diviser. Vous pouvez spécifier la proportion des données à utiliser pour l'entraînement et pour le test en ajustant le paramètre `train_size` (ou `test_size`).

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

- `test_size=0.2` indique que 20% des données seront utilisées pour l'évaluation du modèle et 80% pour l'entraînement.
- `random_state=42` permet de fixer la graine de randomisation, garantissant que la division des données soit reproductible (toujours la même séparation si le code est exécuté à nouveau).

### 5. Vérification des ensembles
Après la séparation, il est important de vérifier que les ensembles d'entraînement et de test ont été créés correctement. Voici un exemple pour vérifier les tailles de chaque ensemble :

```python
print(f"Taille de X_train: {X_train.shape[0]}")
print(f"Taille de X_test: {X_test.shape[0]}")
```

Cela permettra de confirmer que les ensembles sont correctement séparés selon la proportion choisie.

## Résumé de la fonction `train_test_split`

| Paramètre          | Description                                                     |
|--------------------|-----------------------------------------------------------------|
| `X`                | Variables explicatives (features).                              |
| `y`                | Variable cible (target).                                       |
| `test_size`        | Proportion de données à utiliser pour le test (entre 0 et 1).   |
| `train_size`       | Proportion de données à utiliser pour l'entraînement (entre 0 et 1). |
| `random_state`     | Graine de randomisation pour assurer la reproductibilité.       |

## Importance de la validation croisée
Dans certains cas, surtout avec un petit jeu de données, il est recommandé d'utiliser la **validation croisée**. Cette méthode divise les données en plusieurs sous-ensembles, en utilisant successivement chaque sous-ensemble pour tester le modèle et les autres pour l'entraîner. Cela permet une évaluation plus robuste de la performance du modèle.

### Exemple de validation croisée avec `cross_val_score` :
```python
from sklearn.model_selection import cross_val_score
from sklearn.linear_model import LinearRegression

# Création du modèle
model = LinearRegression()

# Validation croisée
scores = cross_val_score(model, X, y, cv=5)  # cv=5 pour une validation croisée à 5 plis
print(f"Scores de validation croisée: {scores}")
print(f"Score moyen: {scores.mean()}")
```

## Conclusion
Le **Train-Test Split** est une étape essentielle dans la création d'un modèle d'apprentissage supervisé. Il permet de s'assurer que le modèle ne surajuste pas les données d'entraînement et est capable de généraliser sur de nouvelles données. Utiliser correctement cette technique aide à obtenir des modèles plus robustes et mieux adaptés à des situations réelles.
