# Pipeline de Machine Learning - Standardiser vos données

## Objectifs
- Comprendre le concept de normalisation (ou standardisation) des données dans le contexte du machine learning.
- Améliorer les performances des modèles de machine learning grâce à la normalisation des données.

## Pourquoi normaliser les données ?

La normalisation est une étape clé dans le prétraitement des données pour les algorithmes de machine learning, particulièrement pour ceux basés sur des distances, comme le KNN (k-nearest neighbors). En effet, les algorithmes peuvent donner des résultats erronés si les données sont sur des échelles différentes. Examinons un exemple simple pour comprendre le problème.

### Exemple concret

Imaginons que nous avons deux types de fruits : des tomates et des fraises. Nous connaissons la taille (en centimètres) et le poids (en grammes) de chaque fruit. Nous venons de mesurer deux nouveaux fruits et nous devons les classer en tant que tomate ou fraise. Pour cela, nous appliquons l'algorithme KNN (k-nearest neighbors), qui classe les objets en fonction de leur proximité dans l'espace des caractéristiques.

Cependant, nos données de taille et de poids ont des échelles très différentes. La taille des fruits varie généralement de quelques centimètres, tandis que le poids peut varier de dizaines de grammes. Si l'on trace un graphique de ces données, les échelles différentes rendent les distances moins fiables pour classer les fruits.

#### Problème d'échelle

Voici un graphique trompeur qui représente la distance entre les fruits et les nouveaux fruits :

- L'axe vertical représente la taille en centimètres.
- L'axe horizontal représente le poids en grammes.

Sur ce graphique, les distances entre les points peuvent sembler similaires, mais ce n'est pas le cas à cause des échelles différentes.

#### Changement d'échelle

Si on ajuste les axes pour qu'ils aient la même échelle (en utilisant la normalisation), le graphique ressemblera à ceci :

À ce moment-là, il devient beaucoup plus facile de distinguer que le **New_fruit_1** est probablement une tomate et le **New_fruit_2** une fraise.

#### Problème d'unité

Maintenant, imaginez que nous mesurons le poids en "onces" (l'unité impériale britannique, où 1 gramme = 0,035274 oz) et la taille en millimètres. Les résultats des mesures seraient différents et affecteraient le classement. Pourtant, les fruits sont exactement les mêmes !

Cela démontre l'importance de standardiser les données avant d'utiliser des algorithmes de machine learning, afin de garantir que les différentes unités et échelles ne biaisent pas les résultats.

### La normalisation des données

La normalisation consiste à transformer les données pour qu'elles aient la même échelle. Cela permet de rendre les distances entre les observations plus cohérentes et d'éviter que certaines caractéristiques dominent les autres.

L'un des moyens les plus courants de normaliser les données est d'utiliser un **scaler**, tel que `StandardScaler` de la bibliothèque **scikit-learn**. Ce scaler transforme les données de manière à ce qu'elles aient une moyenne de 0 et un écart-type de 1. Cela permet de "centrer" les données autour de 0 et de les rendre comparables entre elles.

## Étapes de la normalisation avec `StandardScaler` en Python

Voici un exemple complet de l'application de la normalisation avec `StandardScaler`. Cette étape se fait généralement après avoir séparé les données en ensembles d'entraînement et de test.

### Étape 1 : Importation des bibliothèques nécessaires

```python
# Importation de la bibliothèque nécessaire
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import train_test_split
import pandas as pd
```

### Étape 2 : Préparation des données

Supposons que nous avons un DataFrame `df_fruits` avec les colonnes `weight_g` (poids en grammes), `size_cm` (taille en centimètres), et `fruit` (étiquette du fruit, soit "tomate", soit "fraise").

```python
# Exemple de données de fruits
df_fruits = pd.DataFrame({
    'weight_g': [200, 150, 180, 120, 250, 210],
    'size_cm': [10, 8, 9, 7, 11, 10],
    'fruit': ['tomato', 'strawberry', 'tomato', 'strawberry', 'tomato', 'tomato']
})

# Séparation des caractéristiques (features) et des étiquettes (labels)
X = df_fruits[['weight_g', 'size_cm']]  # caractéristiques (poids et taille)
y = df_fruits['fruit']  # étiquettes (fruit)
```

### Étape 3 : Séparation des données en ensembles d'entraînement et de test

```python
# Séparer les données en ensembles d'entraînement et de test
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
```

### Étape 4 : Création et ajustement du scaler

```python
# Création et ajustement du scaler sur l'ensemble d'entraînement
scaler = StandardScaler().fit(X_train)
```

### Étape 5 : Transformation des données

Une fois le scaler ajusté sur les données d'entraînement, on peut l'utiliser pour transformer à la fois les données d'entraînement et de test.

```python
# Transformation des données d'entraînement et de test
X_train_scaled = scaler.transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

### Étape 6 : Transformation inverse (si nécessaire)

Si vous avez besoin de retrouver les valeurs originales après la transformation, vous pouvez utiliser la méthode `inverse_transform()`.

```python
# Transformation inverse (retour aux valeurs originales)
X_train_new = scaler.inverse_transform(X_train_scaled)

# Vérification si la transformation inverse donne les données originales
print(X_train_new == X_train)  # Cela devrait retourner True
```

## Pourquoi cette étape est-elle importante ?

- **Améliorer les performances des modèles** : Les algorithmes de machine learning basés sur des distances (comme KNN, SVM, ou la régression logistique) dépendent de la mesure de la distance entre les points de données. Si les caractéristiques ont des échelles très différentes, certaines caractéristiques domineront les autres dans le calcul des distances. Cela peut fausser les prédictions du modèle.
  
- **Comparabilité** : Standardiser les données permet de les rendre comparables entre elles, quelle que soit l'unité de mesure initiale ou l'échelle des différentes caractéristiques.

## Applications du machine learning avec normalisation

- **Classification** : Les algorithmes comme KNN et SVM (Support Vector Machine) nécessitent une normalisation des données pour être efficaces.
- **Régression** : Les modèles de régression linéaire ou logistique bénéficient également d'une normalisation, notamment lorsqu'il existe des caractéristiques sur des échelles très variées.
- **Clustering** : Les algorithmes de clustering, comme K-means, se basent sur des distances pour regrouper des données similaires. Une normalisation est donc essentielle pour éviter des biais.

## Ressources

- [Khan Academy - Distribution Normale](https://www.khanacademy.org/math/probability/normal-distributions-a2)
- [Documentation officielle de `StandardScaler` sur scikit-learn](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html)
