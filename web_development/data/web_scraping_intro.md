# Web Scraping avec Python

## Introduction
Le web scraping permet d’extraire des données à partir de pages web de manière automatisée.  

Cette technique est essentielle dans de nombreux contextes, tels que la veille concurrentielle, la collecte de données pour des modèles de machine learning ou l’analyse de tendances.  

Cette fiche technique propose une approche pas à pas pour réaliser du web scraping avec Python, en utilisant la bibliothèque BeautifulSoup.

### Cas d’utilisation courants
| Domaine                   | Exemples d’applications                                   |
|---------------------------|---------------------------------------------------------|
| Veille commerciale        | Extraction des prix des produits sur des sites e-commerce |
| Recrutement               | Collecte d’offres d’emploi ciblées                     |
| Analyse des réseaux sociaux| Suivi des mentions ou tendances sur des hashtags         |

## Cadre juridique
Avant de scraper, respecter les conditions d’utilisation des sites web et s’assurer que l’extraction de données ne viole pas les règlements en vigueur (par exemple, RGPD). Éviter de scraper des données sensibles ou privées.

## Bases de HTML et CSS
Le HTML structure le contenu des pages web sous forme de balises. Le CSS gère leur apparence.

**Exemple de structure HTML minimale :**
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Page Exemple</title>
  </head>
  <body>
    <p class="paragraphe">Ceci est un texte.</p>
  </body>
</html>
```
Dans cet exemple, la balise `<p>` est dédiée à un paragraphe.

## Outils requis
- **Requests** : pour récupérer le contenu HTML d’une page.
- **BeautifulSoup** : pour analyser et extraire les données de la structure HTML.

### Installation des bibliothèques
Exécuter dans le terminal :
```bash
pip install requests beautifulsoup4
```

## Étapes pour scraper une page web

### 1. Récupération du contenu HTML
Utiliser la bibliothèque `requests` pour obtenir le code source d’une page web.

**Exemple :**
```python
import requests

# URL à scraper
url = "https://www.pokepedia.fr/Liste_des_Pok%C3%A9mon_par_ordre_alphabétique"

# Simuler un navigateur pour éviter le blocage
headers = {"User-Agent": "Mozilla/5.0"}

# Envoi de la requête HTTP
response = requests.get(url, headers=headers)

# Vérification de la réponse
if response.status_code == 200:
    print("Succès : contenu récupéré")
else:
    print(f"Erreur : {response.status_code}")
```
> **Pourquoi faire cela ?** Cela garantit que la page renvoie le contenu attendu.

### 2. Analyse et parsing HTML avec BeautifulSoup
Créer une instance BeautifulSoup pour traiter le contenu HTML.

**Exemple :**
```python
from bs4 import BeautifulSoup

# Créer la "soupe"
soup = BeautifulSoup(response.text, 'html.parser')

# Afficher un extrait formaté
print(soup.prettify()[:500])
```
> **Objectif :** Visualiser la structure HTML et identifier les balises pertinentes.

### 3. Extraction des données cibles
Identifier les balises contenant les informations d’intérêt. Utiliser `find` ou `find_all` pour cibler des éléments spécifiques.

**Exemple : Extraction des noms de Pokémon :**
```python
# Trouver les balises correspondantes
noms_pokemon = soup.find_all("a", class_="mw-redirect")

# Extraire le texte des balises
liste_pokemon = [nom.get_text() for nom in noms_pokemon]

# Afficher les 10 premiers noms
print(liste_pokemon[:10])
```
> **Pourquoi utiliser `class_="mw-redirect"` ?** Cette classe correspond à l’emplacement des noms de Pokémon sur la page cible.

### 4. Sauvegarde des données
Exporter les données dans un format utilisable (CSV, JSON, etc.).

**Exemple : Sauvegarde en CSV :**
```python
import csv

# Créer un fichier CSV
with open("pokemon.csv", "w", newline="", encoding="utf-8") as fichier_csv:
    writer = csv.writer(fichier_csv)
    writer.writerow(["Nom"])
    for nom in liste_pokemon:
        writer.writerow([nom])

print("Données enregistrées dans pokemon.csv")
```

## Optimisations et bonnes pratiques
- **Limiter le nombre de requêtes :** Respecter les serveurs web en espaçant les requêtes (par exemple, avec `time.sleep`).
- **Gérer les erreurs :** Implémenter une gestion des erreurs HTTP et des exceptions Python.

**Exemple : Gestion des erreurs HTTP :**
```python
try:
    response = requests.get(url, headers=headers)
    response.raise_for_status()
except requests.exceptions.RequestException as e:
    print(f"Erreur lors de la récupération des données : {e}")
```

## Ressources utiles
- [Documentation BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
- [Liste des Pokémon - Poképedia](https://www.pokepedia.fr/Liste_des_Pok%C3%A9mon_par_ordre_alphab%C3%A9tique)
- [Tutoriel Requests](https://docs.python-requests.org/en/latest/)

Ce guide constitue une introduction pratique pour réaliser du web scraping. Adapter les techniques présentées en fonction des besoins spécifiques et des contraintes imposées par les sites cibles.

