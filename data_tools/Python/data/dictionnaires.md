[⬅ Page Précédente](../README.md)

# Python : Les Dictionnaires

## Objectif

Les dictionnaires en Python sont des structures de données très puissantes qui permettent de stocker des données sous forme de paires clé-valeur.

Contrairement aux listes où les éléments sont indexés par des entiers, les dictionnaires utilisent des clés personnalisées pour accéder à leurs valeurs. Cette structure est particulièrement utile dans des situations où l'on souhaite associer une valeur spécifique à un identifiant unique et faciliter l'accès à ces données.

L'objectif de cette fiche est de comprendre la création, l'utilisation et les opérations sur les dictionnaires en Python, en montrant des exemples concrets d’utilisation.

---

### 1. Définition et Création d'un Dictionnaire

Un dictionnaire en Python est une collection non ordonnée de paires clé-valeur. Il permet de stocker et de récupérer des données en associant une clé unique à une valeur. Les clés dans un dictionnaire doivent être immuables, comme des chaînes de caractères, des entiers ou des tuples.

#### Syntaxe de création d'un dictionnaire :

```python
# Création d'un dictionnaire vide
mon_dictionnaire = {}

# Création d'un dictionnaire avec des éléments
pokemons = {
    "Pikachu": "électrique",
    "Bulbizarre": "plante",
    "Salamèche": "feu"
}
```

**Explication** :  
- `mon_dictionnaire` est un dictionnaire vide, prêt à être rempli.
- Le dictionnaire `pokemons` contient des paires clé-valeur où les clés sont des noms de Pokémons (par exemple "Pikachu") et les valeurs sont leurs types (par exemple "électrique").

### 2. Accès aux Valeurs d'un Dictionnaire

L'accès aux valeurs se fait en utilisant la clé correspondante. En revanche, contrairement à une liste où l'on utilise un index numérique, ici on utilise une clé qui peut être un string ou un autre type immuable.

#### Exemple d'accès à une valeur par clé :

```python
# Accéder au type de Pikachu
print(pokemons["Pikachu"])  # Affiche "électrique"
```

**Explication** :  
L'accès à la valeur de la clé "Pikachu" retourne le type associé, soit "électrique".

### 3. Ajout et Modification des Éléments

Les dictionnaires permettent d'ajouter de nouveaux éléments ou de modifier ceux existants en utilisant la clé.

#### Ajout d'un nouvel élément :

```python
# Ajouter un nouveau Pokémon au dictionnaire
pokemons["Carapuce"] = "eau"
print(pokemons)
```

**Explication** :  
On ajoute une nouvelle entrée où "Carapuce" est la clé et "eau" est la valeur associée.

#### Modification d'un élément existant :

```python
# Modifier le type de Pikachu
pokemons["Pikachu"] = "électrique et acier"
print(pokemons)
```

**Explication** :  
La valeur associée à la clé "Pikachu" est mise à jour pour refléter un double type "électrique et acier".

### 4. Suppression d'Éléments

Il est possible de supprimer des éléments d'un dictionnaire de plusieurs manières.

#### Suppression avec `del` :

```python
# Supprimer l'entrée "Bulbizarre"
del pokemons["Bulbizarre"]
print(pokemons)
```

**Explication** :  
La fonction `del` permet de supprimer une paire clé-valeur en spécifiant la clé à supprimer.

#### Suppression avec `pop()` :

```python
# Supprimer et récupérer le type de Salamèche
type_salamèche = pokemons.pop("Salamèche")
print(type_salamèche)  # Affiche "feu"
print(pokemons)
```

**Explication** :  
La méthode `pop()` permet de supprimer un élément et de récupérer sa valeur en même temps.

### 5. Opérations Avancées sur les Dictionnaires

Les dictionnaires offrent diverses méthodes pour manipuler les données de manière plus avancée.

#### Parcourir les clés et les valeurs :

```python
# Parcourir les clés et valeurs du dictionnaire
for nom, type_ in pokemons.items():
    print(f"{nom} est de type {type_}")
```

**Explication** :  
La méthode `items()` retourne un générateur qui permet de parcourir toutes les paires clé-valeur du dictionnaire.

#### Vérifier la présence d'une clé :

```python
# Vérifier si la clé "Pikachu" existe dans le dictionnaire
if "Pikachu" in pokemons:
    print("Pikachu est dans le dictionnaire")
```

**Explication** :  
L'opérateur `in` permet de vérifier la présence d'une clé dans un dictionnaire.

#### Obtenir toutes les clés ou toutes les valeurs :

```python
# Obtenir toutes les clés
print(pokemons.keys())

# Obtenir toutes les valeurs
print(pokemons.values())
```

**Explication** :  
La méthode `keys()` retourne un objet dict_keys contenant toutes les clés, et `values()` retourne un objet dict_values contenant toutes les valeurs.

### 6. Exemple Complet : Gestion d'une Équipe Pokémon

Imaginons qu’on souhaite organiser une équipe de Pokémons sous forme de dictionnaire. Les noms des Pokémons seront les clés, et les valeurs seront leurs niveaux d'entraînement.

```python
# Création d'un dictionnaire pour l'équipe Pokémon
équipe = {
    "Pikachu": 35,
    "Evoli": 20,
    "Dracaufeu": 50
}

# Accéder au niveau de Pikachu
print(équipe["Pikachu"])  # Affiche 35

# Ajouter un nouveau Pokémon
équipe["Tortank"] = 45
print(équipe)

# Améliorer le niveau de Dracaufeu
équipe["Dracaufeu"] += 10
print(équipe["Dracaufeu"])  # Affiche 60

# Supprimer un Pokémon de l'équipe
del équipe["Evoli"]
print(équipe)
```

**Explication** :  
- Le dictionnaire `équipe` contient trois Pokémons avec leurs niveaux d'entraînement respectifs.
- On accède à un niveau, on ajoute un nouveau Pokémon, on améliore un niveau existant et on supprime un Pokémon de l'équipe.

### 7. Ressources Complémentaires

Pour aller plus loin et approfondir la compréhension des dictionnaires en Python, voici quelques ressources supplémentaires :

- [Les dictionnaires en Python - W3Schools](https://www.w3schools.com/python/python_dictionaries.asp)
- [5 Advanced Operations Using Dictionaries in Python](https://betterprogramming.pub/5-advanced-operations-using-dictionaries-in-python-5f8edb4719fa)
- [Machine Learnia: Les dictionnaires](https://www.youtube.com/watch?v=QR-gUWAeLqs)

---

Cette fiche a pour but de fournir une compréhension complète des dictionnaires, leur utilisation et leurs méthodes principales. Grâce à ces concepts et exemples, il sera facile d'intégrer les dictionnaires dans des projets Python pour organiser et manipuler des données efficacement.

[⬅ Page Précédente](../README.md)

