# Python - Boucles

## Introduction

Les boucles sont des structures de contrôle très courantes en programmation, permettant de répéter un bloc d'instructions plusieurs fois. En Python, il existe principalement deux types de boucles : **while** et **for**. Ces boucles permettent d'exécuter des actions répétitives de manière concise et flexible. Cette fiche technique détaillée présente les différents types de boucles, leur fonctionnement, ainsi que des exemples concrets pour illustrer leur utilisation. Cette fiche s'adresse aux débutants et explique chaque concept pas à pas.

---

## Sommaire

1. Boucle conditionnelle `while` (tant que)
2. Boucle itérative `for` (« pour tout... »)
3. `break` et `continue`
4. Les boucles imbriquées
5. Ressources
6. Challenge
    - Critères de validation

---

## 1. Boucle conditionnelle `while` (tant que)

La boucle `while` permet d'exécuter un bloc d'instructions tant qu'une condition spécifiée est vraie. Elle est idéale lorsque l'on ne connaît pas à l'avance le nombre d'itérations, mais qu'on veut arrêter la boucle dès que la condition devient fausse.

### Syntaxe

```python
while condition:
    instruction_1
    instruction_2
    ...
    instruction_n
```

- **condition** : Expression qui est évaluée avant chaque itération. Si elle est vraie, les instructions de la boucle sont exécutées. Dès qu'elle devient fausse, la boucle s'arrête.

### Exemple

```python
nombre = 0

while nombre < 10:
    nombre += 1  # incrémente de 1 à chaque itération
    print(nombre)

print('Fini !')
```

**Explication du code :**
- La boucle commence par vérifier si la condition `nombre < 10` est vraie.
- Si oui, elle exécute `nombre += 1`, ce qui augmente la valeur de `nombre` à chaque itération.
- Lorsque `nombre` atteint 10, la condition devient fausse et la boucle se termine.
- Enfin, le message `'Fini !'` est affiché.

**Cas d'usage :**
- Utiliser `while` lorsque le nombre d'itérations dépend d'une condition dynamique (ex. attente de l'entrée utilisateur, surveillance d'un état, etc.).

### Piège à éviter : boucle jamais exécutée

```python
nombre = -1

while nombre >= 0:
    print("Rien ne s'affiche...")
```

- Ici, la condition `nombre >= 0` est fausse dès le début (car `nombre = -1`), ce qui empêche la boucle d’être exécutée.

### Piège à éviter : boucle infinie

```python
while True:
    print("Ce texte sera affiché encore et encore !")
```

- Cette boucle ne s'arrêtera jamais, car `True` est toujours vrai. Il est essentiel de prévoir une condition d'arrêt ou une instruction `break`.

---

## 2. Boucle itérative `for` (« pour tout... »)

La boucle `for` est utilisée pour parcourir un ensemble d'éléments (une liste, une plage de nombres, une chaîne de caractères, etc.) et exécuter un bloc d'instructions pour chaque élément.

### Syntaxe

```python
for element in iterable:
    instruction_1
    instruction_2
    ...
    instruction_n
```

- **element** : L'élément actuel dans l'itérable.
- **iterable** : Une séquence de valeurs (par exemple une liste, une chaîne, ou un objet généré par `range()`).

### Exemple

Afficher les entiers entre 0 et 100 avec `for` :

```python
for nombre in range(0, 101):
    print(nombre)
```

**Explication du code :**
- La fonction `range(0, 101)` génère une séquence de nombres allant de 0 à 100 (le 101 est exclus).
- Pour chaque nombre dans cette séquence, la boucle affiche sa valeur.

**Cas d'usage :**
- Utiliser `for` pour itérer sur des objets avec un nombre d'éléments connu à l'avance.

---

## 3. `break` et `continue`

Les instructions `break` et `continue` permettent de contrôler l'exécution des boucles.

### `break`

L'instruction `break` permet de sortir immédiatement de la boucle en cours, même si la condition n'est pas encore fausse.

```python
for nombre in range(5):
    if nombre == 3:
        break
    print(nombre)
```

**Explication du code :**
- La boucle s'arrête dès que `nombre == 3`, et les nombres 0, 1 et 2 sont affichés. Le `break` interrompt la boucle.

### `continue`

L'instruction `continue` saute directement à l'itération suivante de la boucle sans exécuter les instructions restantes dans l'itération en cours.

```python
for nombre in range(5):
    if nombre == 3:
        continue
    print(nombre)
```

**Explication du code :**
- Lorsque `nombre == 3`, l'instruction `continue` fait sauter l'affichage de ce nombre. Ainsi, la boucle affiche tous les nombres de 0 à 4 sauf 3.

---

## 4. Les boucles imbriquées

Il est possible d'imbriquer des boucles les unes dans les autres. Chaque boucle interne dépend de la boucle externe et sera exécutée pour chaque itération de la boucle externe.

### Exemple

```python
for i in range(1, 6):
    for j in range(1, i + 1):
        print(j, end=' ')
    print()  # Saut de ligne après chaque boucle interne
```

**Explication du code :**
- La boucle extérieure fait varier `i` de 1 à 5.
- La boucle intérieure, pour chaque valeur de `i`, affiche les nombres de 1 à `i`.

Cela produit un affichage comme suit :

```
1
1 2
1 2 3
1 2 3 4
1 2 3 4 5
```

---

## 5. Ressources

Pour approfondir les concepts des boucles, voici quelques ressources utiles :

- [Les boucles en Python (vidéo)](https://youtu.be/x_Jeyvw7n9I)
- [Boucles imbriquées en Python (vidéo)](https://youtu.be/94UHCEmprCY)

---

Cette fiche permet de comprendre et d'utiliser efficacement les boucles en Python, qui sont des éléments essentiels de la programmation. Que ce soit pour répéter des actions ou parcourir des données, maîtriser ces structures de contrôle est un pas fondamental dans l'apprentissage du langage.
