# Introduction à l’ETL/ELT et au Data Warehousing

## Objectifs
- **Définir** le concept de data warehouse et son rôle dans l’analyse des données.  
- **Distinguer** les bases de données de type OLTP et OLAP.  
- **Appréhender** les principes fondamentaux des processus ETL et ELT.  
- **Savoir** choisir entre ETL et ELT selon les cas d’usage.  
- **Découvrir** quelques outils adaptés pour implémenter ces processus.

---

## Sommaire
1. [Qu’est-ce qu’un data warehouse ?](#quest-ce-quun-data-warehouse-)  
   1.1. [Différences entre OLTP et OLAP](#différences-entre-une-base-de-données-oltp-et-olap)  
2. [Qu’est-ce que l’ETL ?](#quest-ce-que-letl-)  
   2.1. [Processus : Extraction, Transformation, Chargement](#extraction)  
3. [ETL vs ELT](#différences-entre-etl-et-elt)  
4. [Outils ETL et ELT](#outils-detl-et-delt)  
5. [Exemple d’un mini-processus ETL (code)](#exemple-dun-mini-processus-etl-en-pseudo-code)  

---

## Qu’est-ce qu’un Data Warehouse ?
Un **data warehouse** (entrepôt de données) est un système centralisé permettant de consolider et de stocker un grand volume de données en provenance de multiples sources. L’objectif est de faciliter l’analyse en offrant une vue globale de l’information.  

### Exemple Pokémon
Imaginons un data warehouse dédié à l’analyse des Pokémon. Les données pourraient provenir :
- Des bases Pokédex traditionnelles (liste des Pokémon, leurs types, leurs évolutions).  
- De données de tournois en ligne (combats, équipes utilisées, statistiques de victoire/défaite).  
- De retours utilisateurs issus d’une application mobile de capture de Pokémon.  

En centralisant ces données au même endroit, il devient possible de répondre rapidement à des questions telles que :  
- Quels types de Pokémon sont les plus utilisés en compétition ?  
- Comment les performances de certains Pokémon évoluent-elles au fil des mois ?  
- Quels environnements de capture sont les plus populaires ?  

---

## Différences entre une base de données OLTP et OLAP

| Caractéristique               | OLTP (Online Transaction Processing)                                     | OLAP (Online Analytical Processing)                                          |
|-------------------------------|----------------------------------------------------------------------------|------------------------------------------------------------------------------|
| **Utilisation**               | Gestion des transactions quotidiennes (enregistrement de captures, etc.) | Analyse et reporting (performances en tournoi, tendances d’utilisation)     |
| **Type d’accès**              | Accès fréquent en lecture/écriture                                        | Accès majoritairement en lecture                                            |
| **Complexité des requêtes**   | Requêtes simples (INSERT, UPDATE, SELECT ciblés)                          | Requêtes complexes et agrégations (GROUP BY, calculs de stats, etc.)        |
| **Performance requise**       | Réponses rapides (millisecondes)                                         | Réponses tolérant des temps plus longs (secondes à minutes)                 |
| **Modèle de données**         | Modèle fortement normalisé                                                | Modèle dénormalisé pour faciliter l’agrégation                              |
| **Utilisateurs typiques**     | Administrateurs, applications clients                                    | Analystes, data scientists, décisionnaires                                  |
| **Exemple d’application**     | Systèmes de gestion des captures, ventes de produits dérivés             | Analyses de tendances, rapports de compétitions annuels                     |
| **Conservation des données**  | Court terme ou temps réel                                                 | Long terme, historique, agrégation de données                               |

---

## Qu’est-ce que l’ETL ?
L’**ETL** (Extract, Transform, Load) est un processus qui permet de :
1. **Extraire** des données de sources hétérogènes.  
2. **Transformer** ces données pour les nettoyer, les harmoniser et les agrémenter.  
3. **Charger** ces données dans un entrepôt cible ou une base de données d’analyse.  

### Rôle de l’ETL
- Garantir la cohérence et la qualité des données dans le data warehouse.  
- Faciliter la création d’une base historique solide pour l’analyse.  
- Fusionner des informations issues de différentes origines (par exemple, associer des données de capture à des données de tournois).  

---

### Extraction
#### Approches courantes
1. **Notification de mise à jour** : la source signale qu’un nouveau Pokémon a été enregistré ou qu’une statistique de combat a été modifiée.  
2. **Extraction incrémentale** : récupération périodique (par ex. chaque semaine) des données modifiées (nouveaux Pokémon découverts dans certaines régions).  
3. **Extraction complète** : récupération de l’intégralité des données d’un système, généralement à forte volumétrie et plus lourde en ressources.  

### Transformation
- **Nettoyage** : suppression des doublons dans la liste des Pokémon capturés, traitement des noms écrits en minuscule/majuscule.  
- **Harmonisation** : convertir tous les poids de Pokémon en kilogrammes (au lieu d’avoir certains poids en livres, d’autres en kilos).  
- **Agrégation** : calcul du nombre moyen de victoires par type de Pokémon, regroupement des données par région pour des analyses géographiques.  

### Chargement
- **Insertion finale** des données préparées dans la structure cible (data warehouse).  
- Processus souvent automatisé et périodique (toutes les nuits, par exemple, on met à jour la table d’historique de captures).

---

## Différences entre ETL et ELT
- **ETL** : extraction, transformation (hors du data warehouse), puis chargement final dans le data warehouse.  
  - Adapté lorsque l’on connaît **précisément** la structure cible et les transformations nécessaires à l’avance.  
  - Idéal pour des systèmes traditionnels ou des données à structure relativement stable (ex. un Pokédex officiel).  

- **ELT** : extraction, chargement (direct dans le data warehouse), puis transformation **à la demande** dans l’entrepôt.  
  - Souvent plébiscité avec les solutions **cloud** et les très gros volumes de données (ex. logs massifs de combats en ligne).  
  - Permet plus de flexibilité : on charge d’abord tout (données brutes), puis on exécute des transformations analytiques au fur et à mesure des besoins.

---

## Outils d’ETL et d’ELT
- **ETL** : Informatica PowerCenter, Talend, Mage, etc.  
- **ELT** : Snowflake, Google BigQuery, Amazon Redshift, DBT, etc.  

Le choix dépend de la **complexité** des transformations, du **volume** de données et des **besoins** en performances/analyses.  

---

## Exemple d’un mini-processus ETL en pseudo-code
Ci-dessous, un court exemple en pseudo-code (Python simplifié) illustrant la récupération de données Pokémon, leur transformation, puis leur chargement.  

```python
# 1. EXTRACTION
donnees_pokedex = extraire_donnees("pokedex.csv")  # Extraction depuis un fichier CSV
donnees_tournois = extraire_donnees("api_tournois.json")  # Extraction depuis une API

# 2. TRANSFORMATION
def nettoyer_nom_pokemon(nom):
    return nom.strip().title()  # On met la première lettre en majuscule, le reste en minuscule

for pokemon in donnees_pokedex:
    pokemon["nom"] = nettoyer_nom_pokemon(pokemon["nom"])
    pokemon["type_principal"] = pokemon["type_principal"].upper()  # Harmoniser le type en majuscule

# Exemple d'agrégation pour les données de tournois
stats_par_pokemon = {}
for combat in donnees_tournois:
    nom_pokemon = nettoyer_nom_pokemon(combat["pokemon_utilise"])
    if nom_pokemon not in stats_par_pokemon:
        stats_par_pokemon[nom_pokemon] = {"victoires": 0, "combats": 0}
    stats_par_pokemon[nom_pokemon]["combats"] += 1
    if combat["resultat"] == "victoire":
        stats_par_pokemon[nom_pokemon]["victoires"] += 1

# 3. CHARGEMENT
charger_dans_data_warehouse(donnees_pokedex, table="table_pokedex")
charger_dans_data_warehouse(stats_par_pokemon, table="table_stats_tournois")
```

Dans cet exemple fictif, on :
1. **Extrait** des données depuis un CSV (Pokédex) et une API (statistiques de tournois).  
2. **Transforme** ces données pour harmoniser les formats (nettoyage des noms, mise en majuscule pour les types) et calculer quelques agrégats simples (taux de victoires par Pokémon).  
3. **Charge** finalement ces données transformées dans deux tables distinctes d’un data warehouse.  

---

## Ressources supplémentaires
- [Poképédia](https://www.pokepedia.fr/) – Pour approfondir vos connaissances sur l’univers Pokémon.  
- [Snowflake Documentation](https://docs.snowflake.com/) – Exemple de solution cloud pour ELT.  
- [DBT (Data Build Tool)](https://docs.getdbt.com/) – Outil populaire pour l’ELT et le versioning des transformations.  
- [Talend Open Studio](https://www.talend.com/) – Outil open source pour l’ETL.  

---

**En conclusion**, la mise en place d’un data warehouse et l’utilisation d’un processus ETL/ELT constituent des étapes essentielles pour exploiter efficacement des données riches et variées (comme celles de l’univers Pokémon). Grâce à ces approches, il devient plus aisé d’obtenir des analyses fiables et de soutenir des décisions éclairées, qu’il s’agisse de stratégies de compétition, de compréhension de l’évolution des Pokémon, ou encore de projets d’analyse prédictive plus avancés.
```
