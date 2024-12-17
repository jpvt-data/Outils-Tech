# Fonctions Type : Geocodage & Visualisation

## Fonction pour le Géocodage et le Géocodage Inversé

La fonction **`geocode()`** permet de réaliser à la fois un géocodage (adresse -> coordonnées) et un géocodage inversé (coordonnées -> adresse).

**Fonction flexible pour effectuer** :
- un géocodage (adresse -> coordonnées) 
- un géocodage inversé (coordonnées -> adresse).
    
**Paramètres**:
- address (str): Adresse à géocoder. Utilisé si latitude et longitude sont None.
- latitude (float): Latitude pour le géocodage inversé. Utilisé si address est None.
- longitude (float): Longitude pour le géocodage inversé. Utilisé si address est None.

**Retourne**:
- dict: Résultat de la requête avec soit les coordonnées, soit l'adresse.

### Code de la Fonction

```python
import requests

def geocode(address=None, latitude=None, longitude=None):
    if address:
        # Géocodage: adresse -> coordonnées
        url = f"https://api-adresse.data.gouv.fr/search/?q={address.replace(' ', '+')}&limit=1"
        response = requests.get(url)
        data = response.json()
        
        if data['features']:
            coordinates = data['features'][0]['geometry']['coordinates']
            return {'latitude': coordinates[1], 'longitude': coordinates[0]}
        else:
            return {"error": "Adresse non trouvée"}
    
    elif latitude is not None and longitude is not None:
        # Géocodage inversé: coordonnées -> adresse
        url = f"https://api-adresse.data.gouv.fr/reverse/?lon={longitude}&lat={latitude}&limit=1"
        response = requests.get(url)
        data = response.json()
        
        if data['features']:
            address = data['features'][0]['properties']['label']
            return {'address': address}
        else:
            return {"error": "Adresse non trouvée"}
    else:
        return {"error": "Fournir une adresse ou des coordonnées valides"}
```

### Exemple d'utilisation pour le géocodage :
```python
result_geocode = geocode(address="1 rue de la paix, Paris")
print(result_geocode)
```

### Exemple d'utilisation pour le géocodage inversé :
```python
result_reverse_geocode = geocode(latitude=48.866667, longitude=2.333333)
print(result_reverse_geocode)
```
---

## Fonction visualisation geocodage :

La fonction `visualiser_carte`() permet de visualiser un point sur une carte avec Folium.

- Si des coordonnées (latitude, longitude) sont fournies, elles sont utilisées directement.
- Si une adresse est fournie, la fonction utilise `geocodage()` pour récupérer les coordonnées.

**Paramètres** :
- `input_data` (tuple ou str) : 
    - Tuple : (latitude, longitude)
    - String : Adresse postale

**Retour** :
- Affiche une carte Folium centrée sur les coordonnées.

```python
import folium

def visualiser_carte(input_data):
    if isinstance(input_data, tuple):
        latitude, longitude = input_data
        description = "Coordonnées fournies"
    elif isinstance(input_data, str):
        coords = geocode(input_data)
        
        if coords and "latitude" in coords and "longitude" in coords:
            try:
                latitude = float(coords['latitude'])
                longitude = float(coords['longitude'])
                description = f"Adresse : {input_data}"
            except ValueError:
                print("Les coordonnées ne sont pas numériques. Vérifier `geocodage()`.")
                return
        else:
            print("Adresse non trouvée ou coordonnées invalides.")
            return
    else:
        print("Format invalide. Fournir une adresse (str) ou des coordonnées (tuple).")
        return

    # Créer une carte centrée
    carte = folium.Map(location=[latitude, longitude], zoom_start=13)
    folium.Marker(
        location=[latitude, longitude],
        popup=description,
        icon=folium.Icon(color='blue', icon='info-sign')
    ).add_to(carte)

    return carte
```

### Exemple d'utilisation avec des coordonnées
```python
carte1 = visualiser_carte((48.8566, 2.3522))  # Paris
carte1
```

### Exemple d'utilisation avec une adresse
```python
carte2 = visualiser_carte("1 rue de la Paix, Paris")
carte2
```
