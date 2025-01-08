[⬅ Page Précédente](../README.md)

# PCA - Analyse en Composantes Principales : Réduction de dimensions

## Contexte

L'augmentation des dimensions des données peut poser de nombreux problèmes en analyse de données. Visualiser, stocker ou traiter des ensembles de données multidimensionnelles peut devenir complexe et coûteux. L'Analyse en Composantes Principales (ACP) est une technique de machine learning non supervisée qui réduit les dimensions tout en préservant le maximum d'information possible.

## Objectifs

- Comprendre le concept de PCA.
- Appliquer une PCA pour réduire les dimensions d'un jeu de données avec Python.

## Pourquoi réduire les dimensions ?

La PCA permet de :

- **Simplifier les visualisations** : réduire à deux ou trois dimensions facilite l'analyse graphique.
- **Réduire les coûts** : moins de dimensions impliquent moins de stockage et de calculs.
- **Améliorer les performances des modèles** : en éliminant le bruit et les valeurs aberrantes.

### Cas d'utilisation

| Domaine                | Exemple d'utilisation                  |
|------------------------|-----------------------------------------|
| Marketing              | Segmentation des clients.             |
| Génie biomédical      | Analyse de gènes.                    |
| Finance                | Réduction de variables économiques.  |
| Informatique           | Compression de données.              |

## Concepts clés de la PCA

1. **Première composante principale** : maximiser la variance des données.
2. **Deuxième composante principale** : orthogonale à la première, capture la variance suivante.
3. **Réduction** : les composantes principales ayant une faible variance peuvent être ignorées.

## Implémentation pas à pas

### 1. Chargement des données

Utilisation du dataset **Iris** comme exemple.

```python
import pandas as pd
import seaborn as sns

X = sns.load_dataset("iris").iloc[:, :-1]
print(X.head())
```

### 2. Standardisation des données

Pourquoi ? Les différentes échelles des variables peuvent biaiser la PCA. La standardisation assure une moyenne de 0 et un écart-type de 1 pour chaque variable.

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
scaler.fit(X)
X_scaled = scaler.transform(X)
print(X_scaled[:5])
```

### 3. Entraîner le modèle PCA

Réduction à deux dimensions.

```python
from sklearn.decomposition import PCA

pca = PCA(n_components=2)
X_pca = pca.fit_transform(X_scaled)
print(X_pca[:5])
print(X_pca.shape)  # (150, 2)
```

### 4. Variance expliquée

Vérification de la quantité d'information conservée par chaque composante.

```python
print(pca.explained_variance_ratio_)
# [0.7296, 0.2285]
```

### 5. Visualisation des résultats

Affichage des points projetés dans le nouvel espace.

```python
import matplotlib.pyplot as plt

plt.scatter(X_pca[:, 0], X_pca[:, 1], c=sns.load_dataset("iris")["species"].astype('category').cat.codes)
plt.xlabel('Composante Principale 1')
plt.ylabel('Composante Principale 2')
plt.title('Projection ACP')
plt.show()
```

### 6. Réduction adaptative

Pour expliquer au moins 70 % de la variance :

```python
pca_adaptive = PCA(n_components=0.7)
pca_adaptive.fit(X_scaled)
X_pca_adaptive = pca_adaptive.transform(X_scaled)
print(X_pca_adaptive.shape)  # (150, 1)
```

## Interprétation des composantes

Les nouvelles dimensions ne correspondent plus directement aux variables initiales. Utiliser `pca.components_` pour identifier les coefficients associés à chaque composante principale.

```python
print(pca.components_)
```

## Ressources utiles

- [Vidéo explicative sur l'ACP (fr)](https://youtu.be/FTtzd31IAOw?t=1616)
- [Documentation officielle scikit-learn](https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html)

[⬅ Page Précédente](../README.md)