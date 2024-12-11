# Streamlit - Fonctionnalités avancées

Streamlit permet de développer des applications web interactives pour la visualisation et l'analyse de données. Dans un contexte professionnel, il peut être nécessaire d'ajouter des fonctionnalités avancées telles que la création de menus de navigation, l'intégration d'une page de connexion sécurisée, et le déploiement en ligne de l'application. Cette fiche explique comment mettre en place ces éléments de manière détaillée et pédagogique.

## Créer une page de connexion

Pour sécuriser une application Streamlit et contrôler l'accès aux différentes sections, il est possible d'utiliser des modules tiers comme **Streamlit Authenticator**. Ce module offre une authentification basée sur des identifiants et un mot de passe, gère les sessions utilisateur et protège contre les attaques par force brute.

### Pourquoi utiliser une page de connexion ?
Une page de connexion permet de :
- Limiter l'accès aux utilisateurs autorisés uniquement.
- Protéger les données sensibles affichées sur l'application.
- Gérer différents niveaux d'accès selon les rôles utilisateur (par exemple : administrateurs et utilisateurs standards).

### Fonctionnalités principales
- **Authentification par nom d'utilisateur et mot de passe** : Empêche l'accès non autorisé en exigeant des identifiants valides.
- **Gestion des sessions** : Permet de gérer les différentes sections de l'application en fonction des rôles et de maintenir l'état de connexion.
- **Protection contre les attaques par force brute** : Limite les tentatives de connexion incorrectes pour éviter les abus.

### Mise en œuvre détaillée

#### Étape 1 : Installer le module
Utilisez la commande suivante dans le terminal pour installer Streamlit Authenticator :
```bash
pip install streamlit-authenticator
```

#### Étape 2 : Configurer le module
Créez une configuration contenant les informations des utilisateurs autorisés, puis initialisez l'objet d'authentification :
```python
import streamlit as st
from streamlit_authenticator import Authenticate

lesDonneesDesComptes = {
    'usernames': {
        'utilisateur': {
            'name': 'Utilisateur Exemple',
            'password': 'utilisateurMDP',
            'email': 'utilisateur@gmail.com',
            'role': 'utilisateur'
        },
        'admin': {
            'name': 'Admin Exemple',
            'password': 'adminMDP',
            'email': 'admin@gmail.com',
            'role': 'administrateur'
        }
    }
}

authenticator = Authenticate(
    lesDonneesDesComptes, "cookie_name", "cookie_key", 30
)
```
#### Étape 3 : Ajouter le formulaire de connexion
Affichez le formulaire de connexion dans l'application et gérez les états d'authentification :
```python
authenticator.login()
if st.session_state["authentication_status"]:
    st.title("Bienvenue, accès autorisé !")
elif st.session_state["authentication_status"] is False:
    st.error("Identifiants incorrects. Veuillez réessayer.")
```
#### Étape 4 : Gérer les autorisations
Ajoutez une logique conditionnelle pour afficher des contenus spécifiques selon le rôle utilisateur.

---

## Ajouter un menu de navigation

Un menu de navigation est essentiel pour structurer une application et permettre aux utilisateurs de naviguer facilement entre différentes sections.

### Pourquoi utiliser un menu de navigation ?
Un menu interactif améliore l'expérience utilisateur en :
- Organisant les fonctionnalités par sections claires.
- Facilitant l'accès rapide aux différentes pages de l'application.

### Mise en œuvre détaillée

#### Étape 1 : Installer le module
Exécutez cette commande dans le terminal :
```bash
pip install streamlit-option-menu
```

#### Étape 2 : Créer un menu interactif
Ajoutez un menu horizontal ou vertical selon vos besoins :
```python
from streamlit_option_menu import option_menu

selection = option_menu(
    menu_title=None,  # Pas de titre pour le menu
    options=["Accueil", "Analyse", "Contact"],  # Options du menu
    icons=["house", "graph-up", "envelope"],  # Icônes pour chaque option
    menu_icon="cast",  # Icône du menu principal
    default_index=0  # Option par défaut
)

if selection == "Accueil":
    st.write("Bienvenue sur la page d'accueil")
elif selection == "Analyse":
    st.write("Analyse des données")
elif selection == "Contact":
    st.write("Page de contact")
```

---

## Publier une application Streamlit sur Streamlit Cloud

Pour rendre une application accessible à tous, il est possible de la déployer gratuitement sur **Streamlit Cloud**. Ce service simplifie le processus de déploiement et de partage.

### Étapes de déploiement

#### Étape 1 : Créer un compte Streamlit Cloud
Rendez-vous sur [Streamlit.io](https://streamlit.io/) et créez un compte. Vous pouvez utiliser vos identifiants Google ou GitHub pour un accès rapide.

#### Étape 2 : Préparer l'application
1. Assurez-vous que l'application fonctionne correctement en local.
2. Créez un repository GitHub contenant :
   - Le fichier Python de l'application (par ex. `app.py`).
   - Un fichier `requirements.txt` listant toutes les dépendances nécessaires (généré avec `pip freeze > requirements.txt`).

#### Étape 3 : Déployer l'application
1. Connectez Streamlit Cloud à votre compte GitHub.
2. Sélectionnez le repository contenant votre application.
3. Suivez les instructions pour lancer le déploiement.

#### Étape 4 : Configurer la visibilité
Accédez aux paramètres de l'application et activez l'option **"This app is public and searchable"** pour la rendre accessible au grand public.

### Conseils pratiques
- **Performance** : Testez l'application après le déploiement pour vérifier les temps de chargement.
- **Limites** : Le plan gratuit impose des limites sur les ressources. Envisagez un abonnement payant pour des besoins professionnels avancés.

---

En suivant ces étapes, vous pouvez créer des applications Streamlit interactives, sécurisées et accessibles en ligne. Ces fonctionnalités répondent aux besoins des utilisateurs et renforcent l'efficacité des solutions proposées.

