# Python - Les Listes

## Introduction

Les listes en Python sont l'un des types de données les plus utilisés, car elles offrent une flexibilité et une richesse fonctionnelle élevées. Elles permettent de stocker des éléments sous forme de séquence, ce qui facilite la gestion et la manipulation de données variées. Contrairement aux chaînes de caractères (strings), les listes sont **mutables**, c'est-à-dire qu'on peut modifier leur contenu après leur création. Cela les rend particulièrement adaptées à de nombreuses situations où il est nécessaire de travailler avec des ensembles de données évolutifs.

Cette fiche technique aborde les bases des listes en Python : leur création, la manipulation des éléments, l'itération, ainsi que des exemples pratiques d’utilisation.

Les listes sont une structure de données fondamentale qui peut contenir tout type d'objet : des nombres, des chaînes de caractères, des objets, voire d'autres listes. Cette polyvalence permet de résoudre une multitude de problèmes dans le développement de logiciels.

### Utilisation des Listes

Les listes en Python peuvent être utilisées dans divers contextes, notamment :
- Stocker des séries de valeurs de manière ordonnée.
- Manipuler des collections de données (tri, modification, insertion).
- Appliquer des algorithmes de traitement sur des ensembles d'éléments (par exemple, calculs sur des données numériques, extraction d'informations spécifiques).

---

## Créer une Liste

En Python, une liste se crée en entourant les éléments avec des crochets `[ ]`. Les éléments à l'intérieur de la liste sont séparés par des virgules.

### Exemple :

```python
ma_liste = [10, 20, 30, 40]
print(ma_liste)
```

**Explication :**  
Ici, `ma_liste` est une liste contenant quatre éléments numériques. La méthode `print()` affiche la liste dans la sortie.

### Pourquoi faire ça ?

La création d’une liste est la première étape pour organiser des données de manière séquentielle. En Python, les listes sont flexibles, et on peut y ajouter ou retirer des éléments facilement.

---

## Accéder aux Éléments d'une Liste

On peut accéder aux éléments d’une liste en utilisant des indices. Python utilise un système d'indexation qui commence à 0.

### Exemple :

```python
ma_liste = ["Léon", "René", "Bernard"]
print(ma_liste[0])  # Accède au premier élément
```

**Explication :**  
Ici, `ma_liste[0]` accède au premier élément de la liste, "Léon". Si l’on souhaite accéder au dernier élément, il est aussi possible d’utiliser un indice négatif, comme suit :

```python
print(ma_liste[-1])  # Accède au dernier élément ("Bernard")
```

### Pourquoi faire ça ?

L'accès aux éléments d’une liste permet d'interagir avec des données spécifiques, que ce soit pour les afficher, les modifier, ou les analyser.

---

## Modifier les Éléments d'une Liste

Les listes étant mutables, il est possible de modifier un ou plusieurs éléments après la création de la liste.

### Exemple :

```python
ma_liste = [1, 2, 3, 4]
ma_liste[2] = 10  # Remplace l'élément à l'index 2 par 10
print(ma_liste)
```

**Explication :**  
Ici, l'élément à l'index 2 (qui était 3) est remplacé par 10. Le résultat est donc `[1, 2, 10, 4]`.

### Pourquoi faire ça ?

Cela permet de mettre à jour les valeurs d’une liste à mesure que le programme progresse, par exemple dans un algorithme de calcul, ou lors de la modification d'un état de données.

---

## Itérer sur une Liste

L'itération sur une liste permet de parcourir chaque élément, souvent pour effectuer une opération sur chaque valeur.

### Exemple :

```python
ma_liste = ["Léon", "René", "Bernard"]
for nom in ma_liste:
    print(nom)
```

**Explication :**  
Le `for` permet de parcourir chaque élément de la liste, ici chaque nom de la liste est imprimé à l'écran. Le résultat affichera :

```
Léon
René
Bernard
```

### Pourquoi faire ça ?

L'itération est essentielle lorsqu'on souhaite appliquer une opération sur chaque élément d'une liste (par exemple, calculer une somme, rechercher un élément particulier, etc.).

---

## Ajouter ou Supprimer des Éléments dans une Liste

### Ajouter un élément à la fin d'une liste

Pour ajouter un élément à la fin d'une liste, on utilise la méthode `append()`.

### Exemple :

```python
ma_liste = [1, 2, 3]
ma_liste.append(4)  # Ajoute 4 à la fin
print(ma_liste)
```

**Explication :**  
L’élément 4 est ajouté à la fin de la liste. Résultat : `[1, 2, 3, 4]`.

### Supprimer un élément d'une liste

Pour supprimer un élément, on utilise la méthode `remove()`, qui supprime la première occurrence de l’élément donné.

### Exemple :

```python
ma_liste = [1, 2, 3, 4]
ma_liste.remove(3)  # Supprime le premier élément égal à 3
print(ma_liste)
```

**Explication :**  
L'élément 3 est supprimé de la liste, et le résultat sera `[1, 2, 4]`.

### Pourquoi faire ça ?

Les méthodes `append()` et `remove()` permettent de gérer dynamiquement le contenu d’une liste, en ajoutant ou retirant des éléments selon les besoins du programme.

---

## Manipuler des Listes de Niveaux Multiples

Les listes peuvent contenir d'autres listes, formant des structures à plusieurs dimensions, comme les matrices.

### Exemple :

```python
ma_liste_2D = [[1, 2], [3, 4], [5, 6]]
print(ma_liste_2D[1][0])  # Accède à l'élément "3"
```

**Explication :**  
Ici, la liste `ma_liste_2D` contient trois sous-listes. L'élément `ma_liste_2D[1][0]` accède à l’élément à l’index `[1][0]`, qui est le nombre 3.

### Pourquoi faire ça ?

Cela permet de gérer des structures de données complexes, comme des matrices, utiles dans des domaines comme les calculs mathématiques, le traitement d’images ou la manipulation de bases de données à plusieurs dimensions.

---

### Résumé des Concepts

| Concept              | Description                                           | Exemple                                 |
|----------------------|-------------------------------------------------------|-----------------------------------------|
| Création d'une liste | Créer une liste avec des éléments séparés par des virgules | `ma_liste = [10, 20, 30]`              |
| Accès aux éléments   | Accéder aux éléments via un indice (indexation commence à 0) | `ma_liste[1]` (accède au deuxième élément) |
| Modification         | Modifier un élément d'une liste à un index spécifique | `ma_liste[0] = 99`                     |
| Itération            | Parcourir une liste avec une boucle `for`              | `for element in ma_liste:`             |
| Ajouter un élément   | Ajouter un élément à la fin d'une liste avec `append()` | `ma_liste.append(40)`                  |
| Supprimer un élément | Supprimer un élément avec `remove()`                   | `ma_liste.remove(20)`                  |
| Listes imbriquées    | Utiliser des listes à plusieurs dimensions             | `ma_liste_2D[0][1]`                    |

---

## Ressources Complémentaires

- [Comment itérer sur une list ?](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/)
- [Les listes Python - python doctor](https://python.doctor/page-apprendre-listes-list-tableaux-tableaux-liste-array-python-cours-debutant)
- [Sélectionner les données dans une liste](https://railsware.com/blog/python-for-machine-learning-indexing-and-slicing-for-lists-tuples-strings-and-other-sequential-types/)
- [Python Lists - W3School](https://www.w3schools.com/python/python_lists.asp)

---


