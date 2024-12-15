# Clustering Hiérarchique

Le **clustering hiérarchique** est une méthode d'analyse non supervisée utilisée pour regrouper des observations similaires dans des clusters. Contrairement à d'autres algorithmes de clustering, tels que le **K-Means**, où le nombre de clusters doit être spécifié à l'avance, le clustering hiérarchique ne nécessite pas de définir le nombre de clusters initialement. Cette méthode crée une structure arborescente appelée **dendrogramme**, qui permet de visualiser l'évolution du regroupement des observations et de déterminer, à partir de ce diagramme, combien de clusters sont nécessaires. Le clustering hiérarchique utilise une approche dite **bottom-up**, où les observations sont d'abord considérées comme des clusters individuels et sont successivement fusionnées pour former des clusters de plus en plus grands.

## Objectif

Le but de cette fiche est de détailler les étapes d'un **clustering hiérarchique** afin de permettre à un débutant de comprendre, d'implémenter et d'interpréter les résultats d'un tel modèle de clustering. À travers un exemple pratique, le lecteur pourra appliquer cette méthode dans un **notebook Jupyter** et obtenir une visualisation claire des clusters.

## Qu'est-ce que le Clustering Hiérarchique ?

### Principe du Clustering Hiérarchique

Le clustering hiérarchique repose sur l'idée de fusionner les observations les plus proches les unes des autres pour former des clusters. Ce processus est itératif et suit un schéma "bottom-up" (de bas en haut). Voici les grandes étapes de la méthode :

1. **Initialisation** : Chaque observation est considérée comme un cluster à part entière.
2. **Calcul des distances** : On mesure la distance entre chaque paire de clusters.
3. **Fusion des clusters** : Les deux clusters les plus proches (ayant la plus petite distance entre eux) sont fusionnés en un nouveau cluster.
4. **Répétition** : Ce processus de fusion continue jusqu'à ce qu'il ne reste qu'un seul cluster.
5. **Visualisation** : Un dendrogramme est généré pour visualiser l'ensemble des clusters et leurs relations.

### Mesure de la Similarité entre Clusters

Lors de la fusion des clusters, il est nécessaire de mesurer la similarité entre eux. Plusieurs méthodes peuvent être utilisées pour cela :

- **Linkage complet** : La distance entre deux clusters est définie par la distance maximale entre les points de chaque cluster.
- **Linkage simple** : La distance entre deux clusters est définie par la distance minimale entre les points de chaque cluster.
- **Linkage moyen** : La distance est la moyenne des distances entre tous les points des deux clusters.
- **Linkage par centroid** : La distance est calculée entre les centroïdes des deux clusters (les moyennes des points dans chaque cluster).

## Exemple Pratique en Python

Pour appliquer le clustering hiérarchique en Python, nous allons utiliser la bibliothèque **Scikit-learn** et la méthode **AgglomerativeClustering**. Ce code est conçu pour un exemple simple de clustering hiérarchique à partir d'un jeu de données fictif. L'objectif est de générer un dendrogramme et d'identifier le nombre de clusters.

### Étapes de l'implémentation :

1. **Importer les bibliothèques nécessaires**
2. **Créer un jeu de données d'exemple**
3. **Appliquer le clustering hiérarchique**
4. **Visualiser le dendrogramme**
5. **Observer et interpréter les résultats**

### Code Complet

```python
# Étape 1: Importation des bibliothèques nécessaires
import numpy as np
import matplotlib.pyplot as plt
from scipy.cluster.hierarchy import dendrogram, linkage
from sklearn.datasets import make_blobs
from sklearn.cluster import AgglomerativeClustering

# Étape 2: Création d'un jeu de données d'exemple (3 clusters)
X, y = make_blobs(n_samples=150, centers=3, cluster_std=0.60, random_state=0)

# Étape 3: Application du clustering hiérarchique
Z = linkage(X, method='ward')  # Méthode 'ward' minimise la variance au sein des clusters

# Étape 4: Visualisation du dendrogramme
plt.figure(figsize=(10, 7))
dendrogram(Z)
plt.title('Dendrogramme - Clustering Hiérarchique')
plt.xlabel('Index des observations')
plt.ylabel('Distance')
plt.show()

# Étape 5: Appliquer le clustering avec un nombre de clusters spécifié (par exemple 3)
model = AgglomerativeClustering(n_clusters=3)
y_predict = model.fit_predict(X)

# Affichage des clusters dans le graphique
plt.scatter(X[:, 0], X[:, 1], c=y_predict, cmap='viridis')
plt.title('Clusters obtenus par Clustering Hiérarchique')
plt.xlabel('Feature 1')
plt.ylabel('Feature 2')
plt.show()
```

### Explication du Code

1. **Importation des bibliothèques** : 
   - `numpy` est utilisé pour manipuler les données sous forme de matrices.
   - `matplotlib.pyplot` est utilisé pour afficher les graphiques.
   - `scipy.cluster.hierarchy` permet de calculer les distances et de générer le dendrogramme.
   - `sklearn.datasets.make_blobs` permet de créer un jeu de données artificiels avec 3 clusters.

2. **Création du jeu de données** : 
   - `make_blobs` génère un jeu de données avec trois centres (clusters) distincts. Cela permet de tester la capacité du modèle à identifier ces groupes.

3. **Clustering Hiérarchique** :
   - La fonction `linkage` effectue le calcul des distances entre les observations en utilisant la méthode 'ward'. Cette méthode est populaire pour le clustering hiérarchique, car elle minimise la variance intra-cluster.
   
4. **Visualisation du Dendrogramme** : 
   - Le dendrogramme est une représentation visuelle qui montre comment les observations sont fusionnées en clusters. Il permet de choisir un seuil de coupure, ce qui définit le nombre de clusters finaux.

5. **Appliquer le clustering et visualiser les résultats** :
   - `AgglomerativeClustering` applique le clustering en spécifiant le nombre de clusters voulu (ici, 3). Les résultats sont visualisés sous forme de nuage de points où chaque couleur correspond à un cluster.

### Résultat Attendu

Le dendrogramme montre un arbre où chaque division représente une fusion de clusters. Le code génère également un graphique avec les points de données colorés en fonction des clusters obtenus, permettant d'observer comment le modèle a segmenté les données en 3 groupes distincts.

## Quand Utiliser le Clustering Hiérarchique ?

Le clustering hiérarchique est particulièrement utile dans les cas suivants :

- Lorsque le nombre de clusters n'est pas connu à l'avance.
- Pour des visualisations détaillées de la structure des données via le dendrogramme.
- Lorsqu'il est nécessaire de travailler avec des données de petite à moyenne taille, car l'algorithme peut être coûteux en termes de temps de calcul sur de grands ensembles de données.

### Applications Pratiques

- **Analyse des clients** : Segmentation de clients dans le commerce de détail pour personnaliser les offres.
- **Génétique** : Regroupement de gènes ayant des comportements similaires.
- **Exploration de données** : Identification de groupes naturels dans un jeu de données sans avoir besoin de supervision.

## Conclusion

Le **clustering hiérarchique** est une technique de regroupement puissante pour explorer les données et visualiser la structure sous-jacente des observations. En utilisant la méthode agglomérative, il est possible de créer des clusters sans avoir à spécifier leur nombre initialement. Ce type d'algorithme est très utile lorsqu'il est important de comprendre comment les observations se regroupent et peut être appliqué dans divers domaines allant du marketing à la biologie.

### Ressources Complémentaires

- [Introduction au clustering hiérarchique](https://www.displayr.com/what-is-hierarchical-clustering/)
- [Utilisation du clustering hiérarchique avec Python, Scikit-learn, et Scipy](https://stackabuse.com/hierarchical-clustering-with-python-and-scikit-learn/)
- [Documentation de Scikit-learn sur le clustering hiérarchique](https://scikit-learn.org/stable/auto_examples/cluster/plot_agglomerative_dendrogram.html#sphx-glr-auto-examples-cluster-plot-agglomerative-dendrogram-py)
