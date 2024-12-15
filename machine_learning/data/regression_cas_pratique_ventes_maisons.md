# Mise en pratique - Régression - Prédiction des ventes de maisons

## Contexte et objectif

L’objectif de cet exercice est de réaliser une prédiction des prix des maisons en utilisant la régression linéaire multiple. Ce type de régression est supervisé, ce qui signifie que l’on dispose d’un ensemble de données avec des résultats (le prix de vente des maisons) et que l’on cherche à prédire ce résultat en fonction de plusieurs variables (comme la superficie, le nombre de chambres, etc.). Ce cas d’étude est particulièrement pertinent pour aborder des problématiques de prédiction dans des secteurs comme l'immobilier.

### Quand utiliser cette méthode ?

La régression linéaire multiple est utilisée lorsqu'on veut prédire une variable continue (ici le prix de la maison) à partir de plusieurs variables indépendantes. Il est essentiel de comprendre les relations entre les différentes variables avant de les intégrer dans un modèle de régression. Ce modèle est utile lorsqu'on cherche à avoir une prévision quantitative basée sur des données historiques.

### Objectifs de l'exercice
- **Analyser le dataset** : comprendre les données, leurs distributions, et les relations entre les variables.
- **Effectuer une régression linéaire multiple** : prédire les prix de vente des maisons.
- **Évaluer la performance du modèle** : comparer les résultats sur un jeu de données d'entraînement et un jeu de test.

---

## 1. Chargement des données et analyse initiale

### Description des données

Le dataset contient des informations relatives à la vente de maisons. Voici un tableau synthétisant les principales colonnes du dataset :

| **Colonne**            | **Description**                                                                 |
|------------------------|---------------------------------------------------------------------------------|
| `id`                   | Identifiant unique pour chaque maison                                           |
| `date`                 | Date de la vente de la maison                                                   |
| `price`                | Prix de vente de la maison                                                      |
| `bedrooms`             | Nombre de chambres                                                               |
| `bathrooms`            | Nombre de salles de bain                                                         |
| `sqft_living`          | Superficie habitable intérieure                                                  |
| `sqft_lot`             | Superficie du terrain                                                            |
| `floors`               | Nombre d'étages                                                                  |
| `waterfront`           | Variable binaire (1 si vue sur l'eau, 0 sinon)                                  |
| `view`                 | Indice de qualité de la vue (de 0 à 4)                                           |
| `condition`            | Indice de l'état de la maison (de 1 à 5)                                         |
| `grade`                | Indice de qualité de la construction (de 1 à 13)                                 |
| `sqft_above`           | Superficie habitable au-dessus du niveau du sol                                  |
| `sqft_basement`        | Superficie habitable du sous-sol                                                 |
| `yr_built`             | Année de construction de la maison                                              |
| `yr_renovated`         | Année de la dernière rénovation                                                 |
| `zipcode`              | Code postal de la maison                                                        |
| `lat`, `long`          | Coordonnées géographiques (latitude et longitude)                               |
| `sqft_living15`        | Superficie habitable des 15 voisins les plus proches                             |
| `sqft_lot15`           | Superficie des terrains des 15 voisins les plus proches                         |

### Chargement et exploration initiale du dataset

Avant de commencer l’analyse des données, il est important de charger le dataset et d’obtenir un premier aperçu des données.

```python
import pandas as pd

# Charger les données depuis l'URL
url = "https://raw.githubusercontent.com/murpi/wilddata/master/quests/kc_house_data.csv"
data = pd.read_csv(url)

# Aperçu des 5 premières lignes du dataset
data.head()

# Informations générales sur le dataset
data.info()

# Statistiques descriptives
data.describe()
```

**Explications** :
- `data.head()` affiche les premières lignes du dataset pour un aperçu rapide.
- `data.info()` donne des informations sur les types de données et la présence de valeurs manquantes.
- `data.describe()` fournit des statistiques descriptives pour chaque colonne numérique (moyenne, écart-type, quartiles, etc.).

---

## 2. Exploration graphique des données

Une bonne exploration graphique est essentielle pour comprendre les relations entre les variables et détecter des anomalies ou des tendances.

### Visualisation des distributions et des relations

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Distribution des prix de vente
sns.histplot(data['price'], kde=True)
plt.title('Distribution des prix de vente')
plt.show()

# Matrice de corrélation
corr_matrix = data.corr()
sns.heatmap(corr_matrix, annot=True, cmap='coolwarm')
plt.title('Matrice de corrélation')
plt.show()
```

**Explications** :
- `sns.histplot(data['price'], kde=True)` affiche la distribution du prix de vente avec une courbe de densité pour observer sa forme.
- `data.corr()` calcule la matrice de corrélation entre toutes les variables numériques du dataset, et `sns.heatmap()` permet de visualiser cette matrice. Les variables très corrélées entre elles peuvent être utiles pour la régression.

---

## 3. Sélection des variables et préparation des données

La régression linéaire multiple nécessite que l'on choisisse les variables (X) qui influenceront la prédiction de la variable cible (y), ici le prix.

### Sélection des variables pertinentes

Le prix (`price`) sera la variable cible (y), et les autres variables serviront de caractéristiques (X). On peut commencer par tester plusieurs variables et évaluer leur importance.

```python
# Sélection des variables pertinentes (par exemple, en fonction de la corrélation)
X = data[['sqft_living', 'bedrooms', 'bathrooms', 'sqft_lot', 'floors', 'waterfront', 'view', 'condition', 'grade']]
y = data['price']
```

**Explications** :
- `X` contient les variables explicatives (caractéristiques), choisies en fonction de leur relation avec le prix (observée via la matrice de corrélation).
- `y` contient le prix de la maison, la variable cible.

---

## 4. Entraînement et test du modèle

Une étape cruciale en machine learning est de diviser les données en deux ensembles : un ensemble d'entraînement pour créer le modèle, et un ensemble de test pour évaluer sa performance.

### Diviser les données

```python
from sklearn.model_selection import train_test_split

# Diviser les données en ensemble d'entraînement et de test
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

**Explications** :
- `train_test_split()` sépare les données en ensembles d’entraînement (80%) et de test (20%). Cela permet de valider le modèle sur des données qu’il n’a pas vues.

### Entraînement du modèle de régression linéaire

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

# Créer le modèle
model = LinearRegression()

# Entraîner le modèle
model.fit(X_train, y_train)

# Prédictions sur l'ensemble de test
y_pred = model.predict(X_test)

# Calcul de l'erreur et du score R2
mse = mean_squared_error(y_test, y_pred)
r2 = r2_score(y_test, y_pred)

print(f'Mean Squared Error: {mse}')
print(f'R2 Score: {r2}')
```

**Explications** :
- `LinearRegression()` crée un modèle de régression linéaire.
- `model.fit(X_train, y_train)` entraîne le modèle en utilisant les données d’entraînement.
- `model.predict(X_test)` effectue des prédictions sur l’ensemble de test.
- `mean_squared_error()` calcule l'erreur quadratique moyenne, une mesure de la différence entre les prédictions et les valeurs réelles.
- `r2_score()` calcule le coefficient de détermination \( R^2 \), qui évalue la qualité du modèle.

---

## 5. Prédiction des prix manquants

Enfin, les dernières lignes du dataset n’ont pas de prix (`price`), et il est demandé de prédire ces valeurs en utilisant le modèle construit.

```python
# Prédire les prix des maisons sans prix
missing_data = data[data['price'].isna()]
X_missing = missing_data[['sqft_living', 'bedrooms', 'bathrooms', 'sqft_lot', 'floors', 'waterfront', 'view', 'condition', 'grade']]
y_missing_pred = model.predict(X_missing)

# Afficher les prédictions
missing_data['predicted_price'] = y_missing_pred
missing_data[['id', 'predicted_price']]
```

**Explications** :
- `data[data['price'].isna()]` sélectionne les lignes où le prix est manquant.
- `model.predict(X_missing)` prédit les prix de ces maisons.
- Les résultats sont ajoutés à un nouveau tableau avec l'ID et la prédiction du prix.

---

### Conclusion

L'objectif de cette fiche était de guider à travers une analyse de régression linéaire multiple appliquée à la prédiction des prix des maisons. Cet exercice permet d'explorer le dataset, de sélectionner les variables pertinentes, d'entraîner un modèle et de réaliser des prédictions sur des données manquantes.

Il est essentiel de toujours vérifier les performances du modèle avec des métriques comme le score R² afin d'éviter le surapprentissage (overfitting) et garantir une prédiction fiable sur de nouvelles données.

---

## Ressources
- [Documentation scikit-learn](https://scikit-learn.org/stable/)
- [Matrice de corrélation en Python - Seaborn](https://seaborn.pydata.org/generated/seaborn.heatmap.html)
