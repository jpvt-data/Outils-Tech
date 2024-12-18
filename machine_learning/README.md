[⬅ Retour à Outils-Tech](../README.md)

# Machine Learning 🤖

Bienvenue dans la section **Machine Learning** !

Cette partie est dédiée à l'apprentissage du Machine Learning à travers des fiches techniques qui guideront à chaque étape : de l'introduction aux concepts clés, à la préparation des données, l'implémentation des algorithmes, jusqu'au déploiement de modèles.

---

## 🌟 Pourquoi apprendre le Machine Learning ?

Le Machine Learning permet aux systèmes d'apprendre à partir des données et de réaliser des prédictions sans programmation explicite pour chaque tâche. Il est aujourd'hui un pilier central dans des domaines comme :  
- Les recommandations personnalisées (Netflix, Spotify).  
- La prédiction et l'automatisation en entreprise.  
- La reconnaissance d’images, de texte ou de voix.  
- La détection de fraudes et d'anomalies.

---

## 📂 Organisation des fiches techniques

Les fiches sont organisées de manière logique pour progresser étape par étape, en commençant par les bases et en allant vers des concepts plus avancés. Voici le sommaire avec un accès direct à chaque fiche :

### **[Introduction au Machine Learning](./data/intro_machine_learning.md)**  
   Une introduction aux types d'apprentissage, à la fois supervisé, non supervisé et par renforcement. Ce fichier fournit une base solide pour bien démarrer.

### **[Préparation des données](./data/preparation_donnees.md)**  
   Avant de plonger dans les modèles, il est essentiel de bien préparer les données. Cette fiche guide à travers les étapes de nettoyage et de transformation.

### **[Séparation des données - Train/Test Split](./data/train_test_split.md)**  
   Apprendre à séparer les données en échantillons d'entraînement et de test pour évaluer la performance des modèles.

---

### **Natural Language Processing (NLP)**

- **[Introduction](./data/intro_nlp.md)**  
   Introduction au traitement du langage naturel (NLP) et ses applications en Machine Learning
- **[Stemming & Lemmatizing](./data/nlp_stemming_lemmatizing.md)**  
   Techniques de Stemming et Lemmatizing pour simplifier et normaliser le texte en NLP.
- **[WordCloud et Masque Image](./data/nlp.wordcloud.md)**  
   Visualiser la fréquence des mots dans un texte ou un corpus, dans un nyage personnalisable.
  
---

### **Modèles d'apprentissage supervisé**

Voici les principales méthodes d'apprentissage supervisé à explorer dans cette section :

- **[Régression Linéaire Simple](./data/regression_lineaire_simple.md)**  
  Introduction à la régression linéaire pour prédire une variable continue à partir d’une seule variable indépendante.

- **[Régression Linéaire Multiple](./data/regression_lineaire_multiple.md)**  
  Approfondissement de la régression linéaire avec plusieurs variables indépendantes.

- **[Régression - Cas pratique : Ventes de maisons](./data/regression_cas_pratique_ventes_maisons.md)**  
  Appliquer la régression linéaire dans un cas concret de prévision des prix des maisons.

- **[K-Nearest Neighbors (KNN)](./data/knn.md)**  
  Un algorithme simple et puissant pour la classification et la régression, très utilisé en apprentissage supervisé.

- **[KNN Avancé](./data/knn_avance.md)**  
  Approfondir l'algorithme KNN, avec des techniques avancées et des astuces pour améliorer ses performances.

---

### **Modèles d'apprentissage non supervisé**

Les modèles d'apprentissage non supervisé permettent de travailler avec des données non étiquetées. Voici quelques techniques populaires :

- **[K-Means Clustering](./data/kmeans_clustering.md)**  
  L'un des algorithmes de clustering les plus connus, utilisé pour regrouper des objets similaires.

- **[Clustering DBSCAN](./data/clustering_dbscan.md)**  
  DBSCAN est un algorithme de clustering basé sur la densité, particulièrement utile pour les données avec des formes irrégulières.

- **[Clustering Hiérarchique](./data/clustering_hierarchique.md)**  
  Cette méthode de clustering crée une hiérarchie de clusters, permettant une analyse plus approfondie des données.

---

### **Évaluation des modèles et Optimisation**

Une fois les modèles entraînés, il est crucial de les évaluer et d'optimiser leurs performances. Cette section fournit les outils nécessaires :

- **[Cross-Validation et Grid Search](./data/cross_validation_grid_search.md)**  
  Apprendre à valider les modèles avec la validation croisée et à trouver les meilleurs hyperparamètres grâce à la recherche par grille.

- **[Pipeline et Cross-Validation](./data/pipeline_cross_validation.md)**  
  Organiser le flux de travail avec un pipeline et utiliser la validation croisée pour évaluer les modèles de manière plus rigoureuse.

- **[Pipeline avec GridSearch et RandomizedSearch](./data/pipeline_gridsearch_randomized.md)**  
  Approfondir le pipeline avec des techniques avancées pour optimiser les hyperparamètres des modèles.

- **[Standardisation des données dans un pipeline](./data/pipeline_standardiser.md)**  
  Apprendre à standardiser les données dans le cadre du pipeline afin de mieux préparer les modèles.

- **[Pipeline de réduction de dimensions avec PCA](./data/pipeline_pca.md)**  
  Réduire les dimensions des données à l'aide de l'Analyse en Composantes Principales (PCA) pour améliorer les visualisations et les performances des modèles.

---

## 🔧 Bibliothèques et outils utilisés

Pour mettre en pratique ces concepts, utiliser principalement les outils suivants :

- **Python** 🐍 : Le langage principal pour l'implémentation des modèles.
- **Pandas** et **NumPy** : Pour la manipulation des données.
- **Scikit-learn** : Pour implémenter la plupart des algorithmes de Machine Learning.
- **TensorFlow** et **PyTorch** : Pour les modèles de Deep Learning.
- **Matplotlib** et **Seaborn** : Pour la visualisation des données et des résultats des modèles.

---

## 💡 Ressources utiles

Pour compléter l'apprentissage, voici quelques ressources utiles :

- [Documentation officielle Scikit-learn](https://scikit-learn.org/stable/)  
- [Cours Stanford ML (Andrew Ng)](https://www.coursera.org/learn/machine-learning)  
- [Kaggle](https://www.kaggle.com/) : Plateforme pour les compétitions et les ensembles de données.


[⬅ Retour à Outils-Tech](../README.md)
