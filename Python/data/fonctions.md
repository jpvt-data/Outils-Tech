# Introduction aux Fonctions en Python

## Contexte et Objectif

Les fonctions en Python permettent de structurer et de simplifier un programme en encapsulant des blocs de code réutilisables. Elles sont essentielles pour éviter la répétition de code, faciliter la maintenance et rendre le code plus lisible. Cette fiche technique explique de manière détaillée ce qu’est une fonction, comment la définir, l'utiliser, et ce qui se passe à l'intérieur de ces fonctions.

## Définition d’une Fonction

Une fonction est un ensemble d’instructions regroupées sous un nom. Ce nom permet de réutiliser le bloc de code défini dans la fonction à tout moment dans un programme, avec différents arguments ou paramètres.

### Structure de base d'une fonction

La structure d’une fonction commence par le mot-clé `def`, suivi du nom de la fonction, de parenthèses contenant des paramètres (optionnels) et enfin, d'un bloc d'instructions indenté qui détermine l’action que la fonction va réaliser.

### Exemple simple : Calcul de la somme de trois nombres

```python
def somme(coup_1, coup_2, coup_3):
    total = coup_1 + coup_2 + coup_3
    return total
```

Ici, la fonction `somme` prend trois paramètres (`coup_1`, `coup_2`, `coup_3`) et retourne la somme de ces trois valeurs.

### Utilisation de la fonction

```python
resultat = somme(5, 3, 7)
print(resultat)  # Affiche 15
```

Ce code appelle la fonction `somme` avec les arguments 5, 3, et 7. Le résultat retourné est 15.

#### Explication

- `def` est utilisé pour définir la fonction.
- `somme` est le nom de la fonction.
- `(coup_1, coup_2, coup_3)` sont les paramètres, ils permettent de passer des valeurs à la fonction.
- `return` permet de renvoyer une valeur calculée par la fonction.

### Paramètres et Arguments

- **Paramètres** : Ce sont les variables qui apparaissent dans la définition de la fonction (ici `coup_1`, `coup_2`, `coup_3`).
- **Arguments** : Ce sont les valeurs réelles que l'on passe à la fonction lorsque l'on l'appelle (ici 5, 3, et 7).

**Important** : Le nombre d'arguments que l'on passe à la fonction doit correspondre au nombre de paramètres définis.

### Exemple avec conditions

```python
def lancer_de(coup_1, coup_2, coup_3):
    total = coup_1 + coup_2 + coup_3
    if total < 8:
        return "Mauvais coup"
    elif total < 13:
        return "Bon coup"
    else:
        return "Incroyable !"
```

### Appel de la fonction avec des arguments

```python
resultat = lancer_de(4, 3, 2)
print(resultat)  # Affiche "Bon coup"
```

Ici, la fonction retourne `"Bon coup"` car la somme des trois valeurs est 9.

#### Explication

- La fonction `lancer_de` vérifie si la somme des trois coups est inférieure à 8, entre 8 et 13, ou supérieure à 13, puis renvoie un message approprié.

## Fonction sans Paramètres

Une fonction peut également être définie sans paramètres. Dans ce cas, elle ne reçoit aucune donnée d'entrée lors de son appel.

### Exemple de fonction sans paramètres

```python
def saluer():
    return "Bonjour, bienvenue dans le monde des Pokémon !"
```

### Appel de la fonction sans paramètres

```python
message = saluer()
print(message)  # Affiche "Bonjour, bienvenue dans le monde des Pokémon !"
```

#### Explication

La fonction `saluer` ne prend pas de paramètres, mais renvoie un message de salutation.

## Utilisation des Fonctions dans un Contexte plus Large

Les fonctions peuvent être utilisées de manière répétée dans un programme plus complexe pour accomplir des tâches variées. Par exemple, dans le cadre d’un jeu où l’on lance des dés, chaque joueur peut effectuer plusieurs lancers et obtenir un score.

### Exemple : Compter les joueurs qualifiés dans un jeu

Imaginons un tournoi où les participants lancent trois dés. Si leur total est supérieur à 12, ils sont qualifiés pour la finale.

```python
import random

def lancer_de(coup_1, coup_2, coup_3):
    total = coup_1 + coup_2 + coup_3
    if total < 8:
        return "Mauvais coup"
    elif total < 13:
        return "Bon coup"
    else:
        return "Incroyable !"

# Compter les joueurs qualifiés
joueurs_qualifies = 0

for i in range(32):  # 32 joueurs
    # Lancer aléatoire des dés pour chaque joueur
    resultat = lancer_de(random.randint(1, 6), random.randint(1, 6), random.randint(1, 6))
    
    if resultat == "Incroyable !":
        joueurs_qualifies += 1

print(f"Nombre de joueurs qualifiés : {joueurs_qualifies}")
```

### Résultat attendu

```python
Nombre de joueurs qualifiés : 7
```

#### Explication

- `random.randint(1, 6)` génère un nombre aléatoire entre 1 et 6, simulant un lancer de dé.
- La fonction `lancer_de` est appelée pour chaque joueur avec trois valeurs aléatoires.
- Si le résultat est `"Incroyable !"`, cela signifie que le joueur a obtenu un total supérieur à 12 et est qualifié pour la finale.

## Conclusion

Les fonctions permettent de rendre un programme plus modulaire et réutilisable. Elles sont essentielles pour éviter la duplication du code et pour structurer de manière plus claire les opérations complexes. Dans ce contexte, une fonction renvoie des valeurs qui peuvent être utilisées à différents endroits du programme, rendant le développement plus efficace et moins sujet aux erreurs.

## Liens Utiles

- [Documentation Python - Fonctions](https://docs.python.org/3/tutorial/controlflow.html#defining-functions)
- [Python Random Module](https://docs.python.org/3/library/random.html)
