# NLP 4 : Bag of Words

## Objectifs
- Comprendre le principe du **sentiment analysis** (analyse de sentiments)
- Découvrir la notion de **Bag of Words**
- Apprendre à réaliser un **Bag of Words** grâce à la bibliothèque **scikit-learn**

## Contexte et Introduction

L’analyse de texte est une discipline puissante utilisée dans de nombreux domaines, du marketing à la détection de fraude en passant par la gestion de la relation client. Le **sentiment analysis** fait partie des techniques d’analyse de texte les plus populaires. Il permet d'extraire et de classifier l’opinion ou l’émotion exprimée dans un texte. Que ce soit pour analyser les avis de clients sur un produit ou mesurer l’opinion publique à propos d’une personnalité politique, cette méthode s'avère indispensable.

Dans ce cadre, l’approche **Bag of Words (BoW)** est l'une des techniques de prétraitement les plus courantes pour transformer le texte brut en un format que les algorithmes de Machine Learning peuvent traiter. Elle permet de convertir un ensemble de documents textuels en une matrice de comptage des mots, permettant ainsi aux modèles de comprendre le contenu.

Cette fiche expliquera comment appliquer cette approche avec la bibliothèque **scikit-learn** et l'utiliser dans un cadre d'analyse de sentiments.

## Quand utiliser Bag of Words ?

L’approche **Bag of Words** est particulièrement utile dans les situations suivantes :
- Lorsque l’on souhaite analyser de grands ensembles de données textuelles pour en extraire des caractéristiques significatives.
- Pour les tâches de **classification supervisée**, comme la **sentiment analysis**.
- Lorsque les relations sémantiques ou contextuelles entre les mots ne sont pas aussi importantes que leur fréquence d’apparition.

## Processus de travail

L'objectif principal du **Bag of Words** est de convertir un corpus de texte en une représentation numérique sous forme de vecteurs, qui peuvent être utilisés par des algorithmes de Machine Learning. Le processus se divise en plusieurs étapes clés :
1. **Préparation du texte** : nettoyage, suppression des mots inutiles (stopwords), et éventuellement lemmatisation ou stemming.
2. **Tokenization** : découper le texte en unités de base (mots, phrases).
3. **Création du Bag of Words** : comptabilisation des occurrences des mots dans chaque document.
4. **Vectorisation** : transformation des mots en vecteurs de nombres.

### Exemple

Imaginons que tu travailles sur un dataset qui contient des avis de clients sur des restaurants. Tu souhaites prédire si un avis est **positif** ou **négatif** à l'aide d’un modèle de **Machine Learning supervisé**.

Voici un exemple de dataset avec des phrases d'avis clients :

| Index | Avis                          |
|-------|-------------------------------|
| 0     | J'adore ce restaurant !        |
| 1     | Pas mal mais trop cher.        |
| 2     | Un excellent repas.            |
| 3     | Très déçu, je ne reviendrai pas. |

L'objectif est de créer un **Bag of Words** à partir de ce corpus de texte pour ensuite entraîner un modèle de classification pour prédire si un avis est positif ou négatif.

### Étape 1 : Préparer les données et installer les bibliothèques

Avant de commencer, il faut installer la bibliothèque **scikit-learn** si elle n'est pas déjà installée. Pour ce faire, utilise la commande suivante dans un terminal :

```bash
pip install scikit-learn
```

Ensuite, nous allons importer les bibliothèques nécessaires pour travailler avec les données :

```python
import pandas as pd
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import MultinomialNB
from sklearn.metrics import accuracy_score
```

### Étape 2 : Créer un DataFrame avec les données

Imaginons que tu as déjà un jeu de données sous forme de **DataFrame** (un tableau de données) contenant les avis des clients.

```python
# Dataset d'exemple
data = {
    'avis': [
        "J'adore ce restaurant !", 
        "Pas mal mais trop cher.", 
        "Un excellent repas.", 
        "Très déçu, je ne reviendrai pas."
    ],
    'sentiment': ['positif', 'neutre', 'positif', 'négatif']
}

df = pd.DataFrame(data)
```

### Étape 3 : Tokenisation et création du Bag of Words

Maintenant, nous allons transformer ces avis textuels en une matrice de comptage de mots grâce à **CountVectorizer**. 

```python
# Création du CountVectorizer
vectorizer = CountVectorizer()

# Apprentissage sur le corpus d'avis
X = vectorizer.fit_transform(df['avis'])

# Afficher les mots présents dans le vocabulaire
print(vectorizer.get_feature_names_out())
```

Ce code génère la liste des mots qui apparaissent dans le corpus. Chaque mot devient une colonne dans une matrice où chaque ligne représente un document (un avis).

### Étape 4 : Transformation en une matrice de comptage (Bag of Words)

Lorsque **CountVectorizer** transforme le texte en Bag of Words, chaque document devient un vecteur de nombres représentant le nombre d’occurrences de chaque mot dans le texte.

```python
# Afficher la matrice creuse
print(X.toarray())
```

L’output pourrait ressembler à ceci :

```
[[1 1 0 1 1 0]
 [1 1 1 0 1 0]
 [1 0 0 1 1 1]
 [0 0 1 0 1 1]]
```

Cela signifie que dans le premier avis ("J'adore ce restaurant !"), le mot "restaurant" apparaît une fois, tout comme "j'adore", "ce", et "!", alors que d'autres mots du vocabulaire ne sont pas présents (d'où les 0).

### Étape 5 : Entraînement du modèle de Machine Learning

Une fois que le texte a été transformé en vecteurs numériques, nous pouvons utiliser ces données pour entraîner un modèle de classification, par exemple, un classificateur Naïve Bayes, qui est adapté pour ce genre de tâches.

Nous devons d'abord diviser les données en un **train set** et un **test set**, afin de pouvoir évaluer la performance de notre modèle.

```python
# Séparer les données en train et test
X_train, X_test, y_train, y_test = train_test_split(X, df['sentiment'], test_size=0.2, random_state=42)

# Entraîner le modèle
classifier = MultinomialNB()
classifier.fit(X_train, y_train)

# Prédire sur le test set
y_pred = classifier.predict(X_test)

# Évaluer le modèle
accuracy = accuracy_score(y_test, y_pred)
print(f"Accuracy: {accuracy * 100:.2f}%")
```

### Explications des étapes :

- **CountVectorizer** : transforme les avis en une représentation numérique.
- **MultinomialNB** : c'est un modèle de classification basé sur le théorème de Bayes, adapté aux données de type "comptage", comme les fréquences de mots.
- **train_test_split** : permet de diviser les données en un ensemble d’entraînement et un ensemble de test pour évaluer la performance du modèle.

### Conclusion

Le **Bag of Words** est une technique simple mais puissante qui permet de transformer des données textuelles en une représentation numérique exploitable pour les algorithmes de Machine Learning. Cette approche est largement utilisée dans des tâches telles que l’analyse de sentiments, la détection de spam, et la classification de textes en général.

## Ressources

- Documentation de **CountVectorizer** : [https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html)
- Introduction à l'analyse de texte : [Kaggle Text Analysis](https://www.kaggle.com/learn/intro-to-natural-language-processing)
