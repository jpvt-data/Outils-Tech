# NLP 5 – Utilisation de TF-IDF pour l'Analyse de Texte

## Contexte

L’objectif de cette fiche est de comprendre le principe de TF-IDF (Term Frequency-Inverse Document Frequency) et son utilité dans le prétraitement de texte, notamment pour des tâches comme la **classification de texte** ou la **détection de spam**. Ce calcul est souvent utilisé dans le **traitement du langage naturel (NLP)** pour extraire des caractéristiques importantes d'un corpus de texte.

### À quelle étape du projet utiliser TF-IDF ?

TF-IDF intervient principalement lors de l'extraction de caractéristiques pour des modèles de machine learning. Il est particulièrement utile après avoir effectué un nettoyage et une préparation de données, tels que **tokenization**, **lemmatisation** ou **stemming**. L’objectif est de convertir un ensemble de textes en une **matrice de caractéristiques numériques** que les algorithmes de machine learning peuvent traiter.

Les étapes typiques sont les suivantes :

1. Nettoyage des données textuelles (supprimer les mots inutiles, symboles, etc.).
2. Application de TF-IDF pour extraire les caractéristiques les plus significatives des textes.
3. Utilisation des vecteurs obtenus comme entrée pour un modèle de machine learning.

---

## Qu'est-ce que TF-IDF ?

**TF-IDF (Term Frequency - Inverse Document Frequency)** est une mesure statistique utilisée pour évaluer l'importance d'un mot dans un document au sein d'un corpus de textes. L’idée est de donner un poids plus élevé aux mots qui apparaissent fréquemment dans un document mais rarement dans les autres documents du corpus. Cela aide à identifier les termes les plus pertinents dans une tâche de classification, de clustering ou d'indexation de documents.

### Formule de calcul

Le calcul de TF-IDF se fait en deux étapes :

1. **TF (Term Frequency)** : La fréquence du terme dans un document donné.
   
   \[
   TF(t) = \frac{\text{Nombre d'occurrences du terme t dans le document}}{\text{Nombre total de termes dans le document}}
   \]

2. **IDF (Inverse Document Frequency)** : La fréquence inverse du terme dans l'ensemble du corpus de documents. Plus un terme apparaît dans peu de documents, plus il est important.

   \[
   IDF(t) = \log\left(\frac{N}{df(t)}\right)
   \]

   où :
   - \( N \) est le nombre total de documents dans le corpus.
   - \( df(t) \) est le nombre de documents contenant le terme \( t \).

Le score final de **TF-IDF** est simplement le produit de ces deux scores :

\[
\text{TF-IDF}(t) = TF(t) \times IDF(t)
\]

---

## Exemple Concret : Application du TF-IDF avec Scikit-learn

### Étape 1 : Importation des bibliothèques nécessaires

```python
from sklearn.feature_extraction.text import TfidfVectorizer
import pandas as pd
```

### Étape 2 : Création d'un jeu de données

Créons un DataFrame avec quelques phrases pour illustrer l'utilisation de TF-IDF.

```python
# Jeu de données d'exemple
donnees = {
    'sentence': [
        "It is good", 
        "It is not good", 
        "It is very good", 
        "It is bad"
    ]
}

df = pd.DataFrame(donnees)
```

### Étape 3 : Application de TF-IDF

Nous allons maintenant utiliser **TfidfVectorizer** de la bibliothèque Scikit-learn pour transformer ces phrases en une matrice de caractéristiques.

```python
# Initialisation du modèle TF-IDF
tfidf = TfidfVectorizer()

# Application du TF-IDF sur le corpus
tfidf_matrix = tfidf.fit_transform(df['sentence'])

# Convertir la matrice en DataFrame pour mieux visualiser les résultats
tfidf_df = pd.DataFrame(tfidf_matrix.toarray(), columns=tfidf.get_feature_names_out())
```

### Résultats

L'exécution du code ci-dessus produit une matrice de caractéristiques où chaque ligne correspond à une phrase et chaque colonne à un mot, avec le score TF-IDF de chaque mot dans chaque phrase.

Voici ce à quoi cela ressemble :

|     | bad   | good  | is    | it    | not   | very  |
|-----|-------|-------|-------|-------|-------|-------|
| 0   | 0.0   | 0.65  | 0.53  | 0.53  | 0.0   | 0.0   |
| 1   | 0.0   | 0.46  | 0.37  | 0.37  | 0.72  | 0.0   |
| 2   | 0.0   | 0.46  | 0.37  | 0.37  | 0.0   | 0.72  |
| 3   | 0.8   | 0.0   | 0.42  | 0.42  | 0.0   | 0.0   |

Explications :
- Le mot "it" est présent dans toutes les phrases, mais son score est relativement bas.
- Le mot "not" a un score élevé dans la phrase "It is not good" car il est présent uniquement dans cette phrase et donc est jugé plus pertinent dans ce contexte spécifique.

---

## Paramètres du `TfidfVectorizer`

Le modèle `TfidfVectorizer` de Scikit-learn offre plusieurs paramètres que l’on peut configurer pour affiner l'extraction des caractéristiques textuelles :

| Paramètre        | Description                                                      | Exemple                 |
|------------------|------------------------------------------------------------------|-------------------------|
| `lowercase`      | Convertir tous les mots en minuscules avant traitement.           | `True`                  |
| `stop_words`     | Filtrer les mots vides (stopwords) comme "le", "la", "de".        | `'english'`             |
| `ngram_range`    | Spécifier la longueur des n-grams à prendre en compte.            | `(1, 2)` pour des unigrams et bigrams |
| `max_features`   | Limiter le nombre de mots à retenir en fonction de la fréquence.  | `1000`                  |

Exemple avec `ngram_range` et `stop_words` :

```python
# Initialisation avec paramètres personnalisés
tfidf = TfidfVectorizer(stop_words='english', ngram_range=(1, 2))

# Application sur le corpus
tfidf_matrix = tfidf.fit_transform(df['sentence'])
```

---

## Cas d'Utilisation

Le TF-IDF est couramment utilisé pour des tâches comme :

- **Classification de texte** : Identifier à quelle catégorie un document appartient (par exemple, spam vs non-spam).
- **Clustering de documents** : Regrouper des documents similaires en utilisant des algorithmes comme k-means.
- **Système de recommandation** : Recommander des articles ou des produits similaires en fonction du contenu.

Exemple : **Détection de spam**

L’idée ici est de transformer des emails en vecteurs TF-IDF, puis de les alimenter dans un modèle de machine learning pour prédire si un email est un spam ou non.

---

## Liens et Ressources Complémentaires

1. **Documentation officielle de Scikit-learn sur TfidfVectorizer** :  
   [https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html)

2. **Vidéo explicative du modèle TF-IDF** (TV Machine Learning - Feature Extraction from Text) :  
   [https://www.youtube.com/watch?v=7YacOe4XwhY&list=PLIG2x2RJ_4LTF-IIu7-J3y_yg8LRe1WZq&index=3](https://www.youtube.com/watch?v=7YacOe4XwhY&list=PLIG2x2RJ_4LTF-IIu7-J3y_yg8LRe1WZq&index=3)

---

En résumé, TF-IDF est un outil puissant pour convertir des textes en données numériques exploitables pour les modèles de machine learning. Son efficacité réside dans la capacité à accorder plus d'importance aux termes significatifs tout en filtrant ceux qui sont trop courants.
