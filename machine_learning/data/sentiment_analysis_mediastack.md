Voici une fiche pédagogique sur l'utilisation de l'API *mediastack* pour récupérer des articles de presse, analyser les données et créer des visualisations. Ce projet inclut également un travail de nettoyage de texte, l'analyse des sentiments et la création de nuages de mots.

---

# **Analyse des sentiments à partir des articles de presse via l'API Mediastack**

### **1. Introduction**
L'API *mediastack* permet de récupérer des articles de presse à partir de différentes sources. Cette API est gratuite et limite l'accès à 500 requêtes par mois. En utilisant cette API, nous pouvons créer un tableau avec les articles récupérés, faire des analyses statistiques et des visualisations, comme des nuages de mots, tout en excluant les mots vides (stopwords).

### **2. Préparation de l'environnement**

Avant d'utiliser l'API, tu dois t'inscrire sur [mediastack](https://mediastack.com/) pour obtenir une clé API gratuite. Cette clé te permettra de faire des requêtes.

### **3. Installation des bibliothèques nécessaires**
```bash
pip install requests pandas matplotlib wordcloud stop_words spacy
```

### **4. Code pour récupérer et analyser les articles**

#### **a. Importation des bibliothèques**
```python
import requests
import pandas as pd
import matplotlib.pyplot as plt
from datetime import datetime
from wordcloud import WordCloud
from stop_words import get_stop_words
import spacy
from collections import defaultdict
```

#### **b. Définition de la clé API et des paramètres**
```python
API_KEY = "a467a013b407850f200694a07dba3d63"
mots_cles = "ministre"  # Choisir les mots-clés pour la recherche
params = {
    "access_key": API_KEY,
    "keywords": mots_cles,
    "languages": "fr",
    "countries": "fr",
    "sources": "-franceantilles",
    "limit": 100,
    "offset": 0,
}
url = "http://api.mediastack.com/v1/news"
```

#### **c. Récupération des articles**
Nous allons utiliser une boucle pour récupérer plusieurs centaines d'articles :
```python
all_articles = []
for _ in range(5):
    response = requests.get(url, params=params)
    data = response.json()
    all_articles.extend(data["data"])
    params["offset"] += 100
```

#### **d. Création d'un DataFrame avec les articles récupérés**
```python
df = pd.DataFrame(all_articles)
df = df[['source', 'title', 'description', 'url', 'image', 'category', 'language', 'country', 'published_at']]
df.sample(3)
```

#### **e. Calcul des statistiques clés**
```python
print(f"Nombre total d'articles: {len(df)}")
print(f"Nombre de sources uniques: {df['source'].nunique()}")
print(f"Nombre de pays uniques: {df['country'].nunique()}")
print(f"Nombre de catégories uniques: {df['category'].nunique()}")
```

#### **f. Conversion des dates**
```python
df['published_at'] = pd.to_datetime(df['published_at'])
oldest_date = df['published_at'].min().strftime('%d/%m/%Y')
newest_date = df['published_at'].max().strftime('%d/%m/%Y')
print(f"Article le plus ancien: {oldest_date}")
print(f"Article le plus récent: {newest_date}")
```

### **5. Visualisation des données**

#### **a. Nombre d'articles par source**
```python
source_counts = df['source'].value_counts()
plt.figure(figsize=(10, 6))
source_counts.plot(kind='bar')
plt.xlabel('Source')
plt.ylabel("Nombre d'articles")
plt.title("Nombre d'articles par source")
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()
```

#### **b. Nombre d'articles par pays**
```python
source_counts = df['country'].value_counts()
plt.figure(figsize=(10, 6))
source_counts.plot(kind='bar')
plt.xlabel('Pays')
plt.ylabel('Nombre d\'articles')
plt.title('Nombre d\'articles par pays')
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()
```

#### **c. Nombre d'articles par catégorie**
```python
source_counts = df['category'].value_counts()
plt.figure(figsize=(10, 6))
source_counts.plot(kind='bar')
plt.xlabel('Catégories')
plt.ylabel('Nombre d\'articles')
plt.title('Nombre d\'articles par catégorie')
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()
```

#### **d. Création d'un nuage de mots (Titres et Descriptions)**
```python
all_titles = ' '.join(df['title'])
all_descriptions = ' '.join(df['description'])

wordcloud_titles = WordCloud(width=800, height=400).generate(all_titles)
wordcloud_descriptions = WordCloud(width=800, height=400).generate(all_descriptions)

# Affichage des nuages de mots
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(20, 10))
ax1.imshow(wordcloud_titles, interpolation='bilinear')
ax1.set_title('Nuage de mots (Titres)')
ax1.axis('off')
ax2.imshow(wordcloud_descriptions, interpolation='bilinear')
ax2.set_title('Nuage de mots (Descriptions)')
ax2.axis('off')
plt.show()
```

### **6. Traitement des *stopwords* pour affiner le nuage de mots**
Les *stopwords* sont des mots qui sont souvent trop courants pour être utiles dans une analyse (comme "le", "la", "et", "à", etc.).

#### **a. Ajout de *stopwords* personnalisés**
```python
stopwords_persos = {mots_cles}
stopwords = set(get_stop_words('fr'))  # Stopwords en français

# Ajouter des stopwords supplémentaires
additional_stopwords = {...}  # Ajoute ici d'autres mots vides personnalisés

stopwords = stopwords.union(stopwords_persos)
stopwords = stopwords.union(additional_stopwords)
```

#### **b. Création du nuage de mots sans stopwords**
```python
wordcloud_titles = WordCloud(width=800, height=400, stopwords=stopwords).generate(all_titles)
wordcloud_descriptions = WordCloud(width=800, height=400, stopwords=stopwords).generate(all_descriptions)
wordcloud_combined = WordCloud(width=800, height=400, stopwords=stopwords).generate(all_titles + ' ' + all_descriptions)

# Affichage
plt.figure(figsize=(20, 10))
plt.imshow(wordcloud_combined, interpolation='bilinear')
plt.title('Nuage de mots (Titres + Descriptions)')
plt.axis('off')
plt.show()
```

### **7. Conclusion et analyse temporelle**

- L'analyse temporelle permet de comprendre comment les articles évoluent dans le temps, et quels sujets sont les plus abordés selon les périodes.
- Une analyse plus approfondie des sentiments pourrait être ajoutée avec un modèle de NLP pour déterminer l'opinion exprimée dans chaque article.

Avec ce code, tu peux déjà récupérer des articles, les analyser et créer des visualisations. Cette base te permettra de travailler davantage sur l'analyse de sentiments et d'affiner l'interprétation des données.

---

Cette approche te donne un bon point de départ pour une analyse sentimentale, tu peux aller plus loin en intégrant des outils comme *spaCy* ou *TextBlob* pour analyser les sentiments des textes récupérés.
