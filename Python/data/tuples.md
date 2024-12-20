# Python : Les Tuples

## Introduction

Les tuples sont une structure de données fondamentale en Python. Ils permettent de regrouper plusieurs valeurs dans une seule variable, tout comme les listes. Cependant, une différence majeure les distingue : les tuples sont immuables, c'est-à-dire qu'ils ne peuvent pas être modifiés après leur création. Cette immutabilité les rend particulièrement utiles pour des situations où les données doivent rester constantes, comme des coordonnées, des paramètres de configuration ou des valeurs mathématiques fixes.

L'objectif de cette fiche est de présenter les concepts essentiels sur les tuples, leur utilité, et leur manipulation en Python à travers des exemples concrets. 

---

## Sommaire

1. Définition et création d'un tuple
2. Accès aux éléments d'un tuple
3. Opérations et méthodes courantes
4. Utilisation des tuples comme clés de dictionnaire
5. Cas pratiques : Analyse des statistiques de Pokémon
6. Ressources utiles

---

## 1. Définition et création d'un tuple

Un tuple est défini à l'aide de parenthèses `()` et peut contenir différents types de données.

```python
# Exemple 1 : Création de tuples
coordonnees = (12, 45)
statistiques_pokemon = ("Bulbizarre", 49, 45, 65)  # Nom, Attaque, Défense, Vitesse
print(coordonnees)
print(statistiques_pokemon)
```

Les tuples peuvent également être créés sans parenthèses explicites (packing) :

```python
# Exemple 2 : Tuple sans parenthèses
pack = "Pikachu", 55, 40, 90
print(pack)
```

Pourquoi utiliser un tuple ?
- Garantir l'intégrité des données : les valeurs ne peuvent pas être modifiées par accident.
- Améliorer les performances, car les tuples consomment moins de mémoire que les listes.

---

## 2. Accès aux éléments d'un tuple

Accéder aux éléments d'un tuple se fait via leur index, comme pour les listes.

```python
# Exemple 3 : Accès aux éléments
statistiques = ("Salamèche", 52, 43, 65)
nom = statistiques[0]  # Premier élément
attaque = statistiques[1]  # Deuxième élément
print(f"Nom : {nom}, Attaque : {attaque}")
```

Les tuples supportent également le slicing :

```python
# Exemple 4 : Slicing
stats_reduit = statistiques[1:3]  # Extraction de l'attaque et de la défense
print(stats_reduit)
```

---

## 3. Opérations et méthodes courantes

Quelques opérations courantes sur les tuples :

| Opération              | Syntaxe                                   | Description                                     |
|------------------------|-------------------------------------------|------------------------------------------------|
| Longueur d'un tuple    | `len(tuple)`                              | Retourne le nombre d'éléments                 |
| Vérification d'élément | `element in tuple`                        | Vérifie si un élément est présent             |
| Concatenation          | `tuple1 + tuple2`                         | Combine deux tuples                           |
| Répétition             | `tuple * n`                               | Répète un tuple plusieurs fois                |

Exemple :

```python
# Exemple 5 : Opérations
statistiques1 = ("Carapuce", 48, 65, 43)
statistiques2 = ("Rondoudou", 45, 20, 20)
tout_statistiques = statistiques1 + statistiques2
print(tout_statistiques)
print("Rondoudou" in tout_statistiques)  # Vérifie la présence d'un élément
```

---

## 4. Utilisation des tuples comme clés de dictionnaire

Les tuples peuvent être utilisés comme clés dans un dictionnaire, car ils sont immuables.

```python
# Exemple 6 : Tuple comme clé
coordonnees = {(12, 45): "Centre Pokémon", (56, 78): "Arène"}
print(coordonnees[(12, 45)])
```

Cela est particulièrement utile pour des associations de données complexes.

---

## 5. Cas pratiques : Analyse des statistiques de Pokémon

Créer un programme simple qui calcule la moyenne des statistiques d'un Pokémon.

```python
# Exemple 7 : Calcul de la moyenne des statistiques
statistiques_pokemons = [
    ("Bulbizarre", 49, 49, 45),
    ("Salamèche", 52, 43, 65),
    ("Carapuce", 48, 65, 43),
]

for pokemon in statistiques_pokemons:
    nom, attaque, defense, vitesse = pokemon
    moyenne = (attaque + defense + vitesse) / 3
    print(f"{nom} : Moyenne des statistiques = {moyenne:.2f}")
```

Explication :
- Les données des Pokémon sont regroupées dans une liste de tuples.
- Les valeurs sont extraites via unpacking pour effectuer les calculs.

---

## 6. Ressources utiles

- [Documentation officielle Python](https://docs.python.org/3/tutorial/datastructures.html#tuples-and-sequences)
- [Introduction aux tuples - W3Schools](https://www.w3schools.com/python/python_tuples.asp)
- [Cours Python - Developpez.com](https://python.developpez.com/cours/DiveIntoPython/php/frdiveintopython/native_data_types/tuples.php)

---
