[⬅ Page Précédente](../README.md)

# Python - Modules pour l'Analyse de Données

## Introduction

Dans le cadre de l'analyse de données, Python offre une multitude d'outils permettant de simplifier et d'automatiser de nombreuses tâches. L'un des éléments clés de Python est l'utilisation des **modules**, qui permettent d'augmenter les fonctionnalités du langage en réutilisant du code déjà écrit, organisé et testé. Un module en Python est simplement un fichier contenant du code qui peut être réutilisé dans différents projets. Cela permet d'organiser le travail de manière plus lisible et de ne pas réinventer la roue. 

Cette fiche présente les bases de l'utilisation des modules en Python, les types de modules (standards et externes), ainsi que l'importation et la création de modules personnalisés pour vos projets d'analyse de données.

## Qu'est-ce qu'un module ?

Un module en Python est un fichier `.py` qui contient des définitions de fonctions, des classes, et des variables qui peuvent être utilisées dans d'autres fichiers Python. Par exemple, la fonction `print()` est définie dans un module de la bibliothèque standard de Python, et chaque fois que vous utilisez `print()`, vous faites appel à ce module.

### Exemple concret : Utilisation du module mathématique
```python
import math

# Calcul de la racine carrée de 16
resultat = math.sqrt(16)
print(resultat)  # Affiche : 4.0
```

Ici, le module `math` fournit des fonctions mathématiques avancées comme `sqrt()` pour calculer la racine carrée. Au lieu de devoir écrire cette fonction soi-même, il est plus simple d'utiliser celle déjà fournie dans le module.

## Pourquoi utiliser des modules ?

L’utilisation des modules permet de :

- **Réutiliser du code** : Pas besoin de réécrire des fonctions ou des classes courantes.
- **Organiser le code** : Diviser le code en modules pour rendre le script plus propre et plus facile à maintenir.
- **Accéder à des fonctionnalités avancées** : Les modules de la bibliothèque standard ou externes offrent des fonctionnalités très puissantes.
- **Faciliter la collaboration** : En partageant des modules, plusieurs personnes peuvent travailler sur des aspects différents du code sans se chevaucher.

## Types de modules

Il existe deux types de modules en Python :

1. **Modules standards** : Ce sont les modules inclus dans Python par défaut.
2. **Modules externes** : Ce sont des modules créés par la communauté ou des bibliothèques tierces, qui ne sont pas inclus dans Python par défaut et doivent être installés manuellement.

### Modules standards utiles pour les data analysts débutants

Voici quelques modules standards que les data analysts débutants peuvent utiliser pour leurs tâches :

#### 1. `math` : Fonctions mathématiques
```python
import math

# Affichage de la valeur de pi
print(math.pi)  # 3.141592653589793

# Calcul de la racine carrée de 16
print(math.sqrt(16))  # 4.0
```

#### 2. `random` : Génération de nombres aléatoires
```python
import random

# Génération d'un entier aléatoire entre 1 et 10
print(random.randint(1, 10))  # Exemple : 7

# Sélection aléatoire d'un élément dans une liste
print(random.choice(['Pikachu', 'Bulbizarre', 'Salamèche']))  # Exemple : 'Bulbizarre'
```

#### 3. `datetime` : Manipulation des dates et heures
```python
from datetime import datetime, timedelta

# Récupérer la date et l'heure actuelles
now = datetime.now()
print(now)

# Ajouter 7 jours à la date actuelle
future_date = now + timedelta(days=7)
print(future_date)
```

#### 4. `statistics` : Calculs statistiques de base
```python
import statistics

# Liste de données
data = [10, 20, 20, 30, 30, 30, 40, 40, 50]

# Moyenne des données
print(statistics.mean(data))  # 30.0

# Médiane des données
print(statistics.median(data))  # 30

# Mode des données
print(statistics.mode(data))  # 30
```

## Utiliser des modules externes

Les modules externes sont créés par la communauté et peuvent être installés via le gestionnaire de paquets **pip**. Parmi les modules externes populaires, on trouve :

- `pandas` : pour la manipulation et l’analyse de données tabulaires.
- `numpy` : pour les calculs numériques avancés.
- `matplotlib` : pour la création de graphiques.

Ces modules ne sont pas inclus par défaut et doivent être installés manuellement :
```bash
pip install pandas numpy matplotlib
```

## Comment utiliser un module

Pour utiliser un module, il faut d’abord l’importer dans votre script Python. Voici quelques manières d’importer un module :

### 1. Importer le module entier
```python
import math

# Utilisation de la fonction sqrt() du module math
resultat = math.sqrt(16)
print(resultat)
```

### 2. Importer une fonction spécifique
```python
from math import sqrt

# Utilisation de la fonction sqrt() sans préfixer le nom du module
resultat = sqrt(16)
print(resultat)
```

### 3. Importer un module avec un alias
```python
import math as m

# Utilisation de l'alias m pour appeler la fonction sqrt()
resultat = m.sqrt(16)
print(resultat)
```

### 4. Importer plusieurs éléments
```python
from math import sqrt, pi, sin

# Utilisation des fonctions sqrt, pi et sin
resultat = sqrt(16)
print(resultat)

angle = sin(pi/2)
print(angle)  # Affiche : 1.0
```

## Créer un module personnalisé

Créer un module personnalisé est une excellente façon d'organiser son code. Voici les étapes pour créer et utiliser un module personnalisé.

### Étapes pour créer un module :

1. Créer un fichier Python, par exemple `mon_module.py`.
2. Ajouter des fonctions et des variables à ce fichier.
3. Importer ce module dans votre script principal.

### Exemple de création d'un module `mon_module.py` :
```python
# mon_module.py
PI = 3.14159

def carre(x):
    return x ** 2

def aire_cercle(rayon):
    return PI * rayon ** 2
```

### Utilisation du module dans un script principal :
```python
import mon_module

# Utilisation des fonctions et variables du module
print(mon_module.PI)  # 3.14159
print(mon_module.carre(4))  # 16
print(mon_module.aire_cercle(3))  # 28.27431
```

## Exemple de fonctions pour les data analysts

Voici quelques exemples de fonctions que vous pourriez inclure dans vos propres modules pour l’analyse de données.

### Exemple de module `analyse.py` :
```python
# analyse.py
def moyenne(liste):
    return sum(liste) / len(liste)

def ecart_type(liste):
    moy = moyenne(liste)
    variance = sum((x - moy) ** 2 for x in liste) / len(liste)
    return variance ** 0.5

def normaliser(liste):
    min_val = min(liste)
    max_val = max(liste)
    return [(x - min_val) / (max_val - min_val) for x in liste]
```

### Utilisation des fonctions d'analyse dans un script :
```python
import analyse

# Liste des données de CP des Pokémon
donnees_pokemon = [45, 60, 80, 90, 110, 130]

# Calcul de la moyenne et de l'écart-type
print(analyse.moyenne(donnees_pokemon))  # Moyenne des CP

print(analyse.ecart_type(donnees_pokemon))  # Écart-type des CP

# Normalisation des données de CP
donnees_normalisees = analyse.normaliser(donnees_pokemon)
print(donnees_normalisees)  # CP normalisés
```

## Ressources supplémentaires

Pour aller plus loin dans l'utilisation des modules en Python, voici quelques ressources utiles :

- [Python Modules - W3Schools](https://www.w3schools.com/python/python_modules.asp)
- [Python Tutorial for Beginners](https://www.youtube.com/watch?v=CqvZ3vGoGs0)
- [Python #8 - Modularité](https://www.youtube.com/watch?v=A2aD4eQP0qU)

## Conclusion

Les modules sont essentiels dans le développement Python, notamment pour l’analyse de données. Ils permettent de structurer le code, de réutiliser des fonctions, et d'intégrer facilement des bibliothèques externes pour accomplir des tâches complexes. La maîtrise de l’importation, de l’utilisation, et de la création de modules personnalisés est une compétence clé pour tout analyste de données.

[⬅ Page Précédente](../README.md)
