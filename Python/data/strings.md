# Python - Strings : Manipuler les chaînes de caractères

## Introduction

Les chaînes de caractères, ou *strings* en anglais, sont un des types de données les plus utilisés en Python. Elles représentent une séquence ordonnée de caractères, qui peuvent être des lettres, des chiffres, des espaces, des signes de ponctuation, des emojis, des symboles ou même des caractères invisibles.

Manipuler des chaînes de caractères est essentiel lors de la programmation, notamment pour la gestion des textes, la création de rapports ou l'extraction de données.

Cette fiche technique a pour objectif de vous apprendre à manipuler les chaînes de caractères en Python en vous donnant une vue d'ensemble de leur fonctionnement et des principales opérations possibles.

## Sommaire

1. [Les chaînes de caractères : Qu'est-ce que c'est ?](#les-chaînes-de-caractères-qu'est-ce-que-c'est)
2. [Sélectionner des caractères dans une chaîne](#sélectionner-des-caractères-dans-une-chaîne)
3. [Les chaînes de caractères sont immuables](#les-chaînes-de-caractères-sont-immuables)
4. [Quelques détails supplémentaires sur les chaînes](#quelques-détails-supplémentaires-sur-les-chaînes)
5. [Ressources supplémentaires](#ressources-supplémentaires)

## Les chaînes de caractères : Qu'est-ce que c'est ?

Une chaîne de caractères est un ensemble de caractères contenus dans une variable de type `str` (string). C'est un type de données fondamental en Python et très utilisé dans la programmation. Chaque chaîne est un objet, ce qui signifie qu'elle dispose de méthodes associées permettant de la manipuler de manière simple et puissante.

### Exemple :

```python
chaine = "Pikachu, Attrapez-les tous !"
```

Dans cet exemple, `chaine` est une variable de type chaîne de caractères, contenant la phrase "Pikachu, Attrapez-les tous !".

## Sélectionner des caractères dans une chaîne

Les chaînes en Python sont indexées, c'est-à-dire que chaque caractère possède une position spécifique. L'indexation commence à 0 pour le premier caractère et va jusqu'à la longueur de la chaîne moins 1. Python permet aussi d'utiliser des indices négatifs pour accéder aux caractères en partant de la fin de la chaîne.

### Indexation des caractères

```python
s = "Bulbizarre"

# Premier caractère
print(s[0])  # B

# Dernier caractère (index négatif)
print(s[-1])  # e

# Accéder au troisième caractère
print(s[2])  # l
```

### Slicing (extraire une sous-chaîne)

Le slicing permet de sélectionner une portion de la chaîne en utilisant une syntaxe comme `s[start:end]`. L'indice `start` est inclus, mais l'indice `end` est exclusif.

```python
# Exemple de slicing
s = "Bulbizarre"

# Extraire les caractères entre l'indice 0 et 2 (inclus)
print(s[0:3])  # Bul

# Extraire depuis le début jusqu'à l'indice 3
print(s[:4])  # Bulb

# Extraire depuis l'indice 2 jusqu'à la fin
print(s[2:])  # lbizarre

# Extraire toute la chaîne
print(s[:])  # Bulbizarre
```

## Les chaînes de caractères sont immuables

En Python, les chaînes de caractères sont immuables, ce qui signifie qu'une fois créées, elles ne peuvent pas être modifiées. Essayer de modifier directement un caractère d'une chaîne entraînera une erreur.

### Exemple d'erreur :

```python
s = "Salamèche"
s[0] = "s"  # Erreur : TypeError
```

Cependant, il est possible de créer une nouvelle chaîne en modifiant une partie de la chaîne initiale. Cela peut se faire avec des méthodes comme `.replace()`.

### Exemple avec `.replace()` :

```python
s = "Salamèche"
nouvelle_s = s.replace("S", "s")
print(nouvelle_s)  # salamèche
```

Ici, la méthode `.replace()` crée une nouvelle chaîne où toutes les occurrences de "S" sont remplacées par "s". La chaîne `s` reste inchangée.

## Quelques détails supplémentaires sur les chaînes

- **Chaîne vide :** Une chaîne peut être vide, ce qui est représenté par `""`.

  ```python
  chaine_vide = ""
  print(len(chaine_vide))  # 0
  ```

- **Concaténation de chaînes :** Les chaînes peuvent être combinées à l'aide de l'opérateur `+` :

  ```python
  a = "Carapuce"
  b = "Roucool"
  c = a + " et " + b  # "Carapuce et Roucool"
  print(c)
  ```

- **Multiplication de chaînes :** Il est aussi possible de répéter une chaîne plusieurs fois avec l'opérateur `*` :

  ```python
  a = "Pokémon "
  print(a * 3)  # Pokémon Pokémon Pokémon
  ```

## Ressources supplémentaires

Pour aller plus loin dans la manipulation des chaînes de caractères en Python, voici quelques ressources utiles :

- [Documentation officielle Python - Chaînes de caractères](https://docs.python.org/fr/3/tutorial/introduction.html#strings)
- [Méthodes des chaînes en Python](https://python.developpez.com/faq/?page=String)
- [Opérations courantes sur les chaînes](https://www.w3schools.com/python/python_strings.asp)

