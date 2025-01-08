[⬅ Page Précédente](../README.md)

# Commenter et déboguer son code en Python

## Introduction

Le code Python, comme tout code informatique, peut rapidement devenir complexe et difficile à comprendre si les étapes ne sont pas bien expliquées. C'est pourquoi il est crucial d'apprendre à commenter son code et à le déboguer efficacement. Dans cette fiche, on s’intéresse à la manière de rendre son code lisible et facilement compréhensible par d’autres, tout en expliquant comment déboguer et structurer un code clair et fonctionnel. Ces pratiques permettent non seulement de travailler plus efficacement en équipe mais aussi de retrouver rapidement ses repères lorsqu'on revient sur un projet après un certain temps.

## Sommaire

- [Commenter son code](#commenter-son-code)
- [Déboguer son code en Python](#déboguer-son-code-en-python)
- [Exemple de code détaillé](#exemple-de-code-détaillé)

---

## Commenter son code

Commenter son code est une des pratiques les plus importantes dans la programmation, surtout lorsqu'on travaille en équipe ou qu'on souhaite revenir sur un projet plus tard. Un code bien commenté facilite la compréhension des autres développeurs, tout en aidant le programmeur à se rappeler de sa logique quelques mois après.

### Pourquoi commenter son code ?

1. **Facilite la lecture et la compréhension** : Un code peut paraître évident à l'auteur, mais il peut être difficile à comprendre pour un autre développeur. Les commentaires permettent de clarifier les intentions derrière le code et d'expliquer des choix spécifiques.
   
2. **Gain de temps pour les autres développeurs** : Si on travaille en équipe, les autres auront moins de difficultés à comprendre ce qu'on a fait et pourront ainsi reprendre le projet plus rapidement.

3. **Améliore la relecture du code** : Lorsqu'on revient sur un projet après un certain temps, les commentaires permettent de se rappeler pourquoi certaines décisions ont été prises.

### Bonnes pratiques pour commenter son code

- **Commenter les parties complexes** : Si une section de code est difficile à comprendre ou utilise une logique particulière, explique-la.
- **Expliquer les variables importantes** : Mentionner ce que chaque variable représente, surtout quand leur nom ne le décrit pas de façon évidente.
- **Eviter les commentaires redondants** : Ne commenter pas des choses évidentes, comme l'ajout de 1 à une variable. Se concentrer sur l'explication du raisonnement derrière des opérations complexes.
  
Voici un exemple de code commenté :

```python
# Initialisation de la liste des Pokémons capturés
pokemons = ['Pikachu', 'Salamèche', 'Bulbizarre']

# Ajout du suffixe « Capturé » à chaque nom de Pokémon
pokemons_captures = [f"{nom} Capturé" for nom in pokemons]

# Affichage des Pokémons avec leur état
print(pokemons_captures)
```

Dans cet exemple, chaque étape est expliquée pour éviter toute confusion.

---

## Déboguer son code en Python

Le débogage consiste à identifier et corriger les erreurs dans un programme. Les erreurs peuvent être de différents types : erreurs de syntaxe, erreurs logiques, ou encore des erreurs d'exécution. Voici les étapes de base pour déboguer du code Python.

### 1. **Lire les messages d'erreur**

Lorsque Python rencontre un problème, il génère un message d'erreur. Ce message donne des indices sur l'endroit et la nature du problème. Par exemple, une erreur courante pourrait être :

```python
# Erreur typique : une variable n'est pas définie
print(pokemon)
```

**Message d'erreur** : `NameError: name 'pokemon' is not defined`.

Dans ce cas, l'erreur indique que la variable `pokemon` n'a pas été définie avant d'être utilisée.

### 2. **Utiliser les outils de débogage**

Python dispose de nombreux outils pour faciliter le débogage, notamment la fonction `print()` pour afficher l’état des variables ou `pdb`, qui permet de mettre des points d'arrêt dans le code.

Voici un exemple de débogage avec `print()` :

```python
def attaque_pokemon(pokemon, puissance):
    print(f"Pokémon = {pokemon}, Puissance = {puissance}")  # Affiche les valeurs
    return f"{pokemon} inflige {puissance} points de dégâts !"

resultat = attaque_pokemon("Dracaufeu", 90)
print(resultat)
```

Dans cet exemple, on peut suivre les valeurs des variables avant qu'elles ne soient utilisées dans la fonction.

### 3. **Utiliser un débogueur**

Le module `pdb` de Python permet de mettre des points d'arrêt dans le code et d’inspecter les valeurs des variables à différents endroits du programme.

```python
import pdb

def evolution_pokemon(pokemon, niveau):
    pdb.set_trace()  # Déclenche l'arrêt à ce point
    if niveau >= 16:
        return f"{pokemon} évolue !"
    return f"{pokemon} n'est pas encore prêt pour évoluer."

resultat = evolution_pokemon("Reptincel", 14)
```

Une fois le programme en pause à l'instruction `pdb.set_trace()`, on peut interagir avec le programme, inspecter les variables et avancer étape par étape dans le code.

---

## Exemple de code détaillé

Imaginons que l'on souhaite créer une fonction qui prédit si un Pokémon peut remporter un combat en fonction de ses points d’attaque et de défense. On va utiliser un modèle simple de Machine Learning pour faire cette prédiction.

### 1. **Préparer les données**

Le jeu de données contient les informations suivantes :

- Points d’attaque (`attaque`)
- Points de défense (`defense`)
- Résultat du combat (`victoire` : 1 pour victoire, 0 pour défaite)

```python
import pandas as pd

# Création du DataFrame
data = {
    'attaque': [55, 70, 120, 60, 90],
    'defense': [40, 65, 85, 50, 75],
    'victoire': [0, 1, 1, 0, 1]
}

df = pd.DataFrame(data)
```

### 2. **Préparer les données pour le modèle**

On va séparer les caractéristiques (attaque et défense) de l’étiquette (résultat du combat).

```python
X = df[['attaque', 'defense']]  # Les caractéristiques
y = df['victoire']  # L'étiquette
```

### 3. **Créer et entraîner le modèle**

On va utiliser un modèle de régression logistique pour prédire l'issue du combat.

```python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score

# Séparation des données en ensemble d'entraînement et de test
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Création du modèle
modele = LogisticRegression()

# Entraînement du modèle
modele.fit(X_train, y_train)
```

### 4. **Faire une prédiction**

Une fois que le modèle est entraîné, on peut prédire l'issue d'un combat pour un nouveau Pokémon.

```python
# Données de test pour la prédiction
nouveau_pokemon = [[110, 70]]  # Attaque de 110 et défense de 70

# Prédiction
prediction = modele.predict(nouveau_pokemon)
print(f"Victoire probable : {'Oui' if prediction[0] == 1 else 'Non'}")
```

### Explication des étapes :

- **Données d'entrée** : Les points d'attaque et de défense sont utilisés pour prédire le résultat.
- **Modèle** : La régression logistique est adaptée pour des tâches de classification binaire (victoire/défaite).
- **Prédiction** : Le modèle prédit si un Pokémon a des chances de remporter le combat.

---

## Conclusion

Documenter son code et savoir le déboguer efficacement sont des compétences essentielles pour tout développeur. En expliquant bien son raisonnement, on s'assure que d'autres développeurs pourront comprendre et reprendre le travail plus facilement. Le débogage, quant à lui, permet de corriger les erreurs et d’optimiser le code. Ces bonnes pratiques permettent de travailler plus sereinement, que ce soit seul ou en équipe.

---

### Ressources supplémentaires :

- [Python - Debugging with pdb](https://docs.python.org/3/library/pdb.html)
- [Commenter son code en Python - Guide complet](https://realpython.com/python-comments-guide/)

[⬅ Page Précédente](../README.md)

