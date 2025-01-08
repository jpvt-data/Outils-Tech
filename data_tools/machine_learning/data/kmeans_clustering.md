[⬅ Page Précédente](../README.md)

# L'algorithme K-means pour le clustering

## Objectifs

L'algorithme **K-means** est une technique de **clustering** (regroupement) utilisée en apprentissage **non supervisé**. L'objectif de cette fiche est de :
1. Comprendre le principe du **clustering**.
2. Appréhender le fonctionnement de l'algorithme **K-means**.
3. Appliquer **K-means** dans un environnement Python à l'aide de la bibliothèque **scikit-learn**.

### Contexte et usage

Le **clustering** est une méthode qui permet de grouper des objets ou des données en fonction de leurs similarités. Contrairement à l'apprentissage supervisé, il ne nécessite pas de données étiquetées. Le but est de découvrir des structures cachées dans les données sans avoir d'indication préalable.

L'algorithme **K-means** est largement utilisé pour :
- La segmentation de clients dans le marketing.
- La classification d'images en fonction de leurs caractéristiques visuelles.
- La réduction de dimensions pour une analyse exploratoire des données.
  
### Quand utiliser K-means ?
- Lorsqu'on cherche à segmenter des données en groupes sans avoir d'informations sur les catégories existantes (ex. segmentation de clients, images similaires).
- Lorsqu'on souhaite organiser des données en groupes homogènes pour faciliter leur analyse.

### Étapes du K-means et explication des concepts

1. **Initialisation des centres des clusters**  
   L'algorithme commence par choisir **k** points comme centres de clusters. Ces centres peuvent être initialisés de manière aléatoire.

2. **Attribution des points aux clusters**  
   Chaque point de données est assigné au cluster dont le centre est le plus proche (basé sur la distance euclidienne).

3. **Mise à jour des centres**  
   Une fois que chaque point est attribué à un cluster, les centres des clusters sont recalculés en prenant la moyenne des points assignés à chaque cluster.

4. **Répétition**  
   Les étapes d'attribution et de mise à jour des centres sont répétées jusqu'à ce que les centres des clusters ne changent plus ou que le nombre maximal d'itérations soit atteint.

### Utilisation de K-means avec scikit-learn

#### Préparer les données

Le clustering K-means est sensible à l'échelle des données. Avant de lancer l'algorithme, il est recommandé de **normaliser les données** pour que chaque caractéristique contribue de manière égale au calcul de la distance.

```python
from sklearn.preprocessing import StandardScaler

# Exemple de jeu de données X
X = [[1, 2], [1, 4], [1, 0], [10, 2], [10, 4], [10, 0]]

# Normalisation des données
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
```

#### Implémentation de l'algorithme K-means

Voici un exemple complet pour appliquer l'algorithme **K-means** à des données.

```python
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt

# Jeu de données (exemple)
X = [[1, 2], [1, 4], [1, 0], [10, 2], [10, 4], [10, 0]]

# Initialiser le modèle K-means
modelKM = KMeans(n_clusters=2, random_state=3)

# Apprentissage du modèle
modelKM.fit(X)

# Affichage des centres des clusters
print("Centres des clusters :")
print(modelKM.cluster_centers_)

# Affichage des labels de chaque point (cluster d'appartenance)
print("Labels (clusters d'appartenance) :")
print(modelKM.labels_)
```

### Explication du code :

- **KMeans(n_clusters=2, random_state=3)** : Crée un modèle K-means avec 2 clusters et une initialisation contrôlée avec `random_state=3` pour la reproductibilité.
- **modelKM.fit(X)** : Entraîne le modèle sur les données `X`.
- **modelKM.cluster_centers_** : Affiche les coordonnées des centres des clusters.
- **modelKM.labels_** : Affiche le cluster d'appartenance de chaque point de données.

### Visualisation des clusters

On peut également visualiser les résultats du clustering pour mieux comprendre la répartition des points et des clusters.

```python
plt.scatter(X_scaled[:, 0], X_scaled[:, 1], c=modelKM.labels_)
plt.scatter(modelKM.cluster_centers_[:, 0], modelKM.cluster_centers_[:, 1], c='red', marker='X')
plt.title("K-means clustering")
plt.show()
```

### Évaluation du modèle

#### Inertie
L'inertie mesure la compacité des clusters. Plus cette valeur est petite, plus les points d'un même cluster sont proches de leur centre.

```python
print("Inertie :")
print(modelKM.inertia_)
```

#### Méthode Elbow
La méthode **Elbow** permet de choisir le nombre optimal de clusters en traçant l'inertie pour différentes valeurs de **k**. Le "coude" du graphique indique le nombre optimal de clusters.

```python
inertie = []
for k in range(1, 11):
    modelKM = KMeans(n_clusters=k, random_state=3)
    modelKM.fit(X)
    inertie.append(modelKM.inertia_)

plt.plot(range(1, 11), inertie)
plt.title("Méthode Elbow")
plt.xlabel("Nombre de clusters")
plt.ylabel("Inertie")
plt.show()
```

#### Méthode Silhouette
Le score **Silhouette** évalue la qualité du clustering en mesurant la cohésion interne (comment un point est proche des points de son propre cluster) et la séparation (comment il est éloigné des points des autres clusters). Le score varie de -1 à 1, où 1 signifie une bonne séparation, 0 une ambiguïté, et -1 une mauvaise affectation.

```python
from sklearn.metrics import silhouette_score

for k in range(2, 9):
    modelKM = KMeans(n_clusters=k, random_state=3)
    modelKM.fit(X)
    print(f"Silhouette pour {k} clusters : {silhouette_score(X, modelKM.labels_)}")
```

### Résumé des concepts clés

| **Concept**              | **Explication**                                                                            |
|--------------------------|--------------------------------------------------------------------------------------------|
| **K-means**               | Algorithme de clustering qui regroupe les points en **k** clusters.                          |
| **Clustering**            | Méthode de regroupement non supervisée basée sur les similarités entre les données.        |
| **Inertie**               | Mesure de la dispersion interne des points d'un même cluster. Moins l'inertie est élevée, mieux c'est. |
| **Méthode Elbow**         | Méthode visuelle pour choisir le nombre optimal de clusters en observant l'inertie.        |
| **Score Silhouette**      | Mesure de la qualité du clustering. Plus le score est proche de 1, mieux les clusters sont définis. |

### Ressources supplémentaires
- [K-means with scikit-learn (GeeksforGeeks)](https://www.geeksforgeeks.org/k-means-clustering-in-python/)
- [K-means clustering using scikit-learn (heartbeat)](https://heartbeat.fritz.ai/k-means-clustering-using-sklearn-and-python-4a054d67b187)
- [Vidéo explicative du K-means](https://www.youtube.com/watch?v=4b5d3muPQmA)

Cette fiche présente une méthode de clustering puissante pour segmenter des données. Elle est essentielle pour toute personne débutant avec des algorithmes d'apprentissage non supervisé.

[⬅ Page Précédente](../README.md)