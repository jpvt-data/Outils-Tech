[⬅ Page Précédente](../README.md)

# Machine Learning - K-Nearest Neighbours (KNN) - Classification

## Introduction à l'algorithme K-Nearest Neighbours (KNN)

L'algorithme K-Nearest Neighbours (KNN) est une méthode de machine learning supervisé largement utilisée pour des problèmes de classification. KNN est basé sur un principe simple : lorsqu'un point de données doit être classé, il regarde les *k* voisins les plus proches dans l'espace des caractéristiques, et la classe la plus fréquente parmi ces voisins est attribuée. En résumé, **"Dis-moi qui sont tes voisins et je te dirai qui tu es"**.

---

## Objectifs

1. **Comprendre le principe et l'utilisation de KNN pour la classification.**
2. **Apprendre à appliquer KNN avec la bibliothèque scikit-learn.**
3. **Explorer les métriques de performance comme la matrice de confusion et les scores de précision.**

---

## KNN : Principe de Fonctionnement

### Apprentissage Supervisé vs Non Supervisé

- **Apprentissage supervisé** : Le modèle apprend à partir de données étiquetées avec une variable cible (y).
- **Apprentissage non supervisé** : Le modèle apprend à partir de données sans étiquettes de classe.

Dans le cas de KNN, c'est un **apprentissage supervisé** où l'objectif est de prédire une classe en fonction des voisins proches.

### Comment ça marche ?

KNN repose sur la proximité des données dans un espace multidimensionnel. Pour classer un point, on mesure la distance entre ce point et les autres dans l'ensemble de données.

- **k** : Nombre de voisins à considérer pour la classification.
- **Distance** : Méthode la plus courante : **distance euclidienne**, mais des alternatives comme la **distance de Manhattan** sont aussi possibles.

### Types de Problèmes

- **Classification** : Le modèle prédit une catégorie (ex : chat ou chien).
- **Régression** : Le modèle prédit une valeur numérique.

Nous nous concentrons ici sur **la classification**.

---

## Paramètres et Fonctionnement avec scikit-learn

### Utilisation avec scikit-learn

Scikit-learn facilite l'implémentation de KNN avec la classe `KNeighborsClassifier`.

Exemple d'utilisation en Python :

```python
from sklearn.neighbors import KNeighborsClassifier

# Création du modèle avec k=5 voisins
modelKNN = KNeighborsClassifier(n_neighbors=5)

# Entraînement du modèle avec les données d'entraînement
modelKNN.fit(X_train, y_train)

# Prédiction sur les données de test
y_pred = modelKNN.predict(X_test)
```

### Paramètres Importants

- **n_neighbors** : Nombre de voisins à considérer. Par défaut, c'est 5.
  - Exemple : `modelKNN = KNeighborsClassifier(n_neighbors=7)`
- **weights** : Si on souhaite que les voisins plus proches aient plus d'influence, on peut utiliser `weights="distance"`.
  - Exemple : `modelKNN = KNeighborsClassifier(weights="distance")`

### Métriques de Distance Alternatives

- **Distance de Manhattan** : Somme des différences absolues des coordonnées.
- **Distance de Minkowski** : Généralisation de la distance euclidienne et de Manhattan.

Avec scikit-learn, ces métriques peuvent être spécifiées via le paramètre `metric` et `p`.

---

## Préparation des Données

### Traitement des Variables Catégorielles

KNN nécessite des données numériques pour mesurer les distances. Pour transformer des variables catégorielles, deux approches courantes sont :

1. **Factorisation** : Transformation des catégories en valeurs numériques ordonnées. Attention, cela peut induire des relations erronées.
   ```python
   df['animaux_nb'] = df['animaux'].factorize()[0]
   ```

2. **Encodage One-Hot** : Création de colonnes binaires pour chaque catégorie, évitant les problèmes d'ordonnancement.
   ```python
   pd.get_dummies(df['animaux'])
   ```

---

## Métriques de Classification

### Matrice de Confusion

La **matrice de confusion** est utilisée pour évaluer les performances du modèle. Pour un problème binaire (ex : chat/chien), elle peut ressembler à ceci :

|                    | Prédiction Chat | Prédiction Chien |
|--------------------|-----------------|------------------|
| **Vrai Chat**      | 5               | 5                |
| **Vrai Chien**     | 1               | 9                |

### Métriques de Performance

- **Accuracy** : Proportion de prédictions correctes.
  \[
  \text{Accuracy} = \frac{TP + TN}{\text{Total des prédictions}}
  \]
  
- **Recall (Sensibilité)** : Proportion des vrais positifs parmi les éléments réellement positifs.
  \[
  \text{Recall} = \frac{TP}{TP + FN}
  \]

- **F1-Score** : Moyenne harmonique de la précision et du recall, utile quand les classes sont déséquilibrées.
  
- **Precision** : Proportion des vrais positifs parmi les prédictions positives.
  \[
  \text{Precision} = \frac{TP}{TP + FP}
  \]

---

## Exemple Pratique avec scikit-learn

Voici un exemple complet, avec calcul de la matrice de confusion et affichage des métriques de classification :

```python
from sklearn.metrics import confusion_matrix, accuracy_score, classification_report
import matplotlib.pyplot as plt
import seaborn as sns

# Matrice de confusion
cm = confusion_matrix(y_test, y_pred)

# Précision (Accuracy)
accuracy = accuracy_score(y_test, y_pred)

# Affichage de la matrice de confusion avec Seaborn
plt.figure(figsize=(6,4))
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues', xticklabels=["Chat", "Chien"], yticklabels=["Chat", "Chien"])
plt.title("Matrice de Confusion")
plt.xlabel("Prédictions")
plt.ylabel("Vraies Valeurs")
plt.show()

# Affichage des métriques
print("Précision : ", accuracy)
print("Rapport de classification : \n", classification_report(y_test, y_pred))
```

### Graphiques de Visualisation des Distances

Une visualisation utile dans un problème KNN est la distance entre les points. Voici un exemple de visualisation en 2D pour montrer comment KNN classe les points en fonction des voisins les plus proches :

```python
import numpy as np
import matplotlib.pyplot as plt

# Exemple de points en 2D
X = np.random.rand(10, 2)
y = np.array([0, 1, 1, 0, 1, 0, 0, 1, 0, 1])

plt.scatter(X[:, 0], X[:, 1], c=y, cmap='coolwarm')
plt.title('Visualisation des points avec classification KNN')
plt.xlabel('Feature 1')
plt.ylabel('Feature 2')
plt.show()
```

---

## Conclusion

L'algorithme K-Nearest Neighbours est une méthode intuitive et puissante pour résoudre des problèmes de classification. Grâce à **scikit-learn**, son implémentation est simple, et il est facile d'ajuster des paramètres comme le nombre de voisins ou la méthode de pondération. La visualisation et l'évaluation de la performance à l'aide de la matrice de confusion et des métriques comme l'accuracy et le F1-score permettent de mesurer l'efficacité du modèle.


[⬅ Retour à Machine Learning](../README.md)

[⬅ Page Précédente](../README.md)