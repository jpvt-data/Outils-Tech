[⬅ Retour à Python](../README.md)

# Gestion des exceptions en Python

## Introduction
Lors du développement en Python, il est courant de rencontrer des erreurs. Ces erreurs, appelées "exceptions", peuvent survenir à différents moments et dans divers contextes. L'objectif de cette fiche technique est de présenter comment gérer ces erreurs de manière efficace afin de maintenir la stabilité du programme. Cela permet de prévenir les interruptions brutales et d'offrir une gestion fluide des erreurs dans les scripts.

Les exceptions en Python permettent de capturer les erreurs au moment où elles se produisent et de réagir de manière appropriée, par exemple, en affichant un message d'erreur explicite ou en prenant des mesures correctives.

## Contextes d'utilisation
La gestion des exceptions est utile lorsqu'une opération susceptible de provoquer une erreur est réalisée. Par exemple :
- Tentative de division par zéro
- Accès à un fichier qui n'existe pas
- Connexion à une base de données échouée
- Tentative d'accès à un index inexistant dans une liste

Dans tous ces cas, l'application ne doit pas se terminer brutalement mais plutôt gérer l'erreur de manière adéquate. Le mécanisme des exceptions permet d'encapsuler ce type de logique.

## Théorie des exceptions
Une exception se produit lorsqu'une erreur est rencontrée lors de l'exécution d'un programme. Au lieu de laisser l'application échouer, Python offre un mécanisme permettant de capturer cette erreur et de définir un comportement alternatif.

### Lecture d'un message d'erreur
Lorsque Python rencontre une erreur, il génère un message d'exception. Voici un exemple simple :

```python
x = 0
print(12 / x)
```

Résultat d'exécution :
```
ZeroDivisionError: division by zero
```

- **Position de l'erreur** : Python indique que l'erreur s'est produite dans la ligne où se trouve le code `print(12 / x)`.
- **Type d'exception** : Ici, l'exception est une `ZeroDivisionError`, ce qui signifie qu'une tentative de division par zéro a été effectuée.
- **Message d'erreur** : Python nous informe que la division par zéro est impossible.

Il est important de comprendre ces messages d'erreur pour corriger rapidement les problèmes dans le code.

### Gestion des exceptions avec `try` et `except`

Le mécanisme le plus utilisé pour gérer les erreurs est le bloc `try`-`except`. Cela permet de tester un bloc de code et de définir une réaction lorsque l'exception se produit.

### Exemple de base de gestion d'exception

```python
x = 0

try:
    print(12 / x)
except ZeroDivisionError:
    print("Attention, une tentative de division par zéro a été effectuée.")
```

**Explication** :
- Le code dans le bloc `try` est exécuté normalement. Si une erreur se produit, Python passe directement au bloc `except`.
- Dans cet exemple, comme `x` est égal à 0, une erreur de type `ZeroDivisionError` est levée, et Python exécute alors le bloc `except` qui affiche le message "Attention, une tentative de division par zéro a été effectuée."

**Sortie** :
```
Attention, une tentative de division par zéro a été effectuée.
```

### Ajouter plusieurs types d'exceptions

Dans certaines situations, plusieurs types d'exceptions peuvent se produire. Pour chaque type d'erreur, un bloc `except` spécifique peut être défini afin de réagir de manière appropriée.

```python
x = "abc"

try:
    print(12 / x)
except ZeroDivisionError:
    print("Attention, division par zéro !")
except TypeError:
    print("Erreur : mauvaise utilisation d'un type de donnée.")
```

**Explication** :
- Ici, une erreur de type `TypeError` se produira, car on tente de diviser un nombre par une chaîne de caractères.
- Le bloc `except` correspondant à `TypeError` sera exécuté.

**Sortie** :
```
Erreur : mauvaise utilisation d'un type de donnée.
```

### Utilisation du bloc `else` et `finally`

Il est également possible d'utiliser les blocs `else` et `finally` pour gérer les erreurs de manière plus fine.

- Le bloc `else` est exécuté si aucune exception n'a été levée.
- Le bloc `finally` est exécuté quoi qu'il arrive, qu'une exception se produise ou non.

```python
x = 10

try:
    result = 12 / x
except ZeroDivisionError:
    print("Impossible de diviser par zéro.")
else:
    print("L'opération a été effectuée avec succès.")
finally:
    print("Fin du bloc de gestion d'exceptions.")
```

**Explication** :
- Si aucune exception n'est levée dans le bloc `try`, le bloc `else` est exécuté, et on affiche le message "L'opération a été effectuée avec succès."
- Le bloc `finally` est exécuté à la fin, quelle que soit l'issue de l'exécution.

**Sortie** :
```
L'opération a été effectuée avec succès.
Fin du bloc de gestion d'exceptions.
```

## Conclusion
La gestion des exceptions en Python permet de rendre un programme plus robuste en anticipant les erreurs et en y réagissant de manière appropriée. Ce mécanisme est essentiel pour éviter que des erreurs non gérées ne fassent planter l'application, et permet à l'utilisateur de comprendre ce qui s'est passé.

Voici un récapitulatif des points clés pour bien gérer les exceptions :

| Concept             | Description                                        | Exemple de Code                                    |
|---------------------|----------------------------------------------------|----------------------------------------------------|
| `try`               | Bloc où l'on tente d'exécuter du code susceptible de lever une erreur | `try: print(12 / x)`                               |
| `except`            | Bloc où l'on définit la gestion d'une exception spécifique | `except ZeroDivisionError: print("Erreur de division par zéro")` |
| `else`              | Bloc exécuté si aucune exception n'est levée      | `else: print("Succès de l'opération")`             |
| `finally`           | Bloc exécuté qu'une exception soit levée ou non   | `finally: print("Fin du traitement")`              |

#### Ressources supplémentaires
- [Documentation officielle de Python sur les exceptions](https://docs.python.org/fr/3/tutorial/errors.html)
- [Gestion des exceptions sur W3Schools](https://www.w3schools.com/python/python_try_except.asp)
