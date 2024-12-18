# Commenter et déboguer son code en Python

## Introduction

Le code Python, comme tout code informatique, peut rapidement devenir complexe et difficile à comprendre si les étapes ne sont pas bien expliquées. C'est pourquoi il est crucial d'apprendre à commenter son code et à le déboguer efficacement. Dans cette fiche, on s’intéresse à la manière de rendre son code lisible et facilement compréhensible par d’autres, tout en expliquant comment déboguer et structurer un code clair et fonctionnel. Ces pratiques permettent non seulement de travailler plus efficacement en équipe mais aussi de retrouver rapidement ses repères lorsqu'on revient sur un projet après un certain temps.

## Sommaire

- [Commenter son code](#commenter-son-code)
- [Déboguer son code en Python](#déboguer-son-code-en-python)
- [Exemple de code détaillé](#exemple-de-code-détaillé)

---

## Commenter son code

Commenter son code est une des pratiques les plus importantes dans la programmation, surtout lorsqu'on travaille en équipe ou qu'on souhaite revenir sur un projet plus tard. Un code bien commenté facilite la compréhension des autres développeurs, tout en aidant le programmeur à se rappeler de sa logique quelques mois après.

### Pourquoi commenter son code ?

1. **Facilite la lecture et la compréhension** : Un code peut paraître évident à l'auteur, mais il peut être difficile à comprendre pour un autre développeur. Les commentaires permettent de clarifier les intentions derrière le code et d'expliquer des choix spécifiques.
   
2. **Gain de temps pour les autres développeurs** : Si on travaille en équipe, les autres auront moins de difficultés à comprendre ce qu'on a fait et pourront ainsi reprendre le projet plus rapidement.

3. **Améliore la relecture du code** : Lorsqu'on revient sur un projet après un certain temps, les commentaires permettent de se rappeler pourquoi certaines décisions ont été prises.

### Bonnes pratiques pour commenter son code

- **Commenter les parties complexes** : Si une section de code est difficile à comprendre ou utilise une logique particulière, explique-la.
- **Expliquer les variables importantes** : Mentionner ce que chaque variable représente, surtout quand leur nom ne le décrit pas de façon évidente.
- **Eviter les commentaires redondants** : Ne commenter pas des choses évidentes, comme l'ajout de 1 à une variable. Se concentrer sur l'explication du raisonnement derrière des opérations complexes.
  
Voici un exemple de code commenté :

```python
# Initialisation de la liste des utilisateurs
utilisateurs = ['Alice', 'Bob', 'Charlie']

# Création d'une nouvelle liste avec les utilisateurs formatés
# On ajoute le préfixe "Utilisateur: " à chaque nom dans la liste
utilisateurs_formatés = [f"Utilisateur: {nom}" for nom in utilisateurs]

# Affichage des utilisateurs formatés
print(utilisateurs_formatés)
```

Dans cet exemple, chaque étape est expliquée pour éviter toute confusion.

---

## Déboguer son code en Python

Le débogage consiste à identifier et corriger les erreurs dans un programme. Les erreurs peuvent être de différents types : erreurs de syntaxe, erreurs logiques, ou encore des erreurs d'exécution. Voici les étapes de base pour déboguer du code Python.

### 1. **Lire les messages d'erreur**

Lorsque Python rencontre un problème, il génère un message d'erreur. Ce message donne des indices sur l'endroit et la nature du problème. Par exemple, une erreur courante pourrait être :

```python
# Erreur typique : une variable n'est pas définie
print(nom)
```

**Message d'erreur** : `NameError: name 'nom' is not defined`.

Dans ce cas, l'erreur indique que la variable `nom` n'a pas été définie avant d'être utilisée.

### 2. **Utiliser les outils de débogage**

Python dispose de nombreux outils pour faciliter le débogage, notamment la fonction `print()` pour afficher l’état des variables ou `pdb`, qui permet de mettre des points d'arrêt dans le code.

Voici un exemple de débogage avec `print()` :

```python
def calcul_somme(a, b):
    print(f"a = {a}, b = {b}")  # Affiche les valeurs de a et b
    return a + b

resultat = calcul_somme(3, 5)
print(f"Résultat = {resultat}")
```

Dans cet exemple, on peut suivre les valeurs des variables avant qu'elles ne soient utilisées dans le calcul.

### 3. **Utiliser un débogueur**

Le module `pdb` de Python permet de mettre des points d'arrêt dans le code et d’inspecter les valeurs des variables à différents endroits du programme.

```python
import pdb

def calcul_somme(a, b):
    pdb.set_trace()  # Déclenche l'arrêt à ce point
    return a + b

resultat = calcul_somme(3, 5)
```

Une fois le programme en pause à l'instruction `pdb.set_trace()`, on peut interagir avec le programme, inspecter les variables et avancer étape par étape dans le code.

---

## Exemple de code détaillé

Imaginons que l'on souhaite créer une fonction qui prédit si une personne est éligible à un prêt bancaire en fonction de son revenu annuel et de son historique de crédit. On va utiliser un modèle simple de Machine Learning pour prédire cette éligibilité. C’est un exemple de modèle supervisé où le modèle apprend à partir de données étiquetées (le résultat est déjà connu).

### 1. **Préparer les données**

Le jeu de données contient les informations suivantes :

- Revenu annuel (`revenu`)
- Score de crédit (`score_credit`)
- Éligibilité au prêt (`éligible` : 1 pour oui, 0 pour non)

```python
import pandas as pd

# Création du DataFrame
data = {
    'revenu': [30000, 45000, 60000, 50000, 120000],
    'score_credit': [650, 700, 750, 680, 800],
    'éligible': [0, 1, 1, 0, 1]
}

df = pd.DataFrame(data)
```

### 2. **Préparer les données pour le modèle**

On va séparer les caractéristiques (revenu et score de crédit) de l'étiquette (éligibilité au prêt).

```python
X = df[['revenu', 'score_credit']]  # Les caractéristiques
y = df['éligible']  # L'étiquette (la variable que l'on veut prédire)
```

### 3. **Créer et entraîner le modèle**

On va utiliser un modèle de régression logistique pour prédire si une personne est éligible au prêt en fonction de son revenu et de son score de crédit.

```python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score

# Séparation des données en ensemble d'entraînement et de test
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Création du modèle
modele = LogisticRegression()

# Entraînement du modèle
modele.fit(X_train, y_train)
```

### 4. **Faire une prédiction**

Une fois que le modèle est entraîné, on peut prédire l'éligibilité d'une nouvelle personne.

```python
# Données de test pour la prédiction
nouvelle_personne = [[70000, 720]]  # Revenu de 70,000 et score de crédit de 720

# Prédiction
prediction = modele.predict(nouvelle_personne)
print(f"Éligibilité au prêt : {'Oui' if prediction[0] == 1 else 'Non'}")
```

### Explication des étapes :

- **Données d'entrée** : On utilise les informations de revenu et de score de crédit pour prédire l’éligibilité.
- **Modèle** : Le modèle de régression logistique est un algorithme de Machine Learning supervisé qui est bien adapté pour des tâches de classification binaire (oui/non, éligible/non éligible).
- **Entraînement du modèle** : On divise les données en deux parties : une pour entraîner le modèle et l'autre pour tester sa performance.
- **Prédiction** : Le modèle prédit si une nouvelle personne est éligible ou non en fonction de son revenu et de son score de crédit.

---

## Conclusion

Documenter son code et savoir le déboguer efficacement sont des compétences essentielles pour tout développeur. En expliquant bien son raisonnement, on s'assure que d'autres développeurs pourront comprendre et reprendre le travail plus facilement. Le débogage, quant à lui, permet de corriger les erreurs et d’optimiser le code. Ces bonnes pratiques permettent de travailler plus sereinement, que ce soit seul ou en équipe.

--- 

### Ressources supplémentaires :

- [Python - Debugging with pdb](https://docs.python.org/3/library/pdb.html)
- [Commenter son code en Python - Guide complet](https://realpython.com/python-comments-guide/)
