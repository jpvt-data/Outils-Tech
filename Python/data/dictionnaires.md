# Python : Les Dictionnaires

## Objectif

Les dictionnaires en Python sont des structures de données très puissantes qui permettent de stocker des données sous forme de paires clé-valeur. Contrairement aux listes où les éléments sont indexés par des entiers, les dictionnaires utilisent des clés personnalisées pour accéder à leurs valeurs. Cette structure est particulièrement utile dans des situations où l'on souhaite associer une valeur spécifique à un identifiant unique et faciliter l'accès à ces données.

L'objectif de cette fiche est de comprendre la création, l'utilisation et les opérations sur les dictionnaires en Python, en montrant des exemples concrets d’utilisation. À la fin de cette fiche, il sera possible de manipuler des dictionnaires pour stocker et accéder à des données de manière efficace.

---

### 1. Définition et Création d'un Dictionnaire

Un dictionnaire en Python est une collection non ordonnée de paires clé-valeur. Il permet de stocker et de récupérer des données en associant une clé unique à une valeur. Les clés dans un dictionnaire doivent être immuables, comme des chaînes de caractères, des entiers ou des tuples.

#### Syntaxe de création d'un dictionnaire :

```python
# Création d'un dictionnaire vide
mon_dictionnaire = {}

# Création d'un dictionnaire avec des éléments
personnes = {
    "Alex": 25,
    "Ben": 30,
    "Charlie": 35
}
```

**Explication** :  
- `mon_dictionnaire` est un dictionnaire vide, prêt à être rempli.
- Le dictionnaire `personnes` contient des paires clé-valeur où les clés sont des noms (par exemple "Alex") et les valeurs sont des âges (par exemple 25).

### 2. Accès aux Valeurs d'un Dictionnaire

L'accès aux valeurs se fait en utilisant la clé correspondante. En revanche, contrairement à une liste où l'on utilise un index numérique, ici on utilise une clé qui peut être un string ou un autre type immuable.

#### Exemple d'accès à une valeur par clé :

```python
# Accéder à l'âge de Ben
print(personnes["Ben"])  # Affiche 30
```

**Explication** :  
L'accès à la valeur de la clé "Ben" retourne l'âge associé, soit 30.

### 3. Ajout et Modification des Éléments

Les dictionnaires permettent d'ajouter de nouveaux éléments ou de modifier ceux existants en utilisant la clé.

#### Ajout d'un nouvel élément :

```python
# Ajouter une nouvelle personne au dictionnaire
personnes["David"] = 40
print(personnes)
```

**Explication** :  
On ajoute une nouvelle entrée où "David" est la clé et 40 est la valeur associée.

#### Modification d'un élément existant :

```python
# Modifier l'âge de Ben
personnes["Ben"] = 32
print(personnes)
```

**Explication** :  
La valeur associée à la clé "Ben" est mise à jour de 30 à 32.

### 4. Suppression d'Éléments

Il est possible de supprimer des éléments d'un dictionnaire de plusieurs manières.

#### Suppression avec `del` :

```python
# Supprimer l'entrée "Charlie"
del personnes["Charlie"]
print(personnes)
```

**Explication** :  
La fonction `del` permet de supprimer une paire clé-valeur en spécifiant la clé à supprimer.

#### Suppression avec `pop()` :

```python
# Supprimer et récupérer l'élément "Alex"
age_alex = personnes.pop("Alex")
print(age_alex)  # Affiche 25
print(personnes)
```

**Explication** :  
La méthode `pop()` permet de supprimer un élément et de récupérer sa valeur en même temps.

### 5. Opérations Avancées sur les Dictionnaires

Les dictionnaires offrent diverses méthodes pour manipuler les données de manière plus avancée.

#### Parcourir les clés et les valeurs :

```python
# Parcourir les clés et valeurs du dictionnaire
for nom, age in personnes.items():
    print(f"{nom} a {age} ans")
```

**Explication** :  
La méthode `items()` retourne un générateur qui permet de parcourir toutes les paires clé-valeur du dictionnaire.

#### Vérifier la présence d'une clé :

```python
# Vérifier si la clé "Ben" existe dans le dictionnaire
if "Ben" in personnes:
    print("Ben est dans le dictionnaire")
```

**Explication** :  
L'opérateur `in` permet de vérifier la présence d'une clé dans un dictionnaire.

#### Obtenir toutes les clés ou toutes les valeurs :

```python
# Obtenir toutes les clés
print(personnes.keys())

# Obtenir toutes les valeurs
print(personnes.values())
```

**Explication** :  
La méthode `keys()` retourne un objet dict_keys contenant toutes les clés, et `values()` retourne un objet dict_values contenant toutes les valeurs.

### 6. Exemple Complet : Gestion d'un Frigo

Imaginons qu’on souhaite organiser les aliments de notre frigo sous forme de dictionnaire. Les catégories d'aliments seront les clés, et les valeurs seront les listes d’aliments correspondantes.

```python
# Création d'un dictionnaire pour le frigo
frigo = {
    "viandes": ["boeuf", "poulet", "porc"],
    "fruits": ["pomme", "banane", "orange"],
    "légumes": ["carotte", "brocoli", "tomate"]
}

# Accéder aux fruits dans le frigo
print(frigo["fruits"])  # Affiche ['pomme', 'banane', 'orange']

# Ajouter un nouvel aliment dans les légumes
frigo["légumes"].append("épinard")
print(frigo["légumes"])  # Affiche ['carotte', 'brocoli', 'tomate', 'épinard']

# Supprimer un aliment
frigo["fruits"].remove("banane")
print(frigo["fruits"])  # Affiche ['pomme', 'orange']
```

**Explication** :  
- Le dictionnaire `frigo` contient trois catégories : "viandes", "fruits", et "légumes".
- On accède à la liste des fruits, on y ajoute un nouvel élément (épinard dans la catégorie "légumes") et on supprime un élément de la catégorie "fruits".

### 7. Ressources Complémentaires

Pour aller plus loin et approfondir la compréhension des dictionnaires en Python, voici quelques ressources supplémentaires :

- [Les dictionnaires en Python - W3Schools](https://www.w3schools.com/python/python_dictionaries.asp)
- [5 Advanced Operations Using Dictionaries in Python](https://betterprogramming.pub/5-advanced-operations-using-dictionaries-in-python-5f8edb4719fa)
- [Machine Learnia: Les dictionnaires](https://www.youtube.com/watch?v=QR-gUWAeLqs)

---

Cette fiche a pour but de fournir une compréhension complète des dictionnaires, leur utilisation et leurs méthodes principales. Grâce à ces concepts et exemples, il sera facile d'intégrer les dictionnaires dans des projets Python pour organiser et manipuler des données efficacement.
