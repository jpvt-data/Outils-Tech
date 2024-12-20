# Fiche Technique : Web Scraping - Crawling

## Sommaire

1. Introduction : Comprendre le crawling
2. Étapes clés du crawling
3. Exemple pratique : Extraction des informations des Pokémon
   - Récupération des URL
   - Scraping de niveau 2 : Extraction de détails
   - Application à l'ensemble des données

## Introduction : Comprendre le crawling

Le crawling consiste à parcourir une ou plusieurs pages web pour extraire des données structurées. Contrairement au scraping classique qui se concentre sur une seule page, le crawling explore également les liens contenus dans ces pages pour collecter des données supplémentaires. 

### Applications

- Indexation de sites web par les moteurs de recherche.
- Extraction d'informations détaillées à partir de bases interconnectées (exemple : données produits sur des e-commerces).
- Analyse des réseaux sociaux ou communautés en ligne pour comprendre les connexions.

## Étapes clés du crawling

Le processus de crawling suit deux grandes étapes :

| Étape                  | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| Récupération des URL   | Identifier les liens intéressants à partir d'une page initiale.            |
| Scraping des pages     | Collecter les données nécessaires à partir des pages référencées.          |

Il est essentiel de choisir un format structuré pour stocker les résultats : tableaux (DataFrames), dictionnaires ou JSON.

---

## Exemple pratique : Extraction des informations des Pokémon

Objectif : Récupérer les noms et types des Pokémon depuis Poképédia, puis explorer les pages de chaque Pokémon pour collecter leurs statistiques détaillées (attaque, défense, etc.).

### Bibliothèques nécessaires
```python
from bs4 import BeautifulSoup
import requests
import pandas as pd
```

### 1. Récupération des URL

Utilisation de la page listant les Pokémon pour extraire les liens vers leurs fiches individuelles.

```python
# URL de la page principale
url = "https://www.pokepedia.fr/Liste_des_Pok%C3%A9mon_par_num%C3%A9ro"

# Requête HTTP
html = requests.get(url)

# Analyse avec BeautifulSoup
soup = BeautifulSoup(html.text, 'html.parser')

# Extraction des liens des Pokémon
table_pokemon = soup.find("table", {"class": "tableaustandard sortable"})
links = table_pokemon.find_all("a")

# Stockage dans un DataFrame
data = {
    "nom": [link.text for link in links],
    "url": ["https://www.pokepedia.fr" + link["href"] for link in links]
}
df_pokemon = pd.DataFrame(data)
print(df_pokemon.head())
```

### 2. Scraping de niveau 2 : Extraction de détails

Création d'une fonction pour aller sur chaque fiche et récupérer les statistiques des Pokémon.

```python
# Fonction pour crawler une fiche Pokémon
def extraire_statistiques(url):
    try:
        # Requête HTTP
        html = requests.get(url)
        soup = BeautifulSoup(html.text, 'html.parser')

        # Recherche des statistiques
        stats_table = soup.find("table", {"class": "tableaustandard"})
        stats = stats_table.find_all("td")

        # Extraction des valeurs
        attaque = int(stats[1].text.strip())
        defense = int(stats[2].text.strip())

        return attaque, defense
    except Exception as e:
        return None, None

# Test sur un lien
print(extraire_statistiques(df_pokemon.iloc[0]["url"]))
```

### 3. Application à l'ensemble des données

Application de la fonction sur tous les liens et ajout des statistiques dans le DataFrame.

```python
# Ajout des colonnes statistiques
df_pokemon["attaque"], df_pokemon["defense"] = zip(*df_pokemon["url"].apply(extraire_statistiques))

# Affichage des données complètes
print(df_pokemon.head())
```

### Analyse

Calculer des statistiques globales, comme la moyenne des attaques et défenses :

```python
moyenne_attaque = df_pokemon["attaque"].mean()
moyenne_defense = df_pokemon["defense"].mean()

print(f"Moyenne d'attaque : {moyenne_attaque}")
print(f"Moyenne de défense : {moyenne_defense}")
```

---

## Conclusion

Le crawling permet d'explorer et d'extraire des données à grande échelle de manière automatisée. Dans cet exemple, les données des Pokémon ont été structurées et analysées avec succès, mais ce processus peut être adapté à d'autres types de bases interconnectées.

### Ressources

- Documentation BeautifulSoup : https://www.crummy.com/software/BeautifulSoup/
- Poképédia : https://www.pokepedia.fr
