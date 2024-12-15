# Machine Learning - Régression linéaire simple (univariée)

## Introduction

Le Machine Learning est une branche de l'intelligence artificielle où les algorithmes apprennent à partir de données. Parmi les techniques fondamentales, la **régression linéaire simple** est utilisée pour prédire une variable continue à partir d’une autre variable explicative. Cette fiche explique les concepts, le pourquoi des étapes, et propose un guide pour implémenter cette méthode en Python avec **Pandas**, **Seaborn** et **Scikit-Learn**.

### Pourquoi utiliser la régression linéaire simple ?

- **Prédiction simple** : Estimer une valeur continue (ex. : prix d'un logement) en fonction d'une caractéristique (ex. : superficie).
- **Exploration de relations linéaires** : Identifier des tendances ou des corrélations entre deux variables.
- **Point de départ** : Comprendre des concepts essentiels pour progresser vers des modèles complexes.

Exemple : Estimer le prix d’un logement à partir de sa superficie.

---

## Concepts clés

### 1. Comprendre la régression linéaire simple

Elle repose sur une relation entre deux variables modélisée par une **ligne droite** :

\[ Y = \beta_0 + \beta_1 \cdot X + \varepsilon \]

- **Y** : Variable cible (valeur que l’on prédit, ex. : prix).
- **X** : Variable explicative (facteur influent, ex. : superficie).
- **\(\beta_0\)** : Interception (valeur de Y quand X = 0).
- **\(\beta_1\)** : Pente (comment Y change quand X augmente d'une unité).
- **\(\varepsilon\)** : Résidu ou erreur (écart entre valeurs réelles et prédites).

Cette approche **suppose une relation linéaire** et que les données suivent une distribution cohérente avec cette hypothèse.

---

## Exemple pratique avec explications

### Étape 1 : Préparer et explorer les données

**Pourquoi ?**  
La préparation des données assure que le modèle travaille avec un format exploitable et qu'aucune information essentielle ne manque. L'exploration permet de vérifier si une relation linéaire est plausible.

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error

# Création d'un DataFrame
data = {
    'Superficie (m2)': [30, 50, 60, 80, 100, 120],
    'Prix (k€)': [150, 200, 250, 300, 400, 500]
}
df = pd.DataFrame(data)
```

#### Visualisation des données

**Pourquoi ?**  
Une représentation graphique montre la distribution et l’éventuelle corrélation entre les variables. Si les points ne suivent pas une tendance linéaire, la régression linéaire pourrait être inappropriée.

```python
sns.scatterplot(x='Superficie (m2)', y='Prix (k€)', data=df)
plt.title("Relation entre superficie et prix")
plt.xlabel("Superficie (m2)")
plt.ylabel("Prix (k€)")
plt.show()
```

---

### Étape 2 : Diviser les données en ensembles d'entraînement et de test

**Pourquoi ?**  
Le but est d’entraîner le modèle sur une partie des données (ensemble d'entraînement) et d’évaluer ses performances sur des données inédites (ensemble de test). Cela évite que le modèle "apprenne par cœur" les données initiales, un phénomène appelé sur-apprentissage.

```python
X = df[['Superficie (m2)']]
y = df['Prix (k€)']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
```

---

### Étape 3 : Entraîner le modèle

**Pourquoi ?**  
L’entraînement ajuste les coefficients (\(\beta_0\) et \(\beta_1\)) pour minimiser l’écart entre les prédictions du modèle et les valeurs réelles. C’est ici que le modèle "apprend" la relation entre les données.

```python
model = LinearRegression()
model.fit(X_train, y_train)
```

Affichez les paramètres du modèle pour comprendre son fonctionnement :

```python
print("Pente (coefficient) :", model.coef_[0])
print("Interception :", model.intercept_)
```

Ces coefficients traduisent mathématiquement la relation linéaire identifiée.

---

### Étape 4 : Évaluer les performances du modèle

**Pourquoi ?**  
Évaluer le modèle est essentiel pour vérifier qu’il généralise correctement, c'est-à-dire qu'il fonctionne aussi bien sur de nouvelles données.

1. Faire des prédictions sur l'ensemble de test :

```python
y_pred = model.predict(X_test)
```

2. Calculer l’erreur quadratique moyenne (MSE) :

**Pourquoi le MSE ?**  
Cet indicateur mesure la différence moyenne entre les valeurs prédites et les valeurs réelles. Plus il est faible, meilleur est le modèle.

```python
mse = mean_squared_error(y_test, y_pred)
print("Erreur quadratique moyenne :", mse)
```

---

### Étape 5 : Visualiser le modèle ajusté

**Pourquoi ?**  
Visualiser la ligne ajustée par le modèle permet de mieux comprendre ses prédictions et d’observer si elle correspond aux données.

```python
plt.scatter(X, y, color='blue', label='Données')
plt.plot(X, model.predict(X), color='red', label='Modèle')
plt.title("Ligne de régression")
plt.xlabel("Superficie (m2)")
plt.ylabel("Prix (k€)")
plt.legend()
plt.show()
```

---

### Étape 6 : Prédiction pour une nouvelle entrée

**Pourquoi ?**  
Tester une nouvelle valeur simule une application réelle du modèle, par exemple, estimer le prix d'un logement donné sa superficie.

```python
new_value = [[70]]
price_prediction = model.predict(new_value)
print(f"Prédiction pour 70 m2 : {price_prediction[0]:.2f} k€")
```

---

## Ressources complémentaires

- [Documentation officielle de Scikit-Learn](https://scikit-learn.org/stable/)
- [Cours vidéo sur la régression linéaire](https://www.youtube.com/watch?v=PaFPbb66DxQ)

---

Avec ces ajouts, chaque étape est justifiée pour expliquer non seulement ce qu’elle fait, mais aussi pourquoi elle est importante et comment elle s’inscrit dans le cadre global du modèle. Dis-moi si tu souhaites des ajustements supplémentaires !
