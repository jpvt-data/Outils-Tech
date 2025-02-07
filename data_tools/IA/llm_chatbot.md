# Création d'un Chatbot avec un LLM (Gemini)

## Introduction

Nous avons vu comment utiliser les LLMs à travers les Chatbots en ligne comme ChatGPT ou Gemini. Cependant, il est possible d’aller beaucoup plus loin avec les LLMs en ne leur demandant pas simplement de générer ou de corriger du code, mais en travaillant directement au sein du programme. C’est ainsi que l’on peut créer ses propres Chatbots !

## Objectifs

A la fin de ce guide, vous serez capable de :

✅ Comprendre comment interroger Gemini via l’API de Google AI Studio  
✅ Intégrer Gemini au sein de vos programmes  
✅ Créer un Chatbot conversationnel  

---

## Sommaire

1. [L’API de Google AI Studio](#lapi-de-google-ai-studio)
   - Créer un compte et une clef API
2. [L’API de Google AI Studio dans Python](#lapi-de-google-ai-studio-dans-python)
   - Installation de la bibliothèque Google Gemini  
   - Utilisation des secrets dans Google Colab  
   - Votre premier prompt  
   - Des prompts pour améliorer la réponse  
3. [Création d’un Chatbot](#creation-dun-chatbot)

---

## 1. L’API de Google AI Studio

### Créer un compte et une clef API sur Google AI Studio

Avant de commencer, il faut créer un compte sur la plateforme développeur de Google AI Studio. Une fois connecté, cliquez sur **"Créer une clef API"** et copiez la clef générée. Vous pourrez la retrouver ultérieurement sur votre tableau de bord.

---

## 2. L’API de Google AI Studio dans Python

### Installation de la bibliothèque Google Gemini

Ouvrez un notebook Colab et installez la bibliothèque avec :

```python
!pip install -q -U google-generativeai
```

### Utilisation des Secrets dans Google Colab

Pour stocker votre clef API en toute sécurité, utilisez les variables secrètes de Google Colab :

1. Cliquez sur l’icône **clef** à gauche.
2. Dans le champ **Nom**, entrez `GOOGLE_API_KEY`.
3. Dans le champ **Valeur**, collez votre clef API.
4. Activez l’option "Accès depuis le notebook".

Ensuite, initialisez votre session avec :

```python
import google.generativeai as genai
from google.colab import userdata

GOOGLE_API_KEY = userdata.get('GOOGLE_API_KEY')
genai.configure(api_key=GOOGLE_API_KEY)
```

Pour vérifier que tout fonctionne, affichez les modèles disponibles :

```python
for m in genai.list_models():
    if 'generateContent' in m.supported_generation_methods:
        print(m.name)
```

### Votre premier prompt

Créez un modèle et interrogez-le :

```python
model = genai.GenerativeModel('gemini-1.5-flash')

prompt = "Quel est le dernier roi de France ?"
reponse = model.generate_content(prompt)
print(reponse.text)
```

---

## 3. Création d’un Chatbot

Un Chatbot doit conserver **l’historique des conversations**. Voici comment le mettre en place :

```python
from IPython.display import Markdown, display

# Création du modèle de Chatbot
model = genai.GenerativeModel('gemini-1.5-flash')

# Création du prompt système
system_prompt = """
Tu es un spécialiste de l'Histoire de France. Tu donnes des réponses précises en les replaçant dans le contexte politique du pays.
"""

# Initialisation de l'historique
chat = model.start_chat(history=[{'role': 'user', 'parts': [system_prompt]}])

# Début du Chat
print("Bienvenue dans ce Chat sur l'Histoire de France. Tapez 'fin' pour quitter.")

while True:
    message = input("> ")
    if message.lower() == "fin":
        break
    response = chat.send_message(message)
    display(Markdown(response.text))
```

### Exemple de session :

```plaintext
> Quel est le dernier roi de France ?
Le dernier roi de France est Louis-Philippe Ier, dont le règne prit fin avec la révolution de 1848...

> À quel âge est-il mort ?
Louis-Philippe Ier est mort à l'âge de 76 ans en exil, en Angleterre...

> Quelle était ma première question ?
Ta première question était "Quel est le dernier roi de France ?"
```

