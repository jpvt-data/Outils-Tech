[⬅ Page Précédente](../README.md)

# Scraping de plusieurs pages web

## Introduction

Le web scraping consiste à extraire des données publiquement accessibles sur des sites web. Lorsqu’il s’agit d’analyser ou de collecter des informations issues de plusieurs pages, il devient essentiel d’implémenter un mécanisme permettant de naviguer automatiquement d’une page à une autre. Ce processus est connu sous le nom de crawling.

Cette fiche technique détaille les étapes pour scraper plusieurs pages d'un site web à l'aide de Python et de la bibliothèque BeautifulSoup. Elle inclut des exemples pratiques et adaptés pour illustrer le processus.

**Cas d’utilisation :** Récupération des annonces d’emploi sur un site comprenant plusieurs pages d’offres.

---

## Sommaire
1. [Prérequis et outils](#prerequis-et-outils)
2. [Scraping d’une page unique](#scraping-une-page)
3. [Crawling : Scraping de plusieurs pages](#crawling-pages-multiples)
4. [Exemple concret : Scraper les titres d’articles sur Poképedia](#exemple-concret)
5. [Précautions juridiques et bonnes pratiques](#precautions)
6. [Ressources](#ressources)

---

## 1. Prérequis et outils

### Bibliothèques nécessaires
- `requests` : Pour effectuer des requêtes HTTP et récupérer le contenu des pages web.
- `BeautifulSoup` (module `bs4`) : Pour analyser et extraire les données HTML.

### Installation des bibliothèques
```python
pip install requests beautifulsoup4
```
---

## 2. Scraping d’une page unique <a name="scraping-une-page"></a>

### Objectif
Récupérer les titres d’articles présents sur une seule page web.

### Exemple de code
```python
import requests
from bs4 import BeautifulSoup

def scraper_page(url):
    """
    Fonction pour scraper une page web.
    - url : URL de la page à scraper (str).
    - Retourne une liste des titres présents sur la page.
    """
    reponse = requests.get(url)

    if reponse.status_code == 200:
        soup = BeautifulSoup(reponse.text, 'html.parser')
        titres = soup.find_all('h2')

        donnees = [titre.text.strip() for titre in titres]
        return donnees
    else:
        print(f"Erreur : Impossible de récupérer la page {url}")
        return []

# Exemple d'utilisation
url_exemple = "https://www.pokepedia.fr/Cat%C3%A9gorie:Articles"
resultats = scraper_page(url_exemple)
print(resultats)
```

**Explications :**
1. `requests.get(url)` : Récupère le contenu HTML de la page.
2. `BeautifulSoup(reponse.text, 'html.parser')` : Parse le HTML pour une manipulation aisée.
3. `find_all('h2')` : Recherche tous les éléments HTML avec la balise `<h2>`.
4. `strip()` : Nettoie les espaces superflus.

---

## 3. Crawling : Scraping de plusieurs pages <a name="crawling-pages-multiples"></a>

### Objectif
Automatiser la navigation entre plusieurs pages web pour collecter des données de manière itérative.

### Exemple de code
```python
def scraper_pages(base_url, nb_pages):
    """
    Fonction pour scraper plusieurs pages web.
    - base_url : URL de base sans numéro de page (str).
    - nb_pages : Nombre total de pages à scraper (int).
    - Retourne une liste de données collectées.
    """
    toutes_les_donnees = []

    for numero_page in range(1, nb_pages + 1):
        url_complete = f"{base_url}?page={numero_page}"
        print(f"Scraping de la page : {url_complete}")
        
        donnees = scraper_page(url_complete)
        toutes_les_donnees.extend(donnees)

    return toutes_les_donnees

# Exemple d'utilisation
base_url_exemple = "https://www.pokepedia.fr/Cat%C3%A9gorie:Articles"
resultats_multiples = scraper_pages(base_url_exemple, 3)
print(resultats_multiples)
```

**Explications :**
1. `range(1, nb_pages + 1)` : Crée une boucle pour itérer sur chaque numéro de page.
2. `f"{base_url}?page={numero_page}"` : Construit dynamiquement l’URL de chaque page.
3. `extend()` : Ajoute les données d’une page à la liste principale.

---

## 4. Exemple concret : Scraper les titres d’articles sur Poképedia <a name="exemple-concret"></a>

### Contexte
Poképedia est une encyclopédie consacrée à l’univers de Pokémon. Chaque page de la catégorie contient des articles listés sous forme de titres.

### Exemple d’implémentation
```python
base_url = "https://www.pokepedia.fr/Cat%C3%A9gorie:Articles"
nombre_de_pages = 5

# Scraper les titres sur plusieurs pages
resultats_pokepedia = scraper_pages(base_url, nombre_de_pages)

# Afficher les résultats
for index, titre in enumerate(resultats_pokepedia, start=1):
    print(f"{index}. {titre}")
```

---

## 5. Précautions juridiques et bonnes pratiques <a name="precautions"></a>

1. **Respect des conditions d’utilisation des sites web :** Consulter les mentions légales pour s’assurer que le scraping est autorisé.
2. **Limiter le nombre de requêtes :** Utiliser un délai entre les requêtes pour éviter de surcharger le serveur.
3. **Conformité avec le RGPD :** Ne pas scraper de données personnelles sans consentement.

### Liens utiles
- [CNIL : RGPD et Web Scraping](https://www.cnil.fr/fr/la-reutilisation-des-donnees-publiquement-accessibles-en-ligne-des-fins-de-demarchage-commercial)
- [PLR Avocats : Web Scraping et RGPD](https://www.plravocats.fr/blog/data-protection-rgpd/warning-web-scraping-et-rgpd)

---

## 6. Ressources <a name="ressources"></a>

- [Documentation BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
- [Tutoriel DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-scrape-web-pages-with-beautiful-soup-and-python-3)
- [Vidéo YouTube sur le scraping multiple](https://www.youtube.com/watch?v=h5tfGLsUg7w)

[⬅ Page Précédente](../README.md)
