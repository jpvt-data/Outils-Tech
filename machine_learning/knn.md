[⬅ Retour à Machine Learning](../README.md)

# Machine Learning - K-Nearest Neighbours - Classification

## Introduction à l'algorithme K-Nearest Neighbours (KNN)

L'algorithme K-Nearest Neighbours (KNN) est une méthode de machine learning supervisé utilisée principalement pour des problèmes de classification, bien qu'il puisse aussi être appliqué à la régression. Il repose sur un principe simple : pour classer une donnée, on regarde les "k" voisins les plus proches de cette donnée dans l'espace des caractéristiques, et la classe la plus fréquente parmi ces voisins est attribuée à la donnée à classer. On peut donc résumer cette méthode par la phrase : **"Dis-moi qui est ton voisin et je te dirai qui tu es"**.

## Objectifs

1. **Comprendre l'algorithme KNN et son utilisation pour la classification.**
2. **Apprendre à appliquer KNN avec la bibliothèque scikit-learn.**
3. **Explorer les métriques liées aux classifications, comme la matrice de confusion et les scores de précision.**

## KNN : Principe de Fonctionnement

### Apprentissage Supervisé vs Non Supervisé

Avant de plonger dans KNN, il est utile de comprendre la différence entre **l'apprentissage supervisé** et **l'apprentissage non supervisé** :
- **Apprentissage supervisé** : Le modèle apprend à partir d'un ensemble de données étiquetées (avec une variable cible y).
- **Apprentissage non supervisé** : Le modèle apprend à partir de données non étiquetées, sans variable cible.

Dans le cas de KNN, il s'agit d'un **apprentissage supervisé** où l'objectif est de prédire une classe en fonction des caractéristiques des voisins les plus proches.

### Comment ça marche ?

KNN est basé sur le concept de proximité des données dans un espace multidimensionnel. Le principal concept est de calculer la distance entre un point à classer et les autres points du jeu de données.

- **k** : Représente le nombre de voisins les plus proches utilisés pour la classification.
- **Distance** : La méthode la plus courante pour mesurer cette proximité est la **distance euclidienne**, mais d'autres distances comme la **distance de Manhattan** peuvent être utilisées selon le cas d'usage.

### Types de Problèmes
- **Classification** : Le modèle prédit une catégorie (exemple : chat ou chien).
- **Régression** : Le modèle prédit une valeur numérique.

Ici, nous nous concentrons sur l'application de KNN à un problème de **classification**.

## Paramètres et Fonctionnement avec scikit-learn

### Utilisation avec scikit-learn

Scikit-learn fournit une classe `KNeighborsClassifier` qui permet d'implémenter facilement l'algorithme KNN pour la classification.

Exemple d'utilisation en Python :

```python
from sklearn.neighbors import KNeighborsClassifier

# Création du modèle avec un nombre de voisins k=5
modelKNN = KNeighborsClassifier(n_neighbors=5)

# Entraînement du modèle avec des données d'apprentissage
modelKNN.fit(X_train, y_train)

# Prédiction sur les données test
y_pred = modelKNN.predict(X_test)
```

### Paramètres Importants

- **n_neighbors** : Détermine le nombre de voisins à considérer. Par défaut, il est fixé à 5.
  - Exemple : `modelKNN = KNeighborsClassifier(n_neighbors=7)`

- **weights** : Par défaut, chaque voisin a un poids égal. Si l'on veut que les voisins plus proches aient plus d'influence, on peut utiliser l'option `weights="distance"`, qui attribue un poids inversément proportionnel à la distance.
  - Exemple : `modelKNN = KNeighborsClassifier(weights="distance")`

### La distance

La **distance euclidienne** est la méthode la plus courante pour déterminer la proximité entre les points. Elle est calculée comme suit pour deux points \( p_1 \) et \( p_2 \) dans un espace \( d \)-dimensionnel :

\[
d(p_1, p_2) = \sqrt{\sum_{i=1}^{d}(p_{1i} - p_{2i})^2}
\]

### Métriques de Distance Alternatives

Bien que la distance euclidienne soit la plus utilisée, il existe d'autres métriques comme :
- **Distance de Manhattan** : Mesure la distance comme la somme des différences absolues des coordonnées.
- **Distance de Minkowski** : Généralisation de la distance euclidienne et de Manhattan.

Avec scikit-learn, la métrique peut être spécifiée via le paramètre `metric` et `p`.

## Préparation des Données

### Traitement des Variables Catégorielles

KNN nécessite des données numériques pour calculer les distances. Si vous avez des variables catégorielles, vous devez les transformer :

1. **Factorisation** : Transformation des catégories en valeurs numériques ordonnées. Cependant, cela peut induire des erreurs car KNN pourrait percevoir des relations ordonnées là où il n'y en a pas.
   
   Exemple :
   ```python
   df['animaux_nb'] = df['animaux'].factorize()[0]
   ```

2. **Encodage One-Hot (Get Dummies)** : Cette méthode crée des colonnes binaires pour chaque catégorie, évitant ainsi les problèmes d'ordonnancement.
   
   Exemple :
   ```python
   pd.get_dummies(df['animaux'])
   ```

## Métriques de Classification

L'évaluation des performances d'un modèle de classification se fait souvent à l'aide de la **matrice de confusion**, qui permet de mesurer les prédictions du modèle et leur précision.

### Matrice de Confusion

Une matrice de confusion résume les prédictions effectuées par le modèle par rapport aux vraies valeurs. Pour un problème binaire (chat/chien), elle peut ressembler à ceci :

|                    | Prédiction Chat | Prédiction Chien |
|--------------------|-----------------|------------------|
| **Vrai Chat**      | 5               | 5                |
| **Vrai Chien**     | 1               | 9                |

Où :
- **Vrai Positif (TP)** : Le modèle a correctement prédit un chat (5).
- **Faux Négatif (FN)** : Le modèle a prédit un chien alors que c'était un chat (5).
- **Faux Positif (FP)** : Le modèle a prédit un chat alors que c'était un chien (1).
- **Vrai Négatif (TN)** : Le modèle a correctement prédit un chien (9).

### Métriques Calculées à partir de la Matrice de Confusion

1. **Accuracy (Précision)** : Mesure la proportion de prédictions correctes.
   \[
   \text{Accuracy} = \frac{TP + TN}{\text{Total des prédictions}}
   \]

2. **Recall (Sensibilité)** : Proportion de vrais positifs parmi les éléments réellement positifs.
   \[
   \text{Recall} = \frac{TP}{TP + FN}
   \]

3. **F1-Score** : Moyenne harmonique de la précision et du recall. Il est utilisé quand il y a un déséquilibre dans les classes.

4. **Métrique de précision (Precision)** : Proportion de vrais positifs parmi les prédictions positives.
   \[
   \text{Precision} = \frac{TP}{TP + FP}
   \]

### Exemple d'implémentation de la Matrice de Confusion et des métriques avec scikit-learn

```python
from sklearn.metrics import confusion_matrix, accuracy_score

# Matrice de confusion
cm = confusion_matrix(y_test, y_pred)

# Précision (Accuracy)
accuracy = accuracy_score(y_test, y_pred)

print("Matrice de confusion :\n", cm)
print("Précision : ", accuracy)
```

## Conclusion

L'algorithme K-Nearest Neighbours est une méthode puissante et intuitive pour résoudre des problèmes de classification en machine learning. Il repose sur l'idée simple que les objets similaires sont souvent proches dans l'espace des caractéristiques. En utilisant scikit-learn, vous pouvez facilement appliquer KNN à vos données, ajuster les paramètres comme le nombre de voisins et la méthode de pondération, et évaluer les performances du modèle à l'aide de métriques adaptées comme la matrice de confusion, l'accuracy, le recall, et le F1-score.

[⬅ Retour à Machine Learning](../README.md)