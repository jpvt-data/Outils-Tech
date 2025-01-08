[⬅ Page Précédente](../README.md)

# Python - Les Listes

## Introduction

Les listes en Python sont l'un des types de données les plus utilisés, car elles offrent une flexibilité et une richesse fonctionnelle élevées. Elles permettent de stocker des éléments sous forme de séquence, ce qui facilite la gestion et la manipulation de données variées. Contrairement aux chaînes de caractères (strings), les listes sont **mutables**, c'est-à-dire qu'on peut modifier leur contenu après leur création. Cela les rend particulièrement adaptées à de nombreuses situations où il est nécessaire de travailler avec des ensembles de données évolutifs.

Les listes peuvent contenir tout type d'objet : des nombres, des chaînes de caractères, des objets, voire d'autres listes. Cette polyvalence permet de résoudre une multitude de problèmes dans le développement de logiciels.

---

## Créer une Liste

En Python, une liste se crée en entourant les éléments avec des crochets `[ ]`. Les éléments à l'intérieur de la liste sont séparés par des virgules.

### Exemple :

```python
pokemons = ["Pikachu", "Bulbizarre", "Salamèche"]
print(pokemons)
```

**Explication :**
Ici, `pokemons` est une liste contenant trois noms de Pokémon. La méthode `print()` affiche la liste dans la sortie.

---

## Accéder aux Éléments d'une Liste

On peut accéder aux éléments d’une liste en utilisant des indices. Python utilise un système d'indexation qui commence à 0.

### Exemple :

```python
pokemons = ["Pikachu", "Bulbizarre", "Salamèche"]
print(pokemons[0])  # Accède au premier élément
```

**Explication :**
`pokemons[0]` accède au premier élément de la liste, "Pikachu". Si l’on souhaite accéder au dernier élément, on peut utiliser un indice négatif :

```python
print(pokemons[-1])  # Accède au dernier élément ("Salamèche")
```

---

## Modifier les Éléments d'une Liste

Les listes étant mutables, il est possible de modifier un ou plusieurs éléments après leur création.

### Exemple :

```python
pokemons = ["Pikachu", "Bulbizarre", "Salamèche"]
pokemons[1] = "Carapuce"  # Remplace l'élément à l'index 1 par "Carapuce"
print(pokemons)
```

**Explication :**
L'élément à l'index 1 (qui était "Bulbizarre") est remplacé par "Carapuce". Résultat : `["Pikachu", "Carapuce", "Salamèche"]`.

---

## Itérer sur une Liste

L'itération sur une liste permet de parcourir chaque élément, souvent pour effectuer une opération sur chaque valeur.

### Exemple :

```python
pokemons = ["Pikachu", "Bulbizarre", "Salamèche"]
for pokemon in pokemons:
    print(pokemon)
```

**Explication :**
Le `for` permet de parcourir chaque élément de la liste. Résultat affiché :

```
Pikachu
Bulbizarre
Salamèche
```

---

## Ajouter ou Supprimer des Éléments dans une Liste

### Ajouter un élément à la fin d'une liste

Pour ajouter un élément à la fin d'une liste, on utilise la méthode `append()`.

### Exemple :

```python
pokemons = ["Pikachu", "Bulbizarre"]
pokemons.append("Évoli")  # Ajoute "Évoli" à la fin
print(pokemons)
```

**Explication :**
L’élément "Évoli" est ajouté à la fin de la liste. Résultat : `["Pikachu", "Bulbizarre", "Évoli"]`.

### Supprimer un élément d'une liste

Pour supprimer un élément, on utilise la méthode `remove()`, qui supprime la première occurrence de l’élément donné.

### Exemple :

```python
pokemons = ["Pikachu", "Évoli", "Bulbizarre"]
pokemons.remove("Évoli")  # Supprime "Évoli"
print(pokemons)
```

**Explication :**
L'élément "Évoli" est supprimé de la liste. Résultat : `["Pikachu", "Bulbizarre"]`.

---

## Listes Imbriquées

Les listes peuvent contenir d'autres listes, formant des structures à plusieurs dimensions, comme les matrices.

### Exemple :

```python
pokedex = [["Pikachu", "Électrique"], ["Salamèche", "Feu"], ["Bulbizarre", "Plante"]]
print(pokedex[1][0])  # Accède au Pokémon "Salamèche"
```

**Explication :**
La liste `pokedex` contient trois sous-listes. L'élément `pokedex[1][0]` accède à "Salamèche".

---

## Résumé des Concepts

| Concept              | Description                                           | Exemple                                 |
|----------------------|-------------------------------------------------------|-----------------------------------------|
| Création d'une liste | Créer une liste avec des éléments séparés par des virgules | `pokemons = ["Pikachu", "Évoli"]`      |
| Accès aux éléments   | Accéder aux éléments via un indice (indexation commence à 0) | `pokemons[1]` (accède à "Évoli")        |
| Modification         | Modifier un élément d'une liste à un index spécifique | `pokemons[0] = "Carapuce"`             |
| Itération            | Parcourir une liste avec une boucle `for`              | `for pokemon in pokemons:`             |
| Ajouter un élément   | Ajouter un élément à la fin d'une liste avec `append()` | `pokemons.append("Bulbizarre")`        |
| Supprimer un élément | Supprimer un élément avec `remove()`                   | `pokemons.remove("Évoli")`            |
| Listes imbriquées    | Utiliser des listes à plusieurs dimensions             | `pokedex[0][1]`                        |

---

## Ressources Complémentaires

- [Comment itérer sur une liste ?](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/)
- [Les listes Python - python doctor](https://python.doctor/page-apprendre-listes-list-tableaux-tableaux-liste-array-python-cours-debutant)
- [Sélectionner les données dans une liste](https://railsware.com/blog/python-for-machine-learning-indexing-and-slicing-for-lists-tuples-strings-and-other-sequential-types/)
- [Python Lists - W3School](https://www.w3schools.com/python/python_lists.asp)

[⬅ Page Précédente](../README.md)