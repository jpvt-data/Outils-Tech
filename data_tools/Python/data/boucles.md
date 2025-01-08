### Python - Les Boucles

## Introduction

Les boucles sont des structures de contrôle très courantes en programmation, permettant de répéter un bloc d'instructions plusieurs fois. En Python, il existe principalement deux types de boucles : **while** et **for**. Ces boucles permettent d'exécuter des actions répétitives de manière concise et flexible. Cette fiche technique détaillée présente les différents types de boucles, leur fonctionnement, ainsi que des exemples concrets pour illustrer leur utilisation.

---

## Sommaire

1. Boucle conditionnelle `while` (tant que)  
2. Boucle itérative `for` (« pour tout... »)  
3. `break` et `continue`  
4. Les boucles imbriquées  
5. Ressources  

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
pokeballs = 5

while pokeballs > 0:
    print(f"J'ai lancé une Poké Ball ! Il m'en reste {pokeballs - 1}.")
    pokeballs -= 1

print("Je n'ai plus de Poké Balls.")
```

**Explication du code :**
- La boucle commence par vérifier si `pokeballs > 0` est vrai.  
- Si oui, elle affiche un message et décrémente `pokeballs`.  
- Lorsque `pokeballs` atteint 0, la boucle se termine.  

**Cas d'usage :**
- Utiliser `while` lorsque le nombre d'itérations dépend d'une condition dynamique (ex. attraper des Pokémon jusqu'à manquer de Poké Balls).

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

Lister les Pokémon capturés : 

```python
pokemon_captures = ["Pikachu", "Bulbizarre", "Salamèche", "Carapuce"]

for pokemon in pokemon_captures:
    print(f"J'ai capturé {pokemon} !")
```

**Explication du code :**
- Pour chaque Pokémon de la liste `pokemon_captures`, la boucle affiche un message.  

**Cas d'usage :**
- Utiliser `for` pour itérer sur des objets avec un nombre d'éléments connu à l'avance.

---

## 3. `break` et `continue`

Les instructions `break` et `continue` permettent de contrôler l'exécution des boucles.

### `break`

L'instruction `break` permet de sortir immédiatement de la boucle en cours, même si la condition n'est pas encore fausse.

```python
pokemon_captures = ["Pikachu", "Bulbizarre", "Mewtwo", "Salamèche"]

for pokemon in pokemon_captures:
    if pokemon == "Mewtwo":
        print("Mewtwo repéré, je me prépare pour un combat épique !")
        break
    print(f"{pokemon} capturé.")
```

**Explication du code :**
- La boucle s'arrête dès que `pokemon` est `"Mewtwo"`.  

### `continue`

L'instruction `continue` saute directement à l'itération suivante de la boucle sans exécuter les instructions restantes dans l'itération en cours.

```python
pokemon_captures = ["Pikachu", "Bulbizarre", "Mewtwo", "Salamèche"]

for pokemon in pokemon_captures:
    if pokemon == "Mewtwo":
        print("Mewtwo a fui, je le retrouverai plus tard...")
        continue
    print(f"{pokemon} capturé.")
```

**Explication du code :**
- Lorsque `pokemon` est `"Mewtwo"`, la boucle saute à l'itération suivante, sans afficher `"Mewtwo capturé."`.

---

## 4. Les boucles imbriquées

Il est possible d'imbriquer des boucles les unes dans les autres. Chaque boucle interne dépend de la boucle externe et sera exécutée pour chaque itération de la boucle externe.

### Exemple

```python
types_pokemon = ["Feu", "Eau", "Plante"]
pokemon_captures = ["Salamèche", "Carapuce", "Bulbizarre"]

for type_pokemon in types_pokemon:
    print(f"Pokémon de type {type_pokemon} disponibles :")
    for pokemon in pokemon_captures:
        print(f"- {pokemon}")
    print()
```

**Explication du code :**
- La boucle extérieure parcourt les `types_pokemon`.  
- La boucle intérieure liste les `pokemon_captures` pour chaque type.  

---

## 5. Ressources

Pour approfondir les concepts des boucles, voici quelques ressources utiles :  
- [Les boucles en Python (vidéo)](https://youtu.be/x_Jeyvw7n9I)  
- [Boucles imbriquées en Python (vidéo)](https://youtu.be/94UHCEmprCY)  

---

Cette fiche permet de comprendre et d'utiliser efficacement les boucles en Python, qui sont des éléments essentiels de la programmation. Que ce soit pour répéter des actions ou parcourir des données, maîtriser ces structures de contrôle est un pas fondamental dans l'apprentissage du langage.
