[⬅ Page Précédente](../README.md)

# Python - Sets et manipulation des ensembles

## Introduction

Les ensembles (ou "sets") sont des structures de données très utiles dans Python. Ils permettent de manipuler des collections non ordonnées d'éléments uniques. Les sets sont particulièrement adaptés pour les situations où il est nécessaire d'éliminer les doublons ou d'effectuer des opérations ensemblistes (union, intersection, etc.).

## Qu'est-ce qu'un set ?

Un set est une collection non ordonnée et sans doublons. Cela signifie que chaque élément est unique et qu'il n'y a pas d'ordre spécifique des éléments.

### Comparaison avec d'autres structures :

| Structure | Caractéristiques |
|-----------|-------------------|
| Liste     | Ordonnée, permet les doublons |
| Tuple     | Ordonné, immuable, permet les doublons |
| Set       | Non ordonné, éléments uniques |

### Exemple de création d'un set :
```python
liste_pokemons = ["Pikachu", "Evoli", "Salamèche", "Pikachu", "Bulbizarre"]
ensemble_pokemons = set(liste_pokemons)

print("Liste originale :", liste_pokemons)
print("Set créé :", ensemble_pokemons)
```

Sortie :
```
Liste originale : ['Pikachu', 'Evoli', 'Salamèche', 'Pikachu', 'Bulbizarre']
Set créé : {'Evoli', 'Salamèche', 'Pikachu', 'Bulbizarre'}
```

## Créer, modifier et manipuler des sets

### Créer un set :
Un set peut être créé à partir de n’importe quelle collection (liste, tuple, etc.) :
```python
set_pokemons = set(["Dracaufeu", "Florizarre", "Tortank"])
print(set_pokemons)
```

### Ajouter un élément :
```python
set_pokemons.add("Mewtwo")
print(set_pokemons)
```

### Retirer un élément :
```python
set_pokemons.discard("Florizarre")  # Ne gène pas si l'élément n'existe pas
print(set_pokemons)
```

### Opérations ensemblistes :

| Opération              | Syntaxe             | Description                                   |
|--------------------------|---------------------|-----------------------------------------------|
| Union                   | `set1.union(set2)`  | Combine les éléments des deux sets          |
| Intersection            | `set1.intersection(set2)` | Renvoie les éléments communs entre les deux sets |
| Différence             | `set1.difference(set2)` | Renvoie les éléments présents uniquement dans le premier set |

### Exemple pratique : Comparer deux groupes de Pokémons

```python
generation1 = {"Dracaufeu", "Florizarre", "Tortank", "Pikachu"}
generation2 = {"Pikachu", "Evoli", "Mew", "Dracolosse"}

# Union
print("Tous les Pokémons :", generation1.union(generation2))

# Intersection
print("Pokémons communs :", generation1.intersection(generation2))

# Différence
print("Pokémons uniquement en génération 1 :", generation1.difference(generation2))
```

Sortie :
```
Tous les Pokémons : {'Mew', 'Florizarre', 'Pikachu', 'Tortank', 'Dracolosse', 'Dracaufeu', 'Evoli'}
Pokémons communs : {'Pikachu'}
Pokémons uniquement en génération 1 : {'Tortank', 'Dracaufeu', 'Florizarre'}
```

## Cas d'utilisation des sets

### Identification des doublons

Utiliser des sets pour trouver des Pokémons uniques dans une liste :
```python
liste_pokemons = ["Pikachu", "Evoli", "Pikachu", "Dracaufeu", "Evoli"]
pokemons_uniques = set(liste_pokemons)
print("Pokémons uniques :", pokemons_uniques)
```

### Filtrer des données uniques

Supposons qu’un dresseur enregistre les Pokémons attrapés dans plusieurs listes et souhaite créer une base de données sans doublons :
```python
attrap_safari = {"Psykokwak", "Tartard", "Pikachu"}
attrap_foret = {"Tartard", "Bulbizarre", "Pikachu"}

base_donnees = attrap_safari.union(attrap_foret)
print("Base de données unique :", base_donnees)
```

## Conclusion

Les sets sont puissants pour manipuler des collections non ordonnées d’éléments uniques. Ils simplifient les opérations comme l’élimination des doublons, les comparaisons et les regroupements. En comprenant leurs principes de base et leurs opérations, il devient possible de résoudre des problèmes complexes de manière efficace.

### Ressources supplémentaires

- [Documentation officielle Python sur les sets](https://docs.python.org/3/tutorial/datastructures.html#sets)
- [Tutoriel sur W3Schools](https://www.w3schools.com/python/python_sets.asp)

[⬅ Page Précédente](../README.md)