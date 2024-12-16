# NLP Partie 2 - Stemming & Lemmatizing

## Introduction

Dans le cadre du traitement du langage naturel (NLP), après avoir acquis les bases et exploré certaines statistiques sur du texte, il devient essentiel de nettoyer et de préparer les données pour les rendre utilisables par les modèles d'apprentissage automatique.

Le **stemming** et le **lemmatizing** sont deux techniques cruciales de prétraitement des données textuelles. Elles permettent d'uniformiser les mots en réduisant leur complexité grammaticale pour faciliter leur analyse et leur utilisation dans des algorithmes. Ces techniques sont souvent utilisées avant d'appliquer des modèles de machine learning supervisés ou non supervisés, en particulier lorsqu'il s'agit de classification de texte, d'analyse de sentiment, ou de recherche d'information.

L'objectif de cette fiche est d'expliquer ces deux techniques de manière détaillée, de vous permettre de les implémenter en Python, et de comprendre dans quel contexte chacune d'elles est utile.

## Objectifs

- **Comprendre le fonctionnement du stemming et du lemmatizing.**
- **Savoir comment implémenter ces techniques en Python.**
- **Choisir la méthode la plus appropriée en fonction du problème à résoudre.**

## Stemming

### Qu'est-ce que le Stemming ?

Le **stemming** consiste à réduire un mot à sa racine (ou base), ce qui permet de normaliser les différentes formes d'un mot en une seule forme. Par exemple, les mots "apples", "apple" et "apple's" peuvent être réduits à la racine "appl". Cette opération est particulièrement utile pour regrouper les variantes d'un mot qui partagent une signification similaire. Le stemming est une méthode de prétraitement brut qui ne tient pas compte du sens grammatical du mot, il coupe simplement les suffixes. 

### Exemple de Stemming en Python

Utiliser un stemmer est assez simple avec la bibliothèque **NLTK**. Nous allons ici utiliser le `SnowballStemmer`, qui prend en charge plusieurs langues, y compris l'anglais.

```python
from nltk.stem import SnowballStemmer
import nltk

# Phrase à analyser
sentence = "He likes apples"

# Initialisation du SnowballStemmer pour l'anglais
stem_en = SnowballStemmer("english")

# Application du stemming sur chaque token de la phrase
for word in nltk.word_tokenize(sentence):
    print(stem_en.stem(word))
```

**Explication du Code :**

1. On commence par importer le module `SnowballStemmer` de la bibliothèque NLTK et la fonction `word_tokenize` pour découper la phrase en mots.
2. Ensuite, on crée une instance du `SnowballStemmer` pour l'anglais.
3. Enfin, on applique le stemming sur chaque mot de la phrase en parcourant les tokens de la phrase.

**Résultat attendu :**

```
he
like
appl
```

Le stemming a réduit "likes" à "like" et "apples" à "appl", ce qui permet de traiter les différentes formes d'un même mot de manière unifiée.

### FreqDist après le Stemming

```python
sent_stem = [stem_en.stem(word) for word in nltk.word_tokenize(sentence)]
nltk.FreqDist(sent_stem)
```

**Résultat :**

```
FreqDist({'he': 1, 'like': 1, 'appl': 1})
```

La distribution des fréquences (FreqDist) montre que le mot "like" apparaît une fois, tout comme "he", et "appl" est compté comme une seule occurrence, ce qui permet de mieux analyser les données sans les variations de suffixes.

### Quand utiliser le Stemming ?

Le stemming est particulièrement utile lorsque l'on veut **uniformiser les mots** et éviter la duplication de données dans des modèles d'analyse de texte. Cependant, il peut parfois mener à des erreurs, notamment lorsqu'il découpe des mots de manière trop agressive sans tenir compte de leur contexte grammatical.

### Limitations

Le stemming peut entraîner des racines incorrectes, par exemple :
- "running" pourrait devenir "run", ce qui est correct.
- Mais "better" pourrait devenir "bet", ce qui n'a pas de sens.

## Lemmatizing

### Qu'est-ce que le Lemmatizing ?

Le **lemmatizing** est une technique plus avancée que le stemming. Contrairement au stemming, qui applique des règles fixes pour supprimer les suffixes, le lemmatizing utilise des règles linguistiques pour **trouver le lemme** d'un mot, c'est-à-dire sa forme canonique. Par exemple, le lemme de "running" est "run" et le lemme de "better" est "good".

Le lemmatizing conserve la signification du mot et peut être plus précis dans le traitement du texte.

### Exemple de Lemmatizing en Python

Nous allons utiliser la bibliothèque **spaCy**, une autre bibliothèque puissante pour le traitement du langage naturel. Elle offre un lemmatizer performant, basé sur des modèles linguistiques pré-entraînés.

```python
import spacy

# Chargement du modèle linguistique anglais
nlp = spacy.load('en_core_web_sm')

# Phrase à analyser
sentence = "You are better when I am well."

# Application du lemmatizing
sent_tokens = nlp(sentence)

# Affichage des lemmes
for token in sent_tokens:
    print(token.text, token.lemma_)
```

**Explication du Code :**

1. Le modèle linguistique **'en_core_web_sm'** est chargé à l'aide de spaCy, qui contient les règles nécessaires pour effectuer le lemmatizing.
2. Ensuite, la phrase est analysée avec `nlp()`, ce qui découpe le texte en tokens (mots).
3. On parcourt les tokens et affiche leur forme de base (lemme).

**Résultat attendu :**

```
You you
are be
better good
when when
I I
am be
well well
. .
```

Les mots "are" et "am" sont tous deux réduits à "be", et "better" est réduit à "good", ce qui est plus précis que le stemming.

### Quand utiliser le Lemmatizing ?

Le lemmatizing est utile lorsqu'il est nécessaire de **conserver la signification correcte des mots**, surtout dans des contextes où les variantes grammaticales peuvent changer le sens. Par exemple, dans des tâches de classification de texte ou d'analyse de sentiments, il est préférable de conserver les racines de mots qui respectent leur signification grammaticale.

### Limitations

Le lemmatizing nécessite une analyse plus complexe et dépend de modèles linguistiques qui peuvent être coûteux en termes de ressources pour des textes volumineux.

## Comparaison entre Stemming et Lemmatizing

| Technique      | Avantages                              | Inconvénients                                   | Cas d'utilisation                                      |
|----------------|----------------------------------------|------------------------------------------------|--------------------------------------------------------|
| **Stemming**   | Rapide, simple à mettre en œuvre.      | Peut entraîner des racines non significatives.  | Utilisation rapide de mots pour analyse de fréquence.  |
| **Lemmatizing**| Précis, conserve le sens grammatical.  | Plus lent, nécessite des ressources plus importantes. | Analyse de sentiments, classification de texte.        |

## Ressources

- [NLTK Documentation - SnowballStemmer](https://www.nltk.org/nltk_data/)
- [spaCy Documentation](https://spacy.io/)
- [Introduction au NLP avec Python - Partie 1 (GitHub)](https://github.com/moncompte/Tools-Tech/blob/main/NLP_Part1.md)

## Conclusion

Le stemming et le lemmatizing sont des techniques essentielles pour préparer les données textuelles en vue d'une analyse plus approfondie. Le stemming est plus rapide mais moins précis, tandis que le lemmatizing, bien que plus complexe, conserve une meilleure qualité de résultat. Selon l'application, il peut être nécessaire de choisir l'une ou l'autre technique, ou même de les combiner.
