# Géocodage et Géocodage inversé

## Introduction

Le géocodage est une opération clé dans de nombreux projets de data analytics, de cartographie et d'analyse spatiale. Cette technique permet d'associer des coordonnées géographiques (latitude et longitude) à une adresse postale. À l'inverse, le géocodage inversé permet d'obtenir l'adresse correspondant à un jeu de coordonnées géographiques. Ces opérations sont essentielles dans les applications de géolocalisation, de planification de trajets ou encore dans l'analyse de données géospatiales.

Dans cette fiche technique, nous allons découvrir le processus de géocodage et de géocodage inversé, et apprendre à utiliser l'API **geo.api.gouv.fr** pour effectuer ces tâches. Ce type d'API est particulièrement utile pour obtenir des informations géographiques sur les adresses en France. L'objectif est de comprendre le fonctionnement de ces processus et de pouvoir les appliquer dans un projet d'analyse de données ou de cartographie.

## 1. Concepts de base : Coordonnées géographiques et Cartographie

Les coordonnées géographiques sont des valeurs numériques représentant une localisation sur la surface de la Terre. Deux éléments principaux sont utilisés :

- **Latitude** : Position nord-sud sur la Terre, mesurée à partir de l'équateur. La latitude varie de -90° (pôle Sud) à +90° (pôle Nord).
- **Longitude** : Position est-ouest, mesurée par rapport au méridien de Greenwich. Elle varie de -180° à +180°.

Le système de géocodage que nous utilisons repose sur ce modèle pour représenter des points sur la carte. Ces coordonnées sont ensuite utilisées dans les systèmes de cartographie pour localiser des points d'intérêt.

## 2. Géocodage : Traduction d'une adresse en coordonnées géographiques

Le géocodage consiste à traduire une adresse postale en coordonnées géographiques. Pour effectuer cette opération, on peut utiliser un service comme **geo.api.gouv.fr**, une API REST qui fournit une base de données d'adresses françaises et les coordonnées associées.

### Étapes pour effectuer un géocodage :

1. **Envoyer une requête à l'API geo.api.gouv.fr** : La requête contiendra une adresse à géocoder.
2. **Analyser la réponse** : L'API renvoie un ou plusieurs résultats, comprenant les coordonnées géographiques et un score indiquant la précision de la correspondance.
3. **Extraire les coordonnées** : Retenir les coordonnées du résultat ayant le score le plus élevé.

### Exemple concret : Géocoder une adresse en France

Voici un exemple de code Python pour effectuer un géocodage avec l'API **geo.api.gouv.fr**.

```python
import requests

# Adresse à géocoder
adresse = "1 rue de la paix, Paris"

# Effectuer une requête GET à l'API
url = f"https://api-adresse.data.gouv.fr/search/?q={adresse}&limit=1"
response = requests.get(url)

# Analyser la réponse
data = response.json()

# Extraire la latitude et la longitude
if data['features']:
    latitude = data['features'][0]['geometry']['coordinates'][1]
    longitude = data['features'][0]['geometry']['coordinates'][0]
    print(f"Latitude: {latitude}, Longitude: {longitude}")
else:
    print("Adresse non trouvée")
```

### Explication du code :

- **Requête GET** : On envoie une requête à l'API en utilisant l'adresse à géocoder.
- **Analyse JSON** : La réponse de l'API est au format JSON, que l'on convertit en objet Python pour faciliter l'extraction des données.
- **Extraction des coordonnées** : On récupère la latitude et la longitude des résultats retournés par l'API.

#### Résultat attendu :

```
Latitude: 48.866667, Longitude: 2.333333
```

## 3. Géocodage inversé : Trouver une adresse à partir de coordonnées géographiques

Le géocodage inversé consiste à obtenir une adresse à partir de coordonnées géographiques (latitude et longitude). Ce processus est souvent utilisé pour afficher une adresse à l'utilisateur lorsqu'il clique sur une carte ou pour retrouver des informations sur un lieu donné.

### Étapes pour effectuer un géocodage inversé :

1. **Envoyer une requête à l'API geo.api.gouv.fr** : Cette fois, la requête contient les coordonnées géographiques (latitude et longitude).
2. **Analyser la réponse** : L'API renvoie l'adresse correspondant aux coordonnées ou l'adresse la plus proche.
3. **Extraire l'adresse** : Extraire l'adresse complète de la réponse.

### Exemple concret : Géocoder inversé avec des coordonnées

```python
# Coordonnées à géocoder inversé
latitude = 48.866667
longitude = 2.333333

# Effectuer une requête GET à l'API pour géocodage inversé
url = f"https://api-adresse.data.gouv.fr/reverse/?lon={longitude}&lat={latitude}&limit=1"
response = requests.get(url)

# Analyser la réponse
data = response.json()

# Extraire l'adresse
if data['features']:
    adresse = data['features'][0]['properties']['label']
    print(f"Adresse : {adresse}")
else:
    print("Aucune adresse trouvée")
```

### Explication du code :

- **Requête GET inversée** : On envoie une requête à l'API avec les coordonnées géographiques.
- **Analyse JSON** : On convertit la réponse en JSON et on extrait l'adresse à partir des données retournées.
- **Affichage de l'adresse** : On affiche l'adresse correspondante aux coordonnées.

#### Résultat attendu :

```
Adresse : 1 Rue de la Paix, 75002 Paris, France
```

## 4. Représentation graphique : Visualiser les coordonnées sur une carte

Une fois les coordonnées géographiques obtenues, il est possible de les visualiser sur une carte. Pour cela, la bibliothèque Python **folium** peut être utilisée.

### Exemple de code pour afficher une carte avec un marqueur

```python
import folium

# Coordonnées géographiques du Machu Picchu, Pérou
latitude = -13.1631
longitude = -72.5450

# Créer la carte
m = folium.Map(location=[latitude, longitude], zoom_start=12)

# Ajouter un marqueur sur le Machu Picchu
folium.Marker(location=[latitude, longitude], popup="Machu Picchu").add_to(m)

# Afficher la carte
m
```

### Explication du code :

- **Création de la carte** : La fonction `folium.Map()` génère une carte centrée sur les coordonnées données (latitude, longitude).
- **Ajout d'un marqueur** : Le marqueur est ajouté à la carte à l'emplacement spécifié.
- **Affichage** : La carte est rendue interactive avec `m`.

### Résultat attendu :

Une carte interactive affichant le Machu Picchu avec un marqueur cliquable.

## 5. Liens utiles

- [Documentation de l'API geo.api.gouv.fr](https://geo.api.gouv.fr/adresse)
- [Page Wikipédia sur le Géocodage](https://fr.wikipedia.org/wiki/G%C3%A9ocodage)
- [Bibliothèque Folium pour la cartographie](https://python-visualization.github.io/folium/)

## Conclusion

Le géocodage et le géocodage inversé sont des opérations essentielles pour manipuler des données géographiques. En utilisant l'API **geo.api.gouv.fr**, il est possible de géocoder une adresse en coordonnées géographiques ou vice versa. Ces outils sont largement utilisés dans des applications de géolocalisation, d'analyse spatiale et de cartographie interactive.

