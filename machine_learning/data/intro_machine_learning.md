# Introduction au Machine Learning

## Contexte
Le Machine Learning (ou apprentissage automatique) est une discipline de l'intelligence artificielle qui consiste à donner aux ordinateurs la capacité d'apprendre à partir de données, sans être explicitement programmés. Cette technologie permet de résoudre des problèmes complexes en automatisant l'extraction d'informations et la prise de décision. Utilisé dans divers secteurs (santé, finance, marketing, etc.), il repose sur des algorithmes spécifiques et adaptés à différents types de données et de besoins.

Cette fiche fournit une introduction complète au Machine Learning, ses catégories principales et des exemples pratiques pour illustrer ses concepts clés.

## Objectifs
- Comprendre les fondements du Machine Learning
- Identifier les différentes catégories d'algorithmes
- Explorer des exemples pour illustrer les applications pratiques

## Catégories de Machine Learning
Les algorithmes de Machine Learning se divisent en quatre grandes catégories :

### 1. Apprentissage supervisé
Dans ce cadre, les données sont étiquetées, c'est-à-dire que chaque entrée est associée à une sortie connue. Le modèle apprend à généraliser des réponses à partir de ces données.

**Applications :**
- Prédire le prix de l'immobilier (régression)
- Classer des e-mails en spam ou non-spam (classification)

**Exemple :**
Prédire la consommation énergétique d'une maison en fonction de sa surface et du nombre d'habitants.

### 2. Apprentissage non supervisé
Les données ne sont pas étiquetées. L'objectif est de trouver des motifs ou des regroupements dans les données.

**Applications :**
- Segmentation de clients pour le marketing
- Analyse des tendances sur les réseaux sociaux

**Exemple :**
Identifier des groupes de clients ayant des comportements similaires basés sur leurs achats.

### 3. Apprentissage semi-supervisé
Une partie des données est étiquetée, et le reste est non étiqueté. Ce type d'apprentissage est utile lorsque l'étiquetage des données est coûteux ou complexe.

**Applications :**
- Identification de contenu inapproprié sur les plateformes en ligne

### 4. Apprentissage par renforcement
L'algorithme apprend par essais et erreurs en interagissant avec un environnement. Il reçoit des récompenses ou des punitions en fonction des actions qu'il entreprend.

**Applications :**
- Jeux vidéo (AlphaGo)
- Conduite autonome

**Exemple :**
Optimiser les mouvements d'un robot pour atteindre un objectif en minimisant les échecs.

## Concepts fondamentaux

### Différence entre régression et classification
- **Régression :** Prédire une valeur continue (ex. : prix, température).
- **Classification :** Assigner une étiquette à une donnée (ex. : chat ou chien).

**Exemple :**
- Régression : Prévoir les ventes d'un magasin pour le mois prochain.
- Classification : Identifier si un client est satisfait ou insatisfait à partir des avis en ligne.

### Corrélation vs Causalité
Une corrélation entre deux variables n'implique pas une relation de cause à effet. Toujours analyser les données sous un angle métier avant de conclure.

**Exemple :**
La hausse des ventes de crèmes glacées et des noyades peut être corrélée, mais le facteur causal commun est la température estivale.

## Outils et bibliothèques
- **Scikit-learn :** Bibliothèque pour implémenter des algorithmes standards de Machine Learning.
- **Pandas :** Manipulation et analyse des données tabulaires.
- **Seaborn et Matplotlib :** Visualisation de données.
- **NumPy :** Calculs numériques efficaces.

## Exemple pratique : Classification basique

```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score

# Charger les données Iris
iris = load_iris()
X = iris.data
y = iris.target

# Séparer les données en ensembles d'entraînement et de test
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Créer et entraîner le modèle
clf = RandomForestClassifier()
clf.fit(X_train, y_train)

# Prédire les résultats
predictions = clf.predict(X_test)

# Évaluer la précision
print("Précision :", accuracy_score(y_test, predictions))
```

Ce script charge un jeu de données connu (Iris), entraîne un modèle de classification, puis évalue ses performances.

## Ressources utiles
- [Scikit-learn Documentation](https://scikit-learn.org/stable/)
- [Cours Vidéo : Introduction au Machine Learning](https://www.youtube.com/watch?v=ukzFI9rgwfU)
- [Machine Learning Crash Course par Google](https://developers.google.com/machine-learning/crash-course)

## Conclusion
Le Machine Learning est un domaine vaste et puissant. Comprendre ses catégories et ses concepts fondamentaux est essentiel avant de plonger dans des algorithmes complexes. Cette fiche est une base pour explorer des applications pratiques et approfondir les connaissances.

