[⬅ Page Précédente](../README.md)

# **Python - Les Fonctions**

## **Contexte et Objectif**

Les fonctions en Python permettent de structurer un programme en organisant le code en blocs réutilisables. Cela aide non seulement à éviter la répétition du code, mais aussi à le rendre plus lisible et plus facile à maintenir. Dans cette fiche, nous explorerons en détail ce que sont les fonctions, comment les définir et les utiliser, et comment gérer les différents types de paramètres et de valeurs retournées.

---

## **1. Définition d’une Fonction**

Une fonction est un bloc de code qui accomplit une tâche spécifique et qui peut être réutilisé plusieurs fois dans un programme. Elle peut accepter des **paramètres** (ou arguments) pour personnaliser son comportement, et renvoyer une **valeur** grâce au mot-clé `return`.

### **Structure de Base d’une Fonction**

Une fonction en Python est définie à l’aide du mot-clé `def`, suivi du nom de la fonction, des parenthèses (qui peuvent contenir des paramètres), et d’un bloc d’instructions indentées.

```python
def nom_de_fonction(parametre_1, parametre_2):
    # Instructions à exécuter
    return valeur
```

### **Exemple Simple : Calcul de la somme de trois nombres**

Voici un exemple de fonction qui prend trois paramètres et retourne leur somme :

```python
def somme(coup_1, coup_2, coup_3):
    total = coup_1 + coup_2 + coup_3
    return total
```

### **Appel de la Fonction**

L’appel d’une fonction se fait en utilisant son nom suivi de parenthèses contenant les arguments que l’on souhaite passer à la fonction.

```python
resultat = somme(5, 3, 7)
print(resultat)  # Affiche 15
```

#### **Explication :**
- **`def`** : Mot-clé utilisé pour définir une fonction.
- **`somme`** : Nom de la fonction.
- **`coup_1, coup_2, coup_3`** : Paramètres de la fonction, qui seront utilisés comme variables locales dans la fonction.
- **`return`** : Retourne la valeur calculée à l'appelant (ici, la somme des trois nombres).

---

## **2. Paramètres et Arguments**

### **Paramètres**
Les paramètres sont des variables dans la définition de la fonction. Ils sont utilisés pour recevoir les valeurs (ou arguments) lors de l'appel de la fonction.

### **Arguments**
Les arguments sont les valeurs que vous passez à la fonction lorsqu'elle est appelée. Le nombre d'arguments doit correspondre au nombre de paramètres définis.

```python
# Paramètres : a, b
def addition(a, b):
    return a + b

# Arguments : 3, 5
resultat = addition(3, 5)  # Résultat = 8
```

### **Exemple avec des conditions**

Vous pouvez aussi ajouter des conditions dans une fonction pour effectuer différentes actions selon les valeurs des arguments.

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

```python
resultat = lancer_de(4, 3, 2)
print(resultat)  # Affiche "Bon coup"
```

#### **Explication :**
La fonction `lancer_de` vérifie la somme des trois arguments et retourne un message en fonction de la valeur totale. Si le total est inférieur à 8, le message sera "Mauvais coup", entre 8 et 12 : "Bon coup", et au-dessus de 13 : "Incroyable !".

---

## **3. Fonctions sans Paramètres**

Il est possible de définir une fonction qui ne prend pas de paramètres. Dans ce cas, la fonction ne reçoit aucune donnée à son appel.

### **Exemple : Fonction sans paramètres**

```python
def saluer():
    return "Bonjour, bienvenue dans le monde des Pokémon !"
```

### **Appel de la fonction sans paramètres**

```python
message = saluer()
print(message)  # Affiche "Bonjour, bienvenue dans le monde des Pokémon !"
```

---

## **4. Fonctions avec Valeur par Défaut**

Une fonction peut avoir des paramètres avec des **valeurs par défaut**. Cela signifie que si un argument n'est pas fourni lors de l'appel, la valeur par défaut est utilisée.

### **Exemple : Valeur par défaut**

```python
def salut(message="Bonjour tout le monde !"):
    return message
```

### **Appel avec et sans argument**

```python
print(salut())  # Affiche "Bonjour tout le monde !"
print(salut("Salut, Python !"))  # Affiche "Salut, Python !"
```

---

## **5. Fonctions avec Nombre Variable de Paramètres**

En Python, il est aussi possible de définir une fonction qui accepte un nombre variable d'arguments à l'aide de l'astérisque (`*`) pour les arguments positionnels et du double astérisque (`**`) pour les arguments nommés.

### **Exemple avec `*args` (Arguments positionnels)**

```python
def addition_multiple(*args):
    return sum(args)
```

```python
print(addition_multiple(1, 2, 3))  # Affiche 6
print(addition_multiple(5, 7, 2, 8))  # Affiche 22
```

### **Exemple avec `**kwargs` (Arguments nommés)**

```python
def afficher_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")
```

```python
afficher_info(nom="Pikachu", type="Électrique")  # Affiche "nom: Pikachu" et "type: Électrique"
```

---

## **6. Retourner Plusieurs Valeurs**

Une fonction peut également retourner plusieurs valeurs en les séparant par des virgules. Python les renvoie sous forme de tuple.

### **Exemple : Retour de plusieurs valeurs**

```python
def calcul(a, b):
    somme = a + b
    difference = a - b
    return somme, difference
```

```python
resultat = calcul(10, 5)
print(resultat)  # Affiche (15, 5)
```

---

## **7. Fonctions dans un Contexte Pratique**

Les fonctions peuvent être utilisées de manière répétée dans des programmes plus complexes pour accomplir diverses tâches. Prenons l'exemple d'un jeu où les participants lancent trois dés. Si leur total est supérieur à 12, ils sont qualifiés pour la finale.

### **Exemple : Compter les joueurs qualifiés**

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

---

## **Conclusion**

Les fonctions sont essentielles pour structurer et simplifier un programme Python. Elles permettent de rendre le code plus lisible, réutilisable et plus facile à maintenir. Que ce soit pour des calculs simples ou des opérations complexes, les fonctions vous aideront à rendre votre code plus modulaire et plus efficace. Grâce aux concepts de paramètres, d'arguments, de valeurs par défaut, et de nombre variable d'arguments, vous pouvez définir des fonctions puissantes et flexibles qui s'adaptent à vos besoins spécifiques.

---

## Liens Utiles

- [Documentation Python - Fonctions](https://docs.python.org/3/tutorial/controlflow.html#defining-functions)
- [Python Random Module](https://docs.python.org/3/library/random.html)

[⬅ Page Précédente](../README.md)