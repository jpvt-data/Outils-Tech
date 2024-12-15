# Maîtriser KNN pour la recherche de similarités

## Introduction

L'algorithme des k plus proches voisins (k-NN) est couramment utilisé pour la classification et la régression, mais il peut également être appliqué à la recherche de similarités. Dans ce cadre, il permet de trouver des éléments similaires dans un ensemble de données. Cette fiche technique explore en détail l'utilisation de k-NN pour la recherche de similarités, en mettant l'accent sur les distances et leur impact sur les résultats. L'objectif est d'appliquer cette technique à des cas concrets comme la recommandation de produits similaires ou l'identification d'objets proches dans une base de données.

## Objectifs

À la fin de cette fiche, l'utilisateur sera capable de :

- Comprendre le fonctionnement de l'algorithme k-NN pour la recherche de similarités.
- Choisir et appliquer des métriques de distance adaptées à ses données.
- Utiliser la classe `NearestNeighbors` de scikit-learn pour trouver les voisins les plus proches.
- Visualiser et interpréter les résultats de la recherche de similarités.
- Appliquer ces connaissances à des exemples concrets, tels que la recherche de fruits similaires.

---

## 1. Fondamentaux de k-NN

L'algorithme k-NN est basé sur la proximité des points dans un espace multidimensionnel. L'idée générale est que des objets proches les uns des autres dans cet espace sont susceptibles d'être similaires. 

L'algorithme suit les étapes suivantes :
1. Pour un point donné, calculer sa distance par rapport à tous les autres points.
2. Sélectionner les **k** points les plus proches (les voisins).
3. Utiliser ces **k** voisins pour effectuer une tâche (par exemple, classification, recherche de similarités).

### Exemple : Recherche de livres similaires

Supposons qu'une bibliothèque possède plusieurs livres caractérisés par leur nombre de pages et leur année de publication. Si l'on veut trouver les livres les plus similaires à un livre cible, on appliquera k-NN pour déterminer les livres les plus proches.

```python
import numpy as np
import matplotlib.pyplot as plt

# Données des livres (nombre de pages, année de publication)
livres = np.array([[200, 1990], [150, 2005], [300, 1985], [250, 2000],
                   [180, 2010], [220, 1995], [280, 2015], [190, 1980]])

# Livre cible
livre_cible = np.array([230, 2005])

# Visualisation
plt.figure(figsize=(10, 6))
plt.scatter(livres[:, 0], livres[:, 1], c='blue', label='Livres')
plt.scatter(livre_cible[0], livre_cible[1], c='red', s=100, label='Livre cible')
plt.xlabel('Nombre de pages')
plt.ylabel('Année de publication')
plt.title('Représentation des livres')
plt.legend()
plt.show()
```

### Explication

- Chaque point bleu représente un livre avec deux caractéristiques : le nombre de pages et l'année de publication.
- Le point rouge est le livre cible pour lequel on cherche des livres similaires.

---

## 2. L'importante notion de distance

Le cœur de l'algorithme k-NN réside dans la notion de distance entre deux points. La distance quantifie à quel point deux éléments sont similaires. Plus la distance est faible, plus les éléments sont considérés comme similaires.

### 2.1 Distance Euclidienne

La distance euclidienne est la distance "en ligne droite" entre deux points dans un espace multidimensionnel. Pour deux points **A(x₁, y₁)** et **B(x₂, y₂)**, la distance euclidienne est donnée par :

\[
d = \sqrt{(x₂ - x₁)² + (y₂ - y₁)²}
\]

#### Exemple avec les livres

```python
def distance_euclidienne(point1, point2):
    return np.sqrt(np.sum((point1 - point2) ** 2))

# Calculer la distance entre le livre cible et tous les autres
distances = [distance_euclidienne(livre_cible, livre) for livre in livres]
k = 3  # Trouver les 3 livres les plus proches
indices_plus_proches = np.argsort(distances)[:k]

print("Les 3 livres les plus similaires (indice, distance) :")
for i in indices_plus_proches:
    print(f"Livre {i}: distance = {distances[i]:.2f}")
```

### 2.2 Distance de Manhattan

La distance de Manhattan est la somme des différences absolues entre les coordonnées. Elle est utile lorsque les données sont organisées en grille, comme les rues de Manhattan, d'où son nom.

\[
d = |x₂₁ - x₁₁| + |x₂₂ - x₁₂| + ... + |x₂ₙ - x₁ₙ|
\]

#### Exemple avec les livres

```python
def distance_manhattan(point1, point2):
    return np.sum(np.abs(point1 - point2))

# Calculer la distance de Manhattan entre le livre cible et tous les autres
distances_manhattan = [distance_manhattan(livre_cible, livre) for livre in livres]
indices_plus_proches_manhattan = np.argsort(distances_manhattan)[:k]

print("\nLes 3 livres les plus similaires (distance de Manhattan) :")
for i in indices_plus_proches_manhattan:
    print(f"Livre {i}: distance = {distances_manhattan[i]:.2f}")
```

---

## 3. k-NN en action : l'exemple des fruits

Imaginons une base de données contenant des fruits caractérisés par leur poids, leur taux de sucre et leur acidité. L'algorithme k-NN peut être utilisé pour trouver des fruits similaires.

### Étapes :

1. **Normalisation des données** : La normalisation est essentielle car k-NN est sensible aux échelles des caractéristiques. Sans normalisation, des caractéristiques comme le poids domineront le calcul des distances.

```python
import pandas as pd
from sklearn.preprocessing import StandardScaler

# Données des fruits
fruits_data = [
    {"nom": "Pomme", "poids": 150, "sucre": 10, "acidite": 3},
    {"nom": "Poire", "poids": 170, "sucre": 9, "acidite": 4},
    {"nom": "Orange", "poids": 160, "sucre": 8, "acidite": 7},
    {"nom": "Citron", "poids": 100, "sucre": 2, "acidite": 9},
    {"nom": "Fraise", "poids": 20, "sucre": 7, "acidite": 5},
    {"nom": "Banane", "poids": 120, "sucre": 12, "acidite": 2},
    {"nom": "Ananas", "poids": 1000, "sucre": 13, "acidite": 6},
    {"nom": "Cerise", "poids": 8, "sucre": 8, "acidite": 4}
]

df_fruits = pd.DataFrame(fruits_data)

# Normalisation
scaler = StandardScaler()
X_scaled = scaler.fit_transform(df_fruits[['poids', 'sucre', 'acidite']])

print("Données normalisées :")
print(pd.DataFrame(X_scaled, columns=['poids', 'sucre', 'acidite'], index=df_fruits['nom']))
```

2. **Utilisation de `NearestNeighbors`** : Cette classe permet de trouver les voisins les plus proches dans les données normalisées.

```python
from sklearn.neighbors import NearestNeighbors

# Création du modèle
nn = NearestNeighbors(n_neighbors=3, metric='euclidean')
nn.fit(X_scaled)

# Trouver les voisins de la pomme
pomme_index = df_fruits[df_fruits['nom'] == 'Pomme'].index[0]
distances, indices = nn.kneighbors(X_scaled[pomme_index].reshape(1, -1))

print("\nFruits les plus similaires à une pomme:")
for distance, index in zip(distances[0][1:], indices[0][1:]):  # Exclure la pomme elle-même
    print(f"{df_fruits['nom'].iloc[index]} (Distance: {distance:.2f})")
```

---

## 4. Visualisation des résultats

Afin de mieux comprendre les résultats, une visualisation en 2D des données peut être réalisée grâce à l'Analyse en Composantes Principales (PCA).

```python
from sklearn.decomposition import PCA
import matplotlib.pyplot as plt

# Réduction à 2 dimensions avec PCA
pca = PCA(n_components=2)
X_pca = pca.fit_transform(X_scaled)

# Visualisation
plt.figure(figsize=(12, 8))
plt.scatter(X_pca[:, 0], X_pca[:, 1], c='blue')

for i, fruit in enumerate(df_fruits['nom']):
    plt.annotate(fruit, (X_pca[i, 0], X_pca[i, 1]))

# Mettre en évidence la pomme et ses voisins
plt.scatter(X_pca[pomme_index, 0], X_pca[pomme_index, 1], c='red', s=100)
for index in indices[0][1:]:
    plt.scatter(X_pca[index, 0], X_pca[index, 1], c='green', s=100)

plt.title("Visualisation des fruits et des plus proches voisins de la pomme")
plt.show()
```

---

## 5. Considérations avancées

### 5.1 Choix de la métrique de distance

Le choix de la métrique de distance affecte directement la performance de l'algorithme. Voici quelques exemples de métriques que l'on peut utiliser avec `NearestNeighbors` :

```python
for metric in ['euclidean', 'manhattan', 'chebyshev']:
    nn = NearestNeighbors(n_neighbors=3, metric=metric)
    nn.fit(X_scaled)
    distances, indices = nn.kneighbors(X_scaled[pomme_index].reshape(1, -1))

    print(f"\nFruits les plus similaires à une pomme (metric={metric}):")
    for distance, index in zip(distances[0][1:], indices[0][1:]):
        print(f"{df_fruits['nom'].iloc[index]} (Distance: {distance:.2f})")
```

### 5.2 Recherche de voisins dans un rayon

Parfois, au lieu de spécifier un nombre fixe de voisins, il est préférable de trouver tous les voisins dans un certain rayon. Voici comment procéder :

```python
# Trouver les voisins dans un rayon de 1.5
nn_radius = NearestNeighbors(radius=1.5, metric='euclidean')
nn_radius.fit(X_scaled)



distances, indices = nn_radius.radius_neighbors(X_scaled[pomme_index].reshape(1, -1))

print("\nFruits dans un rayon de 1.5 autour de la pomme:")
for distance, index in zip(distances[0], indices[0]):
    print(f"{df_fruits['nom'].iloc[index]} (Distance: {distance:.2f})")
```

---

## Conclusion

L'algorithme k-NN pour la recherche de similarités est un outil puissant et flexible, essentiel pour de nombreuses applications telles que les recommandations de produits, la recherche d'articles similaires, et bien plus encore. Bien que simple à implémenter, il est important de bien comprendre les métriques de distance et de normaliser les données avant de l'appliquer.
