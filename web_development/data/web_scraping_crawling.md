# Web Scraping : Crawling

## Sommaire

1. Introduction : qu'est-ce que le crawling ?
2. Les grandes étapes
3. Application technique
   - Récupération des URL
   - Extraction des données : exemples concrets
   - Application à une liste d'éléments
4. Challenge
5. Conclusion

---

## 1. Introduction : qu'est-ce que le crawling ?

Le crawling est une technique de web scraping permettant de parcourir une page web pour collecter les liens qu'elle contient. Ensuite, ces liens sont à leur tour explorés pour extraire des informations d'intérêt. Ce processus permet de naviguer en profondeur dans une structure web pour récupérer des données organisées.

### Contexte d'utilisation

Le crawling est utile dans des cas tels que :

- La collecte d'informations à partir de listes ou de catalogues.
- L'extraction automatique de données découpées en plusieurs niveaux (comme des catégories et sous-catégories).
- L'analyse de grandes quantités de pages web reliées entre elles.

Dans cette fiche, un exemple concret est proposé pour récupérer des informations sur les Pokémon à partir de [Poképédia](https://www.pokepedia.fr).

---

## 2. Les grandes étapes

1. Faire du scraping sur une page principale pour extraire les URLs.
2. Parcourir chaque URL pour collecter les données associées.
3. Organiser les données dans une structure tabulaire (par exemple, un DataFrame).

La difficulté principale réside dans la gestion des éléments intermédiaires, tels que les URLs et les données extraites. Le format JSON ou un DataFrame peut être utilisé.

---

## 3. Application technique

### Récupération des URL

**Objectif :** Extraire les liens des Pokémon dans l'ordre du Pokédex.

```python
import requests
from bs4 import BeautifulSoup
import pandas as pd

# URL cible
url_principale = "https://www.pokepedia.fr/Liste_des_Pok%C3%A9mon_dans_l%27ordre_du_Pok%C3%A9dex_National"

# Requête HTTP
html = requests.get(url_principale)
soup = BeautifulSoup(html.text, 'html.parser')

# Extraction des liens
bloc_table = soup.find("table", {"class": "tableaustandard"})
liens = bloc_table.find_all("a")

# Création d'un DataFrame
urls_pokemon = pd.DataFrame({
    "nom": [lien.text for lien in liens],
    "lien": ["https://www.pokepedia.fr" + lien["href"] for lien in liens]
})

print(urls_pokemon.head())
```

### Extraction des données : exemples concrets

**Objectif :** Récupérer le type principal de chaque Pokémon à partir de sa page.

```python
def extraire_type(url):
    """Fonction pour extraire le type principal d'un Pokémon."""
    html = requests.get(url)
    soup = BeautifulSoup(html.text, 'html.parser')

    # Localisation du bloc contenant le type principal
    bloc_type = soup.find("table", {"class": "tableaustandard"})
    try:
        type_principal = bloc_type.find("a").text
    except AttributeError:
        type_principal = "Inconnu"
    
    return type_principal

# Test sur un exemple
url_exemple = urls_pokemon["lien"].iloc[0]
print(extraire_type(url_exemple))
```

### Application à une liste d'éléments

**Objectif :** Appliquer la fonction à tous les Pokémon et organiser les résultats dans un tableau.

```python
# Extraction des types pour chaque Pokémon
urls_pokemon["type_principal"] = urls_pokemon["lien"].apply(extraire_type)

# Aperçu des données
print(urls_pokemon.head())
```

---

## 4. Challenge

Modifier le script pour extraire d'autres informations, comme les statistiques de base (PV, Attaque, etc.) ou la génération à laquelle appartient chaque Pokémon.

### Exemple d'extraction des PV

```python
def extraire_pv(url):
    """Fonction pour extraire les PV d'un Pokémon."""
    html = requests.get(url)
    soup = BeautifulSoup(html.text, 'html.parser')

    # Localisation des PV
    try:
        bloc_stats = soup.find("table", {"class": "tableaustandard"})
        pv = bloc_stats.find_all("td")[1].text.strip()
    except (AttributeError, IndexError):
        pv = "Inconnu"

    return pv

# Ajout des PV au tableau
urls_pokemon["pv"] = urls_pokemon["lien"].apply(extraire_pv)

print(urls_pokemon.head())
```

---

## 5. Conclusion

Le crawling permet d'extraire des informations structurées à partir de sources web hiérarchiques. Avec des outils comme BeautifulSoup et Pandas, il est possible d'organiser les données efficacement et de les analyser. Ce processus est essentiel pour créer des datasets à partir de pages web complexes. Pour aller plus loin, explorer l'utilisation de bibliothèques comme Scrapy pour un crawling à grande échelle.

### Ressources utiles

- [Documentation BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
- [Poképédia](https://www.pokepedia.fr)
- [Tutoriel Pandas](https://pandas.pydata.org/docs/getting_started/index.html)
