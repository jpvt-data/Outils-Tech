[⬅ Retour à Python](../README.md)

# Variables & Types de données

## Introduction

Les variables sont des éléments clés de tout langage de programmation. En Python, elles sont utilisées pour stocker des valeurs qui peuvent être manipulées tout au long du programme. Comprendre la déclaration, l’utilisation et la gestion des variables en Python est essentiel pour bien démarrer en programmation. Cette fiche explique de manière détaillée ce que sont les variables, comment les manipuler et les utiliser dans des situations courantes.

Les variables permettent de rendre un programme flexible, car elles stockent des informations et permettent de les réutiliser ou de les modifier au besoin.

## Définition d'une Variable

Une variable en Python est un espace mémoire qui contient une valeur. Cette valeur peut être un nombre, un texte, ou d'autres types de données. Le nom de la variable est une étiquette qui permet d'accéder à cette valeur en mémoire. Il est possible de modifier la valeur d'une variable au cours de l'exécution du programme.

### Types de Variables en Python

Python prend en charge différents types de variables :
- **int** : Entiers, par exemple 25 (nombre de Poké Balls), 150 (nombre de Pokémon capturés).
- **float** : Nombres à virgule flottante, par exemple 1.5 (taille moyenne d’un Pikachu en mètres), 52.4 (poids d'un Onix en kg).
- **str** : Chaînes de caractères, par exemple 'Bulbizarre', "Sacha".
- **bool** : Valeurs booléennes, soit `True` (vrai), soit `False` (faux).

## Déclaration et Nommage des Variables

### Déclaration

Pour déclarer une variable en Python, il suffit de lui assigner une valeur avec le symbole `=`. Par exemple :

```python
niveau_pikachu = 25
```

Ici, la variable `niveau_pikachu` contient la valeur `25`.

### Règles de Nommage

En Python, il est recommandé d'utiliser la convention **snake_case** pour nommer les variables, c'est-à-dire de séparer les mots par des underscores (`_`) et d’utiliser uniquement des lettres minuscules. Par exemple :
- `nom_pokemon`
- `points_experience`

Il est important de noter que les noms de variables ne peuvent pas commencer par un chiffre et ne doivent pas être des mots réservés en Python, comme `int`, `str`, `print`, etc.

## Exemple : Calcul de l'Expérience Moyenne par Pokémon

Voici un exemple simple pour démontrer comment manipuler les variables en Python :

```python
# Déclaration des variables
experience_totale = 1250  # Expérience totale gagnée dans un combat
nombre_pokemons = 5       # Nombre de Pokémon ayant participé au combat

# Calcul de l'expérience moyenne
experience_moyenne = experience_totale / nombre_pokemons

# Affichage de l'expérience moyenne
print("Chaque Pokémon a gagné", experience_moyenne, "points d’expérience.")
```

### Explication de l'exemple
- **experience_totale** et **nombre_pokemons** sont des variables de type `int` contenant respectivement l’expérience totale gagnée et le nombre de Pokémon ayant participé.
- **experience_moyenne** est calculée en divisant **experience_totale** par **nombre_pokemons**.
- La fonction `print()` affiche le résultat.

## Vérifier le Type d'une Variable

Il peut être utile de vérifier le type d'une variable, surtout lorsqu'on manipule des données provenant de sources externes. La fonction `type()` permet de vérifier le type d'une variable. Par exemple :

```python
nom_pokemon = 'Salamèche'
taille_pokemon = 0.6

print(type(nom_pokemon))  # Affiche <class 'str'>
print(type(taille_pokemon))  # Affiche <class 'float'>
```

### Explication
- `type(nom_pokemon)` renvoie `<class 'str'>`, indiquant que `nom_pokemon` est une chaîne de caractères.
- `type(taille_pokemon)` renvoie `<class 'float'>`, indiquant que `taille_pokemon` est un nombre à virgule flottante.

## Changer le Type d'une Variable (Casting)

Parfois, il est nécessaire de convertir une variable d’un type à un autre. Cela s'appelle le **casting**. Par exemple, si on veut convertir une chaîne de caractères en entier, on peut utiliser `int()` :

```python
# Conversion d'une chaîne de caractères en entier
nombre_pokeballs_str = "10"
nombre_pokeballs_int = int(nombre_pokeballs_str)  # nombre_pokeballs_int devient un entier de valeur 10
```

Il est aussi possible de convertir des entiers en chaînes ou des nombres en flottants. Voici un exemple de conversion :

```python
# Conversion d'un entier en chaîne
niveau_pikachu = 25
niveau_str = str(niveau_pikachu)

# Conversion d'un entier en flottant
pv_max = 50
pv_flottant = float(pv_max)  # pv_flottant devient 50.0
```

### Explication du Casting
- **int()** : Convertit une chaîne ou un flottant en entier.
- **str()** : Convertit n'importe quel type de variable en une chaîne de caractères.
- **float()** : Convertit une chaîne ou un entier en un flottant.

Il est important de noter que certaines conversions peuvent échouer, par exemple convertir une chaîne comme `"Bulbizarre"` en entier entraînera une erreur.

## Gérer les Entrées/Sorties

### Entrée Utilisateur

En Python, pour demander une entrée à l'utilisateur, on utilise la fonction `input()`. Elle permet de capturer une saisie clavier. Par exemple :

```python
nom = input("Quel est le nom de ton Pokémon préféré ? ")
print("Super choix !", nom, "est un excellent Pokémon !")
```

### Sortie Utilisateur

Pour afficher des informations à l'utilisateur, on utilise la fonction `print()`. Par exemple, l'exemple ci-dessus affiche le message "Super choix ! [nom] est un excellent Pokémon !".

### Explication des Entrées/Sorties
- **input()** : Capture une saisie clavier de l'utilisateur.
- **print()** : Affiche un message ou une valeur sur l'écran.

## Conclusion

Comprendre les variables en Python et leur gestion est essentiel pour écrire des programmes efficaces. Les variables permettent de stocker, manipuler et afficher des données dans un programme. À travers des exemples simples, on a vu comment déclarer, manipuler, vérifier et convertir des variables. Ces notions sont essentielles pour aborder des concepts plus complexes en programmation Python.

## Ressources

- [Python Documentation - Variables](https://docs.python.org/3/tutorial/introduction.html#using-python-as-a-calculator)
- [Python Type Conversion](https://www.w3schools.com/python/ref_func_int.asp)


