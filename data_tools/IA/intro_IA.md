# Introduction à l'Intelligence Artificielle Générative (IAG)

## Introduction

Ce guide vous permettra de comprendre les bases des **LLMs** (Large Language Models) comme ChatGPT, qui font partie de l'**Intelligence Artificielle Générative** (**IAG**). Contrairement aux IA classiques, qui se limitent à la prédiction ou à la classification, les IAG sont capables de **générer de nouvelles données** en s'appuyant sur un apprentissage massif.

Les IAG sont devenues incontournables dans le monde professionnel et éducatif. Cependant, elles présentent des risques qu'il est essentiel de comprendre pour une utilisation efficace et responsable.

## Objectifs

A la fin de ce guide, vous serez capable de :

✅ Comprendre les bases du fonctionnement des **LLMs**  
✅ Consulter un **LLM** pour obtenir des résultats précis  
✅ Identifier les limites et les risques des **LLMs**  
✅ Comprendre les enjeux de la **confidentialité des données** en entreprise  

---

## Sommaire

1. [Un bref historique](#un-bref-historique)
2. [Les modèles](#les-modeles)
3. [Les IAG : tour d'horizon](#les-iag-tour-dhorizon)
4. [Les risques et les bonnes pratiques](#les-risques-et-les-bonnes-pratiques)
5. [Atelier LLMs](#atelier-llms)
   - Utiliser ChatGPT
   - Tour d'horizon de Gemini

---

## 1. Un bref historique

Les modèles de traitement du langage naturel (**NLP**) ont commencé avec l'analyse statistique des mots, mais ont rapidement évolué vers des représentations vectorielles (**Word2Vec, Glove, ELMo**). Le tournant majeur est arrivé avec les **Transformers**, introduits par l'article "Attention is All You Need" de Google en 2017.

Depuis, l'émergence de modèles comme **BERT** (Google) et **GPT** (OpenAI) a révolutionné l'intelligence artificielle, permettant des performances accrues en **génération et en compréhension du langage naturel**.

**Les LLMs fonctionnent sur un principe probabiliste**, prédisant les mots les plus probables pour former des phrases. Cependant, ils **ne comprennent pas vraiment** le sens des phrases, ce qui peut entraîner des erreurs (**"hallucinations"**).

---

## 2. Les modèles

On distingue plusieurs types de modèles IAG :

- **Open-source** (ex: **Mistral, Llama**) vs **Propriétaires** (ex: **ChatGPT, Gemini**)
- **Chatbots accessibles en ligne** vs **modèles intégrés à des logiciels**

Les principaux modèles sur le marché incluent :

- **ChatGPT** (OpenAI)
- **Claude** (Anthropic)
- **Gemini** (Google)
- **Llama** (Meta)
- **Mistral** (Mistral AI)

Ces modèles sont accessibles via **des interfaces de chatbot, des API ou en local**, si l'infrastructure le permet.

---

## 3. Les IAG : tour d'horizon

Les LLMs sont disponibles sous plusieurs formes :

### Chatbots accessibles en ligne

- **ChatGPT** (OpenAI)
- **Claude** (Anthropic)
- **Gemini** (Google)
- **HuggingChat** (Hugging Face)

### IAG intégrées dans des outils

- **Gemini dans Google Colab**
- **Codeium pour VS Code**
- **Github Copilot (payant)**
- **Amazon CodeWhisperer (payant)**

---

## 4. Les risques et les bonnes pratiques

### Risques

- **Apprentissage biaisé** : Utiliser ChatGPT sans comprendre le raisonnement peut donner une fausse impression de maîtrise.
- **Confidentialité** : En entreprise, les **données sensibles** ne doivent pas être soumises à des IAG en ligne.
- **Hallucinations** : Les modèles peuvent produire des réponses incorrectes ou inventées.
- **Dépendance excessive** : Trop utiliser ces outils peut nuire à l'autonomie de résolution de problèmes.

### Bonnes pratiques

1. **Ne pas utiliser ChatGPT en phase d'apprentissage initial** pour coder ou résoudre un problème directement.
2. **Privilégier les recherches manuelles** avant de demander de l'aide à une IAG.
3. **Poser des questions génériques et progressives** pour comprendre un concept au lieu de demander une solution toute faite.
4. **Vérifier les réponses fournies** en croisant les sources.
5. **Utiliser les IAG comme copilotes**, pas comme solutions finales.

> **Attention** : Lors des certifications ou tests techniques, l'utilisation d'un LLM est interdite.

---

## 5. Atelier LLMs

### Utiliser ChatGPT intelligemment

Prenons l'exemple suivant :

**Consigne** : Ecrivez un programme qui calcule le carré des entiers entre 0 et 1000, lorsqu’ils sont divisibles par 2 ou par 3, mais pas par 5.

Mauvaise approche :

```python
for i in range(1001):
    if (i % 2 == 0 or i % 3 == 0) and i % 5 != 0:
        print(f"Le carré de {i} est {i**2}")
```

Si vous recopiez la consigne dans ChatGPT, il vous donnera directement ce code. Mais vous n’aurez rien appris.

Bonne approche :

1. **Analyser le problème**
2. **Diviser en sous-tâches**
3. **Chercher les solutions par soi-même**
4. **Utiliser ChatGPT pour valider ou expliquer un concept précis**, comme "Comment vérifier si un nombre est divisible en Python ?"

---

### Tour d'horizon de Gemini

**Gemini (Google)** est un LLM intégré dans Google Colab, permettant d’automatiser certaines tâches de code.

#### Mode Code
- Suggère du code en complétion automatique
- Peut manquer de contexte, menant à des erreurs

#### Mode Chat
- Fonctionne comme ChatGPT
- Idéal pour expliquer du code ou obtenir un raisonnement

**Désactiver Gemini** : Dans Google Colab, aller dans les paramètres (rouage en haut à droite) > "Assistance IA" > Désactiver l'IA générative.

---

## Conclusion

L'IA générative est un outil puissant, mais elle doit être utilisée intelligemment. **Comprendre son fonctionnement et ses limites est essentiel** pour en tirer le meilleur parti sans tomber dans ses pièges.

