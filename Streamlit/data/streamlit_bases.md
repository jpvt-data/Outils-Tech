[⬅ Retour à Streamlit](../README.md)

# Streamlit - Les Bases

**Streamlit** est une bibliothèque open-source qui permet de transformer des scripts Python en applications web interactives, sans avoir besoin de connaissances poussées en développement web. Elle est idéale pour les analystes de données ou les développeurs souhaitant partager leurs analyses de manière visuelle et intuitive. Ce guide couvre les bases essentielles pour débuter avec Streamlit.

---

## Objectifs
- Installer Streamlit.
- Créer et exécuter une application Streamlit simple.
- Ajouter des éléments interactifs tels que du texte, des boutons, des médias et des graphiques.

---

## Sommaire
1. Comprendre une application web
2. Installer Streamlit
3. Créer et exécuter une application Streamlit
4. Ajouter du texte
5. Ajouter des entrées utilisateur
6. Ajouter des médias

---

## 1. Comprendre une application web

Les applications web se basent sur trois technologies principales :
- **HTML** : Structure la page web (titres, paragraphes, liens, etc.).
- **CSS** : Gère l'apparence (couleurs, polices, mise en page).
- **JavaScript** : Permet d'ajouter de l'interactivité (animations, réponses aux actions de l'utilisateur).

Avec **Streamlit**, il n'est pas nécessaire d'écrire du HTML, du CSS ou du JavaScript. Cette bibliothèque génère automatiquement l'interface utilisateur et la rend responsive, c'est-à-dire adaptée aux différents appareils. L'objectif est de simplifier la création d'applications web interactives pour les développeurs Python, sans s'occuper des détails du développement web.

---

## 2. Installer Streamlit

Pour commencer à utiliser Streamlit, il est nécessaire de l'installer sur votre machine.

### Étapes d'installation :
1. **Vérifier que Python est installé** : Assurez-vous d'avoir Python 3.x installé. Si ce n'est pas le cas, installez-le depuis le site officiel de Python.
2. **Installer Streamlit** : Ouvrez un terminal et exécutez la commande suivante pour installer Streamlit via `pip` :
   ```bash
   pip install streamlit
   ```
3. **Vérifier l'installation** : Pour vérifier que Streamlit est installé correctement, exécutez cette commande :
   ```bash
   streamlit hello
   ```
   Cela lancera un exemple d'application Streamlit dans votre navigateur.

---

## 3. Créer et exécuter une application Streamlit

Une fois Streamlit installé, il est temps de créer une première application.

### Étapes :
1. **Créer un fichier Python** : Créez un fichier avec l'extension `.py`, par exemple `app.py`.
2. **Ajouter du code basique** :
   ```python
   import streamlit as st
   
   st.title("Bienvenue sur ma première application Streamlit !")
   ```
3. **Exécuter l'application** : Ouvrez un terminal et lancez l'application en utilisant la commande suivante :
   ```bash
   streamlit run app.py
   ```
   L'application s'ouvrira dans votre navigateur par défaut.

---

## 4. Ajouter du texte

Streamlit offre plusieurs fonctions pour afficher du texte de manière structurée et claire.

### Commandes disponibles :
- **st.title** : Affiche un titre principal.
- **st.header** : Affiche un titre secondaire.
- **st.subheader** : Affiche un titre de sous-section.
- **st.text** : Affiche du texte brut.
- **st.markdown** : Permet d'afficher du texte formaté en Markdown (gras, italique, liens, etc.).
- **st.write** : Affiche des données sous différentes formes (texte, DataFrame, objets Python).

### Exemple de code pour afficher du texte :
```python
st.title("Titre Principal")
st.header("En-tête Importante")
st.subheader("Sous-en-tête")
st.text("Voici un texte simple.")
st.markdown("**Texte formaté en Markdown.**")
```

---

## 5. Ajouter des entrées utilisateur

Streamlit permet d'ajouter facilement des éléments interactifs afin de collecter des données de l'utilisateur. Voici les principales options disponibles.

### **5.1 Boutons**
Les boutons peuvent déclencher des actions lorsque l'utilisateur clique dessus.
```python
if st.button("Clique-moi"):
    st.write("Bouton cliqué !")
```

### **5.2 Sélecteurs**
- **Checkbox** : Permet de demander une confirmation.
  ```python
  agree = st.checkbox("J'accepte les conditions.")
  if agree:
      st.write("Merci pour votre accord.")
  ```
- **Radio Buttons** : Permet de sélectionner une option parmi plusieurs.
  ```python
  choix = st.radio("Choisissez une option :", ['Option 1', 'Option 2', 'Option 3'])
  st.write(f"Vous avez choisi : {choix}")
  ```
- **Selectbox et Multiselect** : Permet de sélectionner une option ou plusieurs options dans une liste déroulante.
  ```python
  st.selectbox("Choisissez un fruit :", ["Pomme", "Banane", "Orange"])
  st.multiselect("Choisissez vos fruits préférés :", ["Pomme", "Banane", "Orange"])
  ```
- **Slider** : Permet de sélectionner une valeur sur une échelle.
  ```python
  age = st.slider("Quel est votre âge ?", 0, 100, 25)
  st.write(f"Vous avez {age} ans.")
  ```

### **5.3 Champs de texte**
- **Text Input** : Permet d'entrer une valeur textuelle sur une ligne.
  ```python
  nom = st.text_input("Entrez votre nom :")
  st.write(f"Bonjour, {nom} !")
  ```
- **Text Area** : Permet de saisir un texte multiligne.
  ```python
  message = st.text_area("Votre message :")
  st.write(f"Votre message : {message}")
  ```

### **5.4 Entrées numériques**
- **Number Input** : Permet d'entrer un nombre.
  ```python
  st.number_input("Entrez un nombre :", min_value=0, max_value=100, value=50)
  ```

### **5.5 Sélection de date et heure**
- **Date Input** : Permet de sélectionner une date.
  ```python
  st.date_input("Sélectionnez une date :")
  ```
- **Time Input** : Permet de sélectionner une heure.
  ```python
  st.time_input("Sélectionnez une heure :")
  ```

---

## 6. Ajouter des médias

Streamlit permet d'ajouter facilement des médias à l'application pour enrichir l'expérience utilisateur.

### **6.1 Ajouter une image**
```python
st.image("chemin/vers/image.jpg", caption="Voici une image", use_column_width=True)
```

### **6.2 Ajouter une vidéo**
```python
st.video("chemin/vers/video.mp4")
```

### **6.3 Ajouter un fichier audio**
```python
st.audio("chemin/vers/audio.mp3")
```

---

## Conclusion

Streamlit est une bibliothèque simple et puissante pour créer des applications web interactives avec Python. Grâce à son approche intuitive, il est possible d'ajouter facilement des éléments interactifs, du texte et des médias pour rendre les applications plus dynamiques et engageantes. En explorant les possibilités graphiques avec des bibliothèques comme Matplotlib ou Plotly, il est possible d'étendre les fonctionnalités de vos applications.

---

### 🚀 Aller plus loin
Explorez l'intégration de bibliothèques de visualisation de données comme **Matplotlib**, **Seaborn** ou **Plotly** pour créer des graphiques et des visualisations interactives directement dans votre application Streamlit.


[⬅ Retour à Streamlit](../README.md)