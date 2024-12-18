[⬅ Retour à Python](../README.md)

# Introduction à Python

## Pourquoi utiliser Python ?

Python est un langage de programmation populaire, particulièrement apprécié pour sa simplicité et sa puissance. Sa syntaxe claire et intuitive le rend idéal pour les débutants tout en étant suffisamment puissant pour des applications complexes. Python est largement utilisé dans des domaines variés comme la science des données, le développement web, l'automatisation, et bien d'autres. Apprendre à manipuler des variables est l'une des premières étapes pour explorer toutes les possibilités offertes par Python.

## Les Caractéristiques de Python

Python se distingue par plusieurs aspects :
- **Simplicité** : Python est un langage facile à lire et à écrire, idéal pour les débutants.
- **Langage interprété** : Le code est exécuté ligne par ligne, facilitant le débogage et le développement rapide.
- **Typage dynamique** : Le type des variables est déterminé automatiquement par leur valeur.
- **Portabilité** : Python fonctionne sur tous les principaux systèmes d'exploitation.
- **Extensibilité** : Grâce à ses bibliothèques, Python permet de réaliser des projets de toutes tailles.

---

# Variables & Types de données

## Introduction

Les variables sont des éléments clés de tout langage de programmation. En Python, elles sont utilisées pour stocker des valeurs qui peuvent être manipulées tout au long du programme. Comprendre la déclaration, l’utilisation et la gestion des variables en Python est essentiel pour bien démarrer en programmation. Cette fiche explique de manière détaillée ce que sont les variables, comment les manipuler et les utiliser dans des situations courantes. 

Les variables permettent de rendre un programme flexible, car elles stockent des informations et permettent de les réutiliser ou de les modifier au besoin.

## Objectifs

À l'issue de cette fiche, il sera possible de :
- Comprendre ce qu'est une variable et son rôle en Python.
- Identifier les différents types de variables en Python.
- Déclarer et manipuler des variables efficacement.
- Vérifier le type d'une variable.
- Convertir une variable d'un type à un autre (cast).
- Interagir avec l'utilisateur via les entrées/sorties.

## Définition d'une Variable

Une variable en Python est un espace mémoire qui contient une valeur. Cette valeur peut être un nombre, un texte, ou d'autres types de données. Le nom de la variable est une étiquette qui permet d'accéder à cette valeur en mémoire. Il est possible de modifier la valeur d'une variable au cours de l'exécution du programme.

### Types de Variables en Python

Python prend en charge différents types de variables :
- **int** : Entiers, par exemple 5, -3, 1000.
- **float** : Nombres à virgule flottante, par exemple 3.14, -0.5, 2.0.
- **str** : Chaînes de caractères, par exemple 'bonjour', "Python".
- **bool** : Valeurs booléennes, soit `True` (vrai), soit `False` (faux).

## Déclaration et Nommage des Variables

### Déclaration

Pour déclarer une variable en Python, il suffit de lui assigner une valeur avec le symbole `=`. Par exemple :

```python
age = 25
```

Ici, la variable `age` contient la valeur `25`.

### Règles de Nommage

En Python, il est recommandé d'utiliser la convention **snake_case** pour nommer les variables, c'est-à-dire de séparer les mots par des underscores (`_`) et d’utiliser uniquement des lettres minuscules. Par exemple :
- `nom_utilisateur`
- `salaire_annuel`

Il est important de noter que les noms de variables ne peuvent pas commencer par un chiffre et ne doivent pas être des mots réservés en Python, comme `int`, `str`, `print`, etc.

## Exemple : Calcul du Salaire Mensuel

Voici un exemple simple pour démontrer comment manipuler les variables en Python :

```python
# Déclaration des variables
salaire_annuel = 36000  # Le salaire annuel en euros
nb_mois = 12            # Le nombre de mois dans une année

# Calcul du salaire mensuel
salaire_mensuel = salaire_annuel / nb_mois

# Affichage du salaire mensuel
print("Le salaire mensuel est de", salaire_mensuel, "euros.")
```

### Explication de l'exemple
- **salaire_annuel** et **nb_mois** sont des variables de type `int` contenant respectivement le salaire annuel et le nombre de mois dans une année.
- **salaire_mensuel** est calculé en divisant **salaire_annuel** par **nb_mois**.
- La fonction `print()` affiche le résultat.

## Vérifier le Type d'une Variable

Il peut être utile de vérifier le type d'une variable, surtout lorsqu'on manipule des données provenant de sources externes. La fonction `type()` permet de vérifier le type d'une variable. Par exemple :

```python
salaire_annuel = 40000
prenom = 'Lionel'

print(type(salaire_annuel))  # Affiche <class 'int'>
print(type(prenom))          # Affiche <class 'str'>
```

### Explication
- `type(salaire_annuel)` renvoie `<class 'int'>`, indiquant que `salaire_annuel` est un entier.
- `type(prenom)` renvoie `<class 'str'>`, indiquant que `prenom` est une chaîne de caractères.

## Changer le Type d'une Variable (Casting)

Parfois, il est nécessaire de convertir une variable d’un type à un autre. Cela s'appelle le **casting**. Par exemple, si on veut convertir une chaîne de caractères en entier, on peut utiliser `int()` :

```python
# Conversion d'une chaîne de caractères en entier
age_str = "25"
age_int = int(age_str)  # age_int devient un entier de valeur 25
```

Il est aussi possible de convertir des entiers en chaînes ou des nombres en flottants. Voici un exemple de conversion :

```python
# Conversion d'un entier en chaîne
salaire_annuel = 36000
salaire_str = str(salaire_annuel)

# Conversion d'un entier en flottant
age_int = 30
age_flottant = float(age_int)  # age_flottant devient 30.0
```

### Explication du Casting
- **int()** : Convertit une chaîne ou un flottant en entier.
- **str()** : Convertit n'importe quel type de variable en une chaîne de caractères.
- **float()** : Convertit une chaîne ou un entier en un flottant.

Il est important de noter que certaines conversions peuvent échouer, par exemple convertir une chaîne comme `"abc"` en entier entraînera une erreur.

## Gérer les Entrées/Sorties

### Entrée Utilisateur

En Python, pour demander une entrée à l'utilisateur, on utilise la fonction `input()`. Elle permet de capturer une saisie clavier. Par exemple :

```python
nom = input("Quel est ton nom ? ")
print("Bonjour,", nom, "!")
```

### Sortie Utilisateur

Pour afficher des informations à l'utilisateur, on utilise la fonction `print()`. Par exemple, l'exemple ci-dessus affiche le message "Bonjour, [nom] !".

### Explication des Entrées/Sorties
- **input()** : Capture une saisie clavier de l'utilisateur.
- **print()** : Affiche un message ou une valeur sur l'écran.

## Conclusion

Comprendre les variables en Python et leur gestion est essentiel pour écrire des programmes efficaces. Les variables permettent de stocker, manipuler et afficher des données dans un programme. À travers des exemples simples, on a vu comment déclarer, manipuler, vérifier et convertir des variables. Ces notions sont essentielles pour aborder des concepts plus complexes en programmation Python.

## Ressources

- [Python Documentation - Variables](https://docs.python.org/3/tutorial/introduction.html#using-python-as-a-calculator)
- [Python Type Conversion](https://www.w3schools.com/python/ref_func_int.asp)
```
