# Introduction à Python

## Pourquoi utiliser Python ?

Python est un langage de programmation incontournable, connu pour sa simplicité et sa polyvalence. Avec sa syntaxe claire et intuitive, il convient aussi bien aux débutants qu'aux experts pour des applications complexes. Python est largement utilisé dans des domaines variés comme la science des données, le développement web, l'automatisation des tâches, et bien plus encore.

Dans le contexte du métier de data analyst, Python est particulièrement prisé pour :

- Manipuler et analyser des données.
- Visualiser des données avec des bibliothèques comme Matplotlib ou Seaborn.
- Automatiser des processus répétitifs.
- Appliquer des algorithmes de machine learning avec des outils comme Scikit-learn.

---

## Les caractéristiques principales de Python

- **Simplicité :** Une syntaxe facile à lire et à écrire.
- **Langage interprété :** Exécution ligne par ligne, facilitant le développement et le débogage.
- **Typage dynamique :** Le type des variables est attribué automatiquement.
- **Portabilité :** Compatible avec les principaux systèmes d'exploitation.
- **Extensibilité :** Grâce à des milliers de bibliothèques disponibles (Pandas, NumPy, etc.).

---

## Exemples de base en Python

### Déclaration de variables et types dynamiques

```python
# Déclaration de variables
nom = "Jean Paul"
age = 45
is_data_analyst = True

# Affichage des variables
print(f"Nom : {nom}, Âge : {age}, Data Analyst : {is_data_analyst}")
```

### Les structures de contrôle

```python
# Exemple de conditionnelle
score = 85
if score >= 90:
    print("Excellent")
elif score >= 70:
    print("Bon")
else:
    print("Peut mieux faire")

# Exemple de boucle
for i in range(5):
    print(f"Itération : {i}")
```

---

## Applications concrètes pour un Data Analyst

### Manipulation de données avec Pandas

```python
import pandas as pd

# Chargement des données
data = pd.DataFrame({
    "Nom": ["Alice", "Bob", "Charlie"],
    "Âge": [25, 30, 35],
    "Salaire": [50000, 60000, 70000]
})

# Aperçu des données
print(data.head())

# Statistiques descriptives
print(data.describe())
```

### Visualisation avec Matplotlib

```python
import matplotlib.pyplot as plt

# Création d'un graphique simple
ages = [25, 30, 35, 40]
salaries = [50000, 60000, 70000, 80000]

plt.plot(ages, salaries, marker='o')
plt.title("Salaire en fonction de l'âge")
plt.xlabel("Âge")
plt.ylabel("Salaire")
plt.show()
```

### Analyse avancée : Prévision avec Scikit-learn

```python
from sklearn.linear_model import LinearRegression
import numpy as np

# Données simulées
ages = np.array([25, 30, 35, 40]).reshape(-1, 1)
salaries = np.array([50000, 60000, 70000, 80000])

# Modèle de régression linéaire
model = LinearRegression()
model.fit(ages, salaries)

# Prédiction pour un nouvel âge
new_age = np.array([[45]])
print(f"Prédiction du salaire pour 45 ans : {model.predict(new_age)[0]:.2f}")
```

---

## Conclusion

Python est un outil incontournable pour les data analysts, offrant une multitude de bibliothèques et fonctionnalités pour simplifier les tâches complexes. Que ce soit pour manipuler des données, créer des visualisations percutantes ou modéliser des algorithmes, maîtriser Python est une compétence essentielle dans ce métier.
