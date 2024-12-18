# Python - Les opérateurs

## Introduction

Les opérateurs en Python sont des éléments essentiels pour effectuer des calculs, comparer des valeurs, ou manipuler des conditions. Apprendre à utiliser les opérateurs est fondamental dans le cadre de la programmation, car ils permettent de manipuler les données de manière logique et mathématique. Cette fiche détaillera les différents types d'opérateurs en Python, leur utilisation, et fournira des exemples concrets pour bien comprendre leur fonctionnement.

## Sommaire

1. [Qu'est-ce qu'un opérateur en Python ?](#qu-est-ce-qu-un-opérateur-en-python)
2. [Les opérateurs arithmétiques](#les-opérateurs-arithmétiques)
3. [Les opérateurs de comparaison](#les-opérateurs-de-comparaison)
4. [Les opérateurs logiques](#les-opérateurs-logiques)

---

### Qu'est-ce qu'un opérateur en Python ?

Un opérateur est un symbole ou un mot réservé qui permet de réaliser une opération sur une ou plusieurs variables ou valeurs. Ces opérations peuvent être mathématiques, logiques ou comparatives. En Python, les opérateurs sont utilisés pour manipuler les données, effectuer des calculs ou prendre des décisions dans un programme.

Voici quelques exemples d'opérateurs :

- `+`, `-`, `*`, `/`, `//`, `%`, `**` (opérateurs arithmétiques)
- `==`, `!=`, `>`, `<`, `>=`, `<=` (opérateurs de comparaison)
- `and`, `or`, `not` (opérateurs logiques)
- `=` (opérateur d'affectation)

### Les opérateurs arithmétiques

Les opérateurs arithmétiques permettent d'effectuer des calculs mathématiques. En Python, voici les opérateurs les plus utilisés :

| Opérateur | Description                | Exemple |
|-----------|----------------------------|---------|
| `+`       | Addition                   | `3 + 5` → `8` |
| `-`       | Soustraction                | `10 - 4` → `6` |
| `*`       | Multiplication              | `2 * 3` → `6` |
| `/`       | Division (résultat en float) | `5 / 2` → `2.5` |
| `//`      | Division entière (résultat sans virgule) | `5 // 2` → `2` |
| `%`       | Modulo (reste de la division) | `5 % 2` → `1` |
| `**`      | Exponentiation              | `2 ** 3` → `8` |

#### Exemple concret :

```python
# Calculs simples avec des opérateurs arithmétiques
a = 10
b = 4

# Addition
addition = a + b  # 10 + 4 = 14

# Division entière
division_entiere = a // b  # 10 // 4 = 2

# Reste de la division (modulo)
reste = a % b  # 10 % 4 = 2

# Exponentiation
exponentiation = 2 ** 3  # 2**3 = 8

print(addition, division_entiere, reste, exponentiation)
```

Ce code démontre comment effectuer des calculs arithmétiques de base avec des variables.

### Les opérateurs de comparaison

Les opérateurs de comparaison servent à comparer deux valeurs ou variables. Le résultat de ces comparaisons est toujours un booléen (`True` ou `False`). Ces opérateurs sont utilisés dans des conditions (structures `if` par exemple) pour prendre des décisions.

| Opérateur | Description        | Exemple    |
|-----------|--------------------|------------|
| `==`      | Égal à             | `a == b` → `False` |
| `!=`      | Différent de       | `a != b` → `True`  |
| `>`       | Supérieur à        | `a > b` → `True`   |
| `<`       | Inférieur à        | `a < b` → `False`  |
| `>=`      | Supérieur ou égal  | `a >= b` → `True`  |
| `<=`      | Inférieur ou égal  | `a <= b` → `False` |

#### Exemple concret :

```python
# Comparaison de deux valeurs
a = 10
b = 5

# Comparaison avec '=='
resultat_egalite = a == b  # False

# Comparaison avec '!='
resultat_diff = a != b  # True

# Comparaison avec '>'
resultat_superieur = a > b  # True

print(resultat_egalite, resultat_diff, resultat_superieur)
```

Les opérateurs de comparaison permettent de déterminer la relation entre deux valeurs, souvent utilisés pour effectuer des décisions conditionnelles dans les programmes.

### Les opérateurs logiques

Les opérateurs logiques sont utilisés pour combiner plusieurs conditions. Ils permettent de construire des expressions complexes où plusieurs conditions doivent être remplies simultanément. Les opérateurs logiques renvoient également un booléen (`True` ou `False`).

| Opérateur | Description                | Exemple    |
|-----------|----------------------------|------------|
| `and`     | Et logique (les deux conditions doivent être vraies) | `True and False` → `False` |
| `or`      | Ou logique (au moins une condition doit être vraie) | `True or False` → `True`  |
| `not`     | Négation (inverse une condition) | `not True` → `False`  |

#### Exemple concret :

```python
# Utilisation des opérateurs logiques
a = 10
b = 5

# 'and' : les deux conditions doivent être vraies
condition_and = (a > b) and (b < 10)  # True and True → True

# 'or' : au moins une condition doit être vraie
condition_or = (a > b) or (b > 10)  # True or False → True

# 'not' : inverse la condition
condition_not = not (a < b)  # not (False) → True

print(condition_and, condition_or, condition_not)
```

Les opérateurs logiques sont essentiels lorsqu'il faut combiner plusieurs conditions pour une prise de décision.

---

### Ressources

- [Documentation officielle de Python - Les opérateurs](https://docs.python.org/3/reference/lexical_analysis.html#operators)
- [Python Tutoriels - Les opérateurs](https://www.learnpython.org/fr/Les-opérateurs)
