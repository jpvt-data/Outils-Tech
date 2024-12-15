# Clustering avec DBSCAN (Density-based Spatial Clustering of Applications with Noise)

## Contexte et objectif
L'algorithme **DBSCAN** (Density-based Spatial Clustering of Applications with Noise) est une méthode de clustering, c'est-à-dire de regroupement de données, basée sur la densité des points dans un espace. Contrairement à d'autres algorithmes de clustering comme **K-Means**, DBSCAN n'exige pas de spécifier au préalable le nombre de clusters, et il est capable de gérer les points dits "bruit" ou outliers, qui ne peuvent pas être associés à un cluster. DBSCAN est particulièrement utile pour identifier des formes de clusters non sphériques, ce qui en fait un outil puissant pour l'analyse de données complexes.

Cette fiche technique explique pas à pas l'utilisation de DBSCAN, les paramètres à définir et comment l'appliquer dans un cas pratique. Elle s'adresse à des débutants en machine learning et fournit des exemples concrets à utiliser dans un environnement Python.

---

## Prérequis
Avant de commencer avec DBSCAN, il est important de comprendre quelques concepts fondamentaux du machine learning et du clustering :
- **Clustering** : C'est un processus non supervisé où l'objectif est de regrouper des données similaires.
- **Supervisé vs non supervisé** : DBSCAN est un algorithme **non supervisé**, car il n'utilise pas de labels prédéfinis pour former les clusters. Il se base uniquement sur la densité des points dans l'espace.

### Cas d'utilisation
DBSCAN est couramment utilisé pour :
- Identifier des anomalies ou des points de bruit dans des ensembles de données.
- Regrouper des points dans des configurations complexes et non linéaires, par exemple dans des données géospatiales ou des données avec des distributions irrégulières.

---

## Étapes pour utiliser DBSCAN

### 1. Comprendre les paramètres de DBSCAN
Avant d'appliquer l'algorithme, il est nécessaire de spécifier deux paramètres clés :
- **Epsilon (ε)** : Définit la distance maximale entre deux points pour qu'ils soient considérés comme voisins. Plus epsilon est grand, plus les points seront regroupés, même s'ils sont éloignés.
- **MinPts (minimum number of points)** : Le nombre minimum de points nécessaire pour qu'une zone soit considérée comme un cluster.

### 2. Application de DBSCAN avec Python

#### a. Installer les librairies nécessaires
Pour appliquer DBSCAN, il est nécessaire d'installer les librairies suivantes :
```bash
pip install numpy scikit-learn matplotlib
```

#### b. Importer les bibliothèques et charger les données
Dans cet exemple, nous utiliserons un jeu de données synthétique pour illustrer le fonctionnement de DBSCAN.

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.cluster import DBSCAN
from sklearn.datasets import make_blobs

# Générer des données simulées pour l'exemple
X, _ = make_blobs(n_samples=300, centers=4, random_state=42)

# Afficher les données initiales
plt.scatter(X[:, 0], X[:, 1], c='black', marker='o')
plt.title("Données avant DBSCAN")
plt.show()
```

**Explication** : Nous générons un ensemble de données avec 4 centres (clusters), puis nous affichons ces données.

#### c. Appliquer DBSCAN
Appliquons maintenant DBSCAN sur ces données.

```python
# Appliquer DBSCAN
dbscan = DBSCAN(eps=0.5, min_samples=5)
y_dbscan = dbscan.fit_predict(X)

# Afficher les résultats du clustering
plt.scatter(X[:, 0], X[:, 1], c=y_dbscan, cmap='viridis', marker='o')
plt.title("Résultat de DBSCAN")
plt.show()
```

**Explication** : La méthode `fit_predict` applique l'algorithme DBSCAN sur les données. Les résultats sont affichés avec des couleurs différentes pour chaque cluster. Les points considérés comme du bruit (c'est-à-dire les points qui ne peuvent pas être associés à un cluster) seront marqués par -1.

#### d. Analyser les résultats
Les points assignés à des clusters seront représentés par des numéros de cluster distincts, tandis que les points de bruit seront marqués par **-1**. Vous pouvez observer comment DBSCAN identifie des clusters de forme irrégulière et étiquette correctement les points de bruit.

**Exemple d'affichage** : Si vous obtenez une couleur pour chaque groupe, et une couleur différente pour les points de bruit, cela indique que DBSCAN a bien séparé les clusters et identifié les anomalies.

### 3. Choisir les bons paramètres
Le choix des paramètres `eps` et `min_samples` dépend fortement de vos données. Voici quelques conseils :
- Un **eps** trop petit pourrait mener à trop de points classés comme bruit.
- Un **eps** trop grand pourrait entraîner la fusion de clusters distincts.
- Le paramètre **min_samples** influence également la formation des clusters. Il est généralement conseillé de le définir comme étant supérieur ou égal à la dimension des données + 1.

### 4. Comparer DBSCAN avec d'autres algorithmes
DBSCAN présente plusieurs avantages par rapport à d'autres techniques de clustering comme **K-Means** :
- **Pas besoin de spécifier le nombre de clusters** à l'avance, ce qui est un inconvénient de K-Means.
- **Identification des points de bruit** : DBSCAN peut détecter les anomalies ou les points qui ne correspondent à aucun cluster.
- **Adapté aux formes de clusters irrégulières**, contrairement à K-Means qui crée des clusters de forme circulaire ou sphérique.

---

## Conclusion

DBSCAN est un algorithme puissant pour le clustering de données, surtout lorsque les données sont irrégulières et contiennent des points de bruit. En définissant correctement les paramètres `eps` et `min_samples`, vous pouvez obtenir des clusters significatifs, même dans des ensembles de données complexes.

---

## Ressources supplémentaires

1. [DBSCAN - All You Need To Know](https://www.kdnuggets.com/2020/04/dbscan-clustering-algorithm-machine-learning.html)
2. [DBSCAN - Visual Explanation](https://www.youtube.com/watch?v=5E097ZLE9Sg)
3. [DBSCAN - Explanation](https://www.youtube.com/watch?v=_A9Tq6mGtLI)

---

### Tableau récapitulatif des paramètres

| Paramètre        | Description                                             | Exemple de valeur     |
|------------------|---------------------------------------------------------|-----------------------|
| **eps**          | Distance maximale pour qu'un point soit dans le même cluster | 0.5                   |
| **min_samples**  | Nombre minimum de points pour former un cluster        | 5                     |
| **-1** (bruit)   | Points qui ne font pas partie d'un cluster             | Identifiés comme bruit|

---

### Cas d'utilisation de DBSCAN
- **Analyse de géolocalisation** : Identifier des zones géographiques à forte densité de points.
- **Détection d'anomalies** : Identifier des points de données qui s'écartent significativement du groupe général.
- **Segmentation de clients** : Identifier des groupes de clients ayant des comportements similaires, même si ces comportements ne sont pas linéaires.

