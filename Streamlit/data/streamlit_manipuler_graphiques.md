[⬅ Retour à Streamlit](../README.md)

# **Streamlit - Manipuler des Graphiques**

## **Objectifs**

- Créer un **dashboard** avec Streamlit.
- Manipuler et **afficher des données** efficacement dans une application web interactive.
- Maîtriser la **création de graphiques** avec Streamlit et des bibliothèques populaires.

---

## **Manipuler des données avec Streamlit**

Streamlit permet de charger, manipuler et afficher des données dans un format interactif directement sur une application web. Voici un aperçu des fonctions les plus utiles :

### **Fonctions de base pour afficher des données**
1. **`st.dataframe()`**  
   - Permet d’afficher un **DataFrame** dans un tableau interactif, avec des options telles que le tri des colonnes.  
   - **Exemple** :  
     ```python
     import streamlit as st
     import pandas as pd

     data = {'Nom': ['Alice', 'Bob', 'Claire'], 'Age': [25, 30, 35]}
     df = pd.DataFrame(data)

     st.dataframe(df)
     ```

2. **`st.table()`**  
   - Affiche un tableau statique en HTML à partir de données structurées (listes, NumPy, DataFrame).  
   - **Exemple** :  
     ```python
     st.table(df)
     ```

3. **`st.json()`**  
   - Affiche un **objet JSON** de manière indentée et lisible.  
   - **Exemple** :  
     ```python
     json_data = {"Nom": "Alice", "Age": 25, "Ville": "Paris"}
     st.json(json_data)
     ```

4. **`st.metric()`**  
   - Crée un **indicateur visuel** pour une métrique, utile pour des KPI (Key Performance Indicators).  
   - **Exemple** :  
     ```python
     st.metric(label="Ventes", value="100k€", delta="5%")
     ```

### **Fonctions avancées**
1. **`st.data_editor()`**  
   - Crée un tableau interactif modifiable par l'utilisateur.  
   - **Exemple** :  
     ```python
     st.data_editor(df)
     ```

2. **`st.column_config()`**  
   - Permet de configurer les options d’affichage d’une colonne dans une table interactive.

> **Documentation supplémentaire** : Pour plus d'informations, consulter la [documentation officielle](https://docs.streamlit.io/).

---

## **Créer des graphiques avec Streamlit**

Streamlit prend en charge plusieurs bibliothèques populaires de visualisation, ainsi que ses propres fonctions pour créer des graphiques interactifs.

### **Étapes générales pour créer un graphique**
1. Importer les bibliothèques nécessaires.
2. Charger ou préparer les données.
3. Créer la figure (graphique).
4. L’afficher dans l’application avec Streamlit.

---

### **1. Afficher un graphique avec Matplotlib**
```python
import streamlit as st
import matplotlib.pyplot as plt

# Données
x = [1, 2, 3, 4, 5]
y = [3, 5, 7, 2, 1]

# Création du graphique
fig, ax = plt.subplots()
ax.plot(x, y)
ax.set_xlabel("Axe X")
ax.set_ylabel("Axe Y")
ax.set_title("Graphique linéaire")

# Affichage
st.pyplot(fig)
```

---

### **2. Afficher un graphique avec Seaborn**
```python
import streamlit as st
import seaborn as sns
import matplotlib.pyplot as plt

# Charger un dataset
data = sns.load_dataset('iris')

# Créer un barplot
sns.barplot(x='species', y='sepal_length', data=data)

# Afficher le graphique
st.pyplot(plt.gcf())
```

---

### **3. Afficher un graphique avec Plotly**
```python
import streamlit as st
import seaborn as sns
import plotly.express as px

# Charger les données
iris = sns.load_dataset("iris")

# Créer un scatterplot interactif
fig = px.scatter(
    iris,
    x="sepal_width",
    y="sepal_length",
    color="species",
    size="petal_length",
    hover_data=["petal_width"]
)

# Afficher le graphique
st.plotly_chart(fig)
```

---

### **4. Afficher un graphique avec les fonctions propres à Streamlit**

Streamlit propose des fonctions simples pour créer rapidement des visualisations interactives :

1. **`st.area_chart()`** : Graphique à aires (idéal pour les tendances cumulées).  
   ```python
   import streamlit as st
   import pandas as pd
   import numpy as np

   data = pd.DataFrame(
       np.random.randn(20, 3),
       columns=["A", "B", "C"]
   )
   st.area_chart(data)
   ```

2. **`st.bar_chart()`** : Graphique à barres.  
   ```python
   st.bar_chart(data)
   ```

3. **`st.line_chart()`** : Graphique linéaire.  
   ```python
   st.line_chart(data)
   ```

4. **`st.map()`** : Carte géographique.  
   - Affiche des données géographiques (latitude, longitude).  
   ```python
   import pandas as pd
   import streamlit as st

   data = pd.DataFrame({
       'lat': [37.7749, 40.7128],
       'lon': [-122.4194, -74.0060]
   })

   st.map(data)
   ```

5. **`st.scatter_chart()`** : Diagramme à nuages de points.

---

## **Bonnes pratiques**
- Organiser les données **avant** de les visualiser.
- Ajouter des titres et des labels clairs pour chaque graphique.
- Expérimenter avec des bibliothèques comme Plotly pour des visualisations interactives.

---

## **Conclusion**
Streamlit offre une manière simple et rapide de manipuler et de visualiser des données dans des applications web interactives. 
Grâce à ses intégrations avec des bibliothèques populaires comme Matplotlib, Seaborn et Plotly, il permet de créer des graphiques variés et dynamiques adaptés à divers besoins d’analyse de données. 

Ces fonctionnalités, combinées à sa facilité d’utilisation, en font un excellent outil pour les Data Analysts qui cherchent à présenter leurs résultats de manière claire et engageante.