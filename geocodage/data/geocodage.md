# Géocodage et Géocodage Inversé

## Introduction

Le géocodage est un processus essentiel dans les projets de data analytics, de cartographie et d’analyse spatiale. Il consiste à convertir une adresse postale en coordonnées géographiques (latitude et longitude). Le géocodage inversé, quant à lui, permet de convertir des coordonnées géographiques en une adresse postale. Ces deux processus sont cruciaux dans des applications telles que la géolocalisation, la planification de trajets ou l’analyse de données géospatiales.

Cette fiche technique décrit les étapes du géocodage et du géocodage inversé, avec des exemples pratiques utilisant l'API **geo.api.gouv.fr** pour travailler avec les données géographiques en France. Vous apprendrez également à créer des fonctions Python pour automatiser le géocodage et à visualiser les données géographiques sur une carte avec la bibliothèque **Folium**.

## 1. Concepts de Base : Coordonnées Géographiques et Cartographie

Les coordonnées géographiques représentent une localisation précise sur la surface de la Terre :

- **Latitude** : Position nord-sud, allant de -90° (pôle Sud) à +90° (pôle Nord).
- **Longitude** : Position est-ouest, allant de -180° à +180° par rapport au méridien de Greenwich.

Ces coordonnées sont utilisées dans les systèmes de cartographie pour localiser des points d’intérêt, tels que des adresses, des commerces, ou des points touristiques.

## 2. Géocodage : Traduction d'une Adresse en Coordonnées Géographiques

Le géocodage consiste à convertir une adresse postale en coordonnées géographiques. Pour cela, nous pouvons utiliser l'API **geo.api.gouv.fr**, qui fournit une base de données d'adresses françaises et leurs coordonnées associées.

### Exemple de Géocodage

Nous allons maintenant voir un exemple de code Python pour géocoder une adresse en utilisant l'API **geo.api.gouv.fr**.

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

### Explication du Code :

- La requête GET est envoyée à l'API avec l'adresse à géocoder.
- La réponse de l'API est analysée au format JSON.
- Nous extrayons les coordonnées (latitude et longitude) du premier résultat de la réponse.

#### Résultat Attendu :

```
Latitude: 48.866667, Longitude: 2.333333
```

### Création de la Fonction `API_adresse`

Nous pouvons automatiser ce processus en créant une fonction qui prend une adresse postale, génère l'URL de la requête et retourne les coordonnées associées.

```python
import requests

def API_adresse(adresse_postale):
    # Créer l'URL de requête
    link_main = 'https://api-adresse.data.gouv.fr/search/?q='
    adresse = adresse_postale.replace(" ", "+")  # Remplacement des espaces par "+"
    link = link_main + adresse
    r = requests.get(link).json()
    
    # Extraction des coordonnées
    if len(r['features']) > 0:
        coordinates = r['features'][0]['geometry']['coordinates']
        return coordinates
    else:
        return None

# Exemple d'utilisation :
print(API_adresse('728 Route de Villerest, 42155 Ouches'))
```

#### Résultat Attendu :

```
[3.993163, 46.00996]
```

## 3. Géocodage Inversé : Trouver une Adresse à partir de Coordonnées Géographiques

Le géocodage inversé permet de retrouver une adresse à partir de coordonnées géographiques. Pour ce faire, nous envoyons une requête contenant la latitude et la longitude à l'API **geo.api.gouv.fr**.

### Exemple de Géocodage Inversé

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

### Résultat Attendu :

```
Adresse : 1 Rue de la Paix, 75002 Paris, France
```

## 4. Visualisation des Coordonnées sur une Carte avec Folium

Une fois que nous avons les coordonnées, nous pouvons les afficher sur une carte interactive. Pour cela, nous utiliserons la bibliothèque **Folium** en Python.

### Exemple de Visualisation avec Folium

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

### Explication du Code :

- La carte est générée avec **folium.Map()**, centrée sur les coordonnées du Machu Picchu.
- Un marqueur est ajouté à l'emplacement spécifié.

### Résultat Attendu :

Une carte interactive avec un marqueur sur le Machu Picchu.

## 5. Application Pratique : Visualisation des Restaurants sur une Carte

Supposons que nous ayons un DataFrame contenant des adresses de restaurants et que nous souhaitions afficher ces adresses sur une carte. Nous utiliserons la fonction `API_adresse` pour géocoder chaque adresse et afficher les résultats sur une carte.

### Application et mise en pratique

Objectif : Création d'une carte interactive à l'aide de la bibliothèque Folium pour **visualiser plusieurs lieux d'intérêt à Bordeaux**.

Lieux d'intérêt à afficher sur la carte :

    La Place de la Bourse
    Le Pont de Pierre
    Le Parc Bordelais
    La Cité du Vin
    La Cathédrale Saint-André

#### Préparation de l'exercice :

Installation de Folium : Si vous ne l'avez pas déjà, installez la bibliothèque Folium avec la commande suivante :

```python
    pip install folium
```

#### Création de la carte interactive :

Voici le code Python pour créer la carte et y ajouter ces lieux :
```python
import folium

# Initialiser la carte centrée sur Bordeaux avec un zoom de départ
carte_bordeaux = folium.Map(location=[44.8378, -0.5792], zoom_start=13)

# Lieux d'intérêt à Bordeaux avec leurs coordonnées GPS
lieux = {
    "Place de la Bourse": [44.8417, -0.5773],
    "Pont de Pierre": [44.8347, -0.5771],
    "Parc Bordelais": [44.8682, -0.5806],
    "Cité du Vin": [44.8697, -0.5572],
    "Cathédrale Saint-André": [44.8370, -0.5792]
}

# Ajouter des marqueurs sur la carte pour chaque lieu
for lieu, coord in lieux.items():
    folium.Marker(
        location=coord,
        popup=lieu,
        icon=folium.Icon(color='blue', icon='info-sign')
    ).add_to(carte_bordeaux)

# Sauvegarder la carte sous forme de fichier HTML
carte_bordeaux.save("carte_bordeaux.html")
```

#### Explication du code :

- **Initialisation de la carte** : La carte est centrée sur les coordonnées de Bordeaux ([44.8378, -0.5792]) avec un niveau de zoom de 13 pour afficher la ville dans un rayon raisonnable.

- **Coordonnées des lieux d'intérêt** : Les lieux comme la Place de la Bourse, le Pont de Pierre, le Parc Bordelais, la Cité du Vin, et la Cathédrale Saint-André sont stockés dans un dictionnaire avec leurs coordonnées GPS respectives.

- **Ajout des marqueurs** : Pour chaque lieu, un marqueur est ajouté à la carte. L'option popup=lieu permet d'afficher le nom du lieu lorsqu'on clique sur le marqueur, et l'option icon='info-sign' personnalise l'icône.

- **Sauvegarde de la carte** : La carte générée est sauvegardée dans un fichier HTML nommé carte_bordeaux.html que vous pouvez ouvrir dans un navigateur pour visualiser la carte interactive.
  
---

## Liens Utiles

- [Documentation de l'API geo.api.gouv.fr](https://geo.api.gouv.fr/adresse)
- [Bibliothèque Folium pour la cartographie](https://python-visualization.github.io/folium/)
- [Page Wikipédia sur le Géocodage](https://fr.wikipedia.org/wiki/G%C3%A9ocodage)

## Conclusion

Le géocodage et le géocodage inversé sont des processus essentiels dans la gestion des données géographiques. L'API **geo.api.gouv.fr** permet de facilement géocoder et effectuer des géocodages inversés en France. La visualisation des données géographiques avec **Folium** permet de créer des cartes interactives, parfaites pour des applications telles que la géolocalisation et l'analyse spatiale.
