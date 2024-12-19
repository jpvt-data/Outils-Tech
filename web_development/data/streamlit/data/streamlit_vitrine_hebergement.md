# Création et Hébergement d'un Site Streamlit "Vitrine Professionnelle"

Ce guide détaille le processus de création, d'hébergement, et de mise en ligne d'un site Streamlit vitrine professionnelle, avec une page de dashboard et des métriques d'exemple. L'objectif est de déployer l'application gratuitement et de la lier à un nom de domaine personnalisé.

## 1. Prérequis

Avant de commencer, vous devez avoir installé Python sur votre machine et avoir une version de `pip` récente. Si ce n'est pas déjà fait, vous pouvez installer Streamlit et les dépendances nécessaires à l'aide de la commande suivante dans votre terminal :

```bash
pip install streamlit pandas plotly scikit-learn numpy
```

Ensuite, créez un répertoire pour votre projet et placez les fichiers suivants dans ce répertoire. Voici une structure d'exemple pour un projet Streamlit avec un dashboard analytique.

### Structure de répertoire

```plaintext
mon_projet/
│
├── main.py
├── pages/
│   ├── 1_analyse_ventes.py
│   ├── 2_analyse_clients.py
│   └── 3_predictions.py
├── utils.py
├── requirements.txt
└── .gitignore
```

### Contenu des fichiers

Voici le contenu détaillé pour chaque fichier, permettant de créer un site Streamlit avec des pages de métriques et des visualisations.

#### **1. Fichier `main.py`**

```python
import streamlit as st
import pandas as pd
import plotly.express as px
from utils import load_data, style_metric_cards

st.set_page_config(
    page_title="Dashboard Analytics",
    page_icon="📊",
    layout="wide",
    initial_sidebar_state="expanded"
)

# Custom CSS
st.markdown("""
    <style>
    .block-container {
        padding-top: 2rem;
    }
    [data-testid="stMetricLabel"] {
        min-height: 0px;
        max-height: 50px;
        font-size: 20px;
    }
    [data-testid="stMetricValue"] {
        font-size: 28px;
    }
    </style>
""", unsafe_allow_html=True)

# Titre principal
st.title("📊 Dashboard Analytics")
st.markdown("### Vue d'ensemble des performances")

# Chargement des données
df = load_data()

# Calcul des métriques avec gestion des deltas
daily_revenue = df.groupby('date')['revenue'].sum().reset_index()
current_revenue = daily_revenue['revenue'].sum()
previous_revenue = daily_revenue['revenue'].shift(1).sum()
revenue_delta = ((current_revenue - previous_revenue) / previous_revenue * 100) if previous_revenue != 0 else 0

# Calcul des autres métriques et affichage sous forme de cartes
# Vous pouvez consulter ce fichier pour plus de détails.
```

#### **2. Fichier `pages/1_analyse_ventes.py`**

```python
import streamlit as st
import pandas as pd
import plotly.express as px
from utils import load_data
from datetime import datetime, timedelta

st.set_page_config(page_title="Analyse des Ventes", page_icon="💰", layout="wide")
st.title("💰 Analyse détaillée des ventes")

# Chargement des données
df = load_data()

# Ajoutez les graphiques et les métriques de votre analyse des ventes ici
```

#### **3. Fichier `pages/2_analyse_clients.py`**

```python
import streamlit as st
import pandas as pd
import plotly.express as px
from utils import load_data

st.set_page_config(page_title="Analyse Clients", page_icon="👥", layout="wide")
st.title("👥 Analyse des clients")

# Ajoutez vos visualisations et analyses client
```

#### **4. Fichier `pages/3_predictions.py`**

```python
import streamlit as st
import pandas as pd
import plotly.express as px
from utils import load_data
from sklearn.linear_model import LinearRegression
import numpy as np

st.set_page_config(page_title="Prédictions", page_icon="🔮", layout="wide")
st.title("🔮 Prédictions et tendances")

# Ajoutez votre modèle prédictif et les graphiques associés
```

#### **5. Fichier `utils.py`**

```python
import pandas as pd
import numpy as np
from datetime import datetime, timedelta

def load_data():
    """Simule le chargement de données pour l'exemple"""
    dates = pd.date_range(start='2023-01-01', end='2024-12-31', freq='D')
    n_records = 10000
    df = pd.DataFrame({
        'date': np.random.choice(dates, n_records),
        'customer_id': np.random.randint(1, 1000, n_records),
        'product': np.random.choice(['Produit A', 'Produit B'], n_records),
        'channel': np.random.choice(['Web', 'Mobile'], n_records),
        'revenue': np.random.normal(100, 30, n_records),
        'converted': np.random.choice([0, 1], n_records)
    })
    return df
```

#### **6. Fichier `requirements.txt`**

```
streamlit
pandas
plotly
scikit-learn
numpy
```

## 2. Hébergement de l'application avec Streamlit Cloud

Pour héberger l'application gratuitement, vous pouvez utiliser **Streamlit Community Cloud**, qui permet de déployer des applications Streamlit de manière simple et gratuite.

### Étapes pour déployer sur Streamlit Cloud

1. **Création d'un compte Streamlit Cloud**
   - Rendez-vous sur [Streamlit Cloud](https://share.streamlit.io) et créez un compte si ce n'est pas déjà fait.

2. **Préparer votre projet GitHub**
   - Créez un dépôt GitHub pour votre projet, et ajoutez tous les fichiers mentionnés ci-dessus dans ce dépôt.

3. **Déploiement de l'application**
   - Une fois votre dépôt GitHub prêt, allez sur Streamlit Cloud et connectez-le à votre dépôt GitHub.
   - Sélectionnez le projet et Streamlit le déploiera automatiquement. Vous pourrez visualiser votre application à l'adresse fournie.

### Maintenir l'application active

Streamlit Cloud maintient l'application en ligne tant qu'elle est utilisée. Si vous avez des utilisateurs qui consultent régulièrement l'application, elle restera active.

## 3. Lier un nom de domaine personnalisé

1. **Acheter un nom de domaine**
   - Vous pouvez acheter un nom de domaine sur des plateformes comme [Namecheap](https://www.namecheap.com) ou [GoDaddy](https://www.godaddy.com).

2. **Configurer les DNS**
   - Connectez-vous à votre fournisseur de domaine et accédez à la gestion des DNS.
   - Ajoutez un enregistrement `CNAME` qui pointe vers l'adresse de votre application Streamlit (généralement sous la forme `votre-utilisateur.streamlit.app`).

3. **Mettre à jour les paramètres de Streamlit**
   - Une fois que vous avez configuré le DNS, Streamlit reconnaîtra automatiquement le nom de domaine après quelques heures.

## 4. Conclusion

Avec ce guide, vous avez créé une application Streamlit avec un dashboard analytique, l'avez déployée gratuitement sur Streamlit Cloud, et l'avez liée à un nom de domaine personnalisé. Vous pouvez maintenant partager votre vitrine professionnelle avec d'autres utilisateurs.