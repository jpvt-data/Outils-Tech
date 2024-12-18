# Fonctions Types pour le Traitement de Texte en NLP

## Pré-requis : Importation des Bibliothèques et Téléchargements
Avant de commencer, s'assurer d'importer les bibliothèques nécessaires et de télécharger les données requises.

```python
# Importations nécessaires
import spacy
from nltk.corpus import stopwords
from wordcloud import WordCloud
import matplotlib.pyplot as plt
import string
from collections import Counter
from PIL import Image
import numpy as np

# Télécharger les ressources NLTK nécessaires
import nltk
nltk.download('stopwords')

# Charger le modèle Spacy pour le français
!python -m spacy download fr_core_news_sm

# Charger le modèle Spacy pour l'anglais (modifier la fonction)
!python -m spacy download en_core_web_sm
```

---

## 1. Fonction de Nettoyage de Texte

Cette fonction nettoie un texte en supprimant la ponctuation, les mots vides et en lemmatizant les mots.

```python
def nettoyer_texte(texte, langue='french'):
    """
    Nettoie un texte en supprimant la ponctuation, les mots vides et en appliquant la lemmatisation.

    Args:
        texte (str): Le texte à nettoyer.
        langue (str): La langue pour les stopwords (par défaut 'french').

    Returns:
        list: Une liste de mots nettoyés.
    """
    # Charger le modèle Spacy
    nlp = spacy.load('fr_core_news_sm')

    # Charger les stopwords
    stop_words = set(stopwords.words(langue))

    # Suppression de la ponctuation
    trans = str.maketrans('', '', string.punctuation)
    texte = texte.translate(trans)

    # Tokenisation et lemmatisation
    doc = nlp(texte)
    tokens_clean = [token.lemma_.lower() for token in doc if token.text.lower() not in stop_words and not token.is_punct and len(token) > 2]

    return tokens_clean
```

---

## 2. Fonction de Calcul de Fréquence de Mots

Cette fonction calcule la fréquence des mots dans une liste de mots nettoyés.

```python
def calculer_frequence(mots):
    """
    Calcule la fréquence des mots dans une liste.

    Args:
        mots (list): Liste de mots.

    Returns:
        dict: Un dictionnaire contenant les mots et leur fréquence.
    """
    return dict(Counter(mots))
```

---

## 3. Fonction pour Créer un Wordcloud

Cette fonction génère un wordcloud simple à partir d'un dictionnaire de fréquences de mots.

```python
def generer_wordcloud(frequences, largeur=800, hauteur=400):
    """
    Génère un wordcloud à partir d'un dictionnaire de fréquences.

    Args:
        frequences (dict): Dictionnaire de fréquences de mots.
        largeur (int): Largeur de l'image du wordcloud.
        hauteur (int): Hauteur de l'image du wordcloud.

    Returns:
        None: Affiche le wordcloud.
    """
    wordcloud = WordCloud(width=largeur, height=hauteur, background_color='white').generate_from_frequencies(frequences)

    plt.figure(figsize=(10, 5))
    plt.imshow(wordcloud, interpolation='bilinear')
    plt.axis('off')
    plt.show()
```

---

## 4. Fonction pour Créer un Wordcloud avec un Masque d'Image

Cette fonction génère un wordcloud en utilisant une image comme masque.

```python
def generer_wordcloud_avec_masque(frequences, chemin_image):
    """
    Génère un wordcloud en utilisant un masque d'image.

    Args:
        frequences (dict): Dictionnaire de fréquences de mots.
        chemin_image (str): Chemin vers l'image servant de masque.

    Returns:
        None: Affiche le wordcloud.
    """
    # Charger l'image et créer le masque
    masque = np.array(Image.open(chemin_image))

    # Générer le wordcloud
    wordcloud = WordCloud(mask=masque, background_color='white').generate_from_frequencies(frequences)

    plt.figure(figsize=(10, 10))
    plt.imshow(wordcloud, interpolation='bilinear')
    plt.axis('off')
    plt.show()
```

---

## Exemple d'Utilisation

```python
texte = """Cette édition des Misérables rend disponibles trois états de l'oeuvre: son texte, établi selon les règles classiques, son état au moment où Hugo en abandonne la rédaction en février 1848."""

# Nettoyage du texte
mots_nettoyes = nettoyer_texte(texte)

# Calcul des fréquences
frequences = calculer_frequence(mots_nettoyes)

# Générer un wordcloud simple
generer_wordcloud(frequences)

# Générer un wordcloud avec un masque
generer_wordcloud_avec_masque(frequences, 'chemin_vers_image.png')
