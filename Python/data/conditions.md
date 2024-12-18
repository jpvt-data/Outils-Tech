# Python - Les Structures Conditionnelles

## Introduction

En programmation, les structures conditionnelles permettent de contrôler le flux d'exécution du programme en fonction de certaines conditions. Cela signifie qu'on peut définir des comportements différents selon que certaines situations sont remplies ou non. En Python, l'indentation est cruciale pour la clarté et l'organisation du code, car elle détermine les blocs de code à exécuter selon les conditions spécifiées. 

Dans cette fiche, on expliquera les différentes structures conditionnelles disponibles en Python et l'importance de l'indentation pour les rendre fonctionnelles. Cette approche est essentielle pour construire des programmes interactifs qui réagissent à des entrées ou des événements.

## Objectifs

- **Comprendre l'importance de l'indentation dans le code Python.**
- **Savoir utiliser les structures conditionnelles (if, if-else, if-elif-else).**
- **Maîtriser l’utilisation de ces structures pour prendre des décisions logiques dans un programme.**

## Sommaire

1. **L'Indentation**
2. **Les Structures Conditionnelles**
   - La structure conditionnelle `if`
   - La structure conditionnelle `if ... else`
   - La structure conditionnelle `if ... elif ... else`

---

### 1. L'Indentation

L'indentation en Python consiste à ajouter des espaces ou des tabulations au début de chaque ligne de code pour définir les blocs d'instructions qui doivent être exécutés ensemble. Contrairement à d'autres langages qui utilisent des symboles comme des crochets (`{}`) pour délimiter les blocs, Python repose sur l'indentation pour cette tâche. Chaque niveau d'indentation définit un bloc de code.

#### Règles d’Indentation

- **Espace ou Tabulation :** Il est recommandé d’utiliser 4 espaces pour chaque niveau d'indentation. Ce standard est universellement accepté dans la communauté Python.
- **Cohérence :** Mélanger les espaces et les tabulations dans un même fichier peut entraîner des erreurs difficiles à détecter. Il est donc essentiel de rester cohérent.

Exemple d'indentation correcte :

```python
if x > 5:
    print("x est plus grand que 5")
```

---

### 2. Les Structures Conditionnelles

Les structures conditionnelles sont utilisées pour exécuter des actions spécifiques en fonction de certaines conditions. Par exemple, on peut vouloir afficher un message uniquement si une variable a une certaine valeur, ou bien prendre une décision en fonction de l'état d'une donnée. Python offre trois formes principales de structures conditionnelles : `if`, `if ... else`, et `if ... elif ... else`.

#### 2.1 La structure conditionnelle `if`

La structure `if` permet d'exécuter un bloc de code uniquement si une condition est vraie. Si la condition est fausse, le bloc de code est ignoré.

**Syntaxe :**
```python
if condition:
    # Code à exécuter si la condition est vraie
```

**Exemple :**

```python
x = 10

if x > 5:  # Si x est supérieur à 5
    print("x est plus grand que 5")
```

**Explication :**  
Ici, la condition `x > 5` est vraie, donc l'instruction `print("x est plus grand que 5")` sera exécutée. Si `x` était inférieur ou égal à 5, rien ne se serait passé.

---

#### 2.2 La structure conditionnelle `if ... else`

La structure `if ... else` permet d'ajouter une branche alternative si la condition est fausse. Si la condition est vraie, le premier bloc est exécuté, sinon c'est le bloc du `else` qui prend le relais.

**Syntaxe :**
```python
if condition:
    # Code à exécuter si la condition est vraie
else:
    # Code à exécuter si la condition est fausse
```

**Exemple :**

```python
x = 10

if x > 12:  # Si x est supérieur à 12
    print("x est plus grand que 12")
else:       # Sinon
    print("x est plus petit ou égal à 12")
```

**Explication :**  
Ici, la condition `x > 12` est fausse, donc le bloc associé au `else` s'exécute, et le message "x est plus petit ou égal à 12" est affiché.

---

#### 2.3 La structure conditionnelle `if ... elif ... else`

Lorsqu’il y a plusieurs cas possibles à traiter, il est plus efficace d'utiliser une structure `if ... elif ... else` plutôt que d'imbriquer plusieurs `if` et `else`. Cela permet d'ajouter plusieurs alternatives à vérifier avant d'arriver au `else` final.

**Syntaxe :**
```python
if condition1:
    # Code à exécuter si condition1 est vraie
elif condition2:
    # Code à exécuter si condition2 est vraie
else:
    # Code à exécuter si aucune condition n'est remplie
```

**Exemple :**

```python
x = 12

if x > 12:  # 1ère condition
    print("x est plus grand que 12")
elif x == 12:  # 2ème condition
    print("x est égal à 12")
else:
    print("x est plus petit que 12")
```

**Explication :**  
Ici, la condition `x == 12` est vraie, donc la deuxième instruction `print("x est égal à 12")` est exécutée. Si `x` était plus grand que 12, la première condition aurait été vraie et le message correspondant aurait été affiché. Si aucune condition n’avait été vraie, le message du `else` aurait été affiché.

---

## Cas d'Utilisation

Les structures conditionnelles sont utilisées dans de nombreux cas en programmation. Par exemple :

- **Vérification des entrées utilisateur :** Pour s'assurer que l'utilisateur a saisi des données valides.
- **Traitement de données :** Pour appliquer des règles d'affaires et des filtres (par exemple, calculer des remises en fonction du montant d'achat).
- **Gestion des erreurs :** Pour gérer les exceptions et prendre des décisions en fonction des erreurs rencontrées.

---

## Conclusion

Les structures conditionnelles en Python sont des éléments clés pour prendre des décisions logiques dans un programme. Elles permettent de contrôler le flux d'exécution en fonction des conditions spécifiées. Une bonne gestion de l'indentation et une utilisation correcte de ces structures conditionnelles assurent la clarté et la lisibilité du code.

Pour en savoir plus, consultez la documentation officielle de Python :  
[Documentation Python sur les structures conditionnelles](https://docs.python.org/3/tutorial/controlflow.html)
