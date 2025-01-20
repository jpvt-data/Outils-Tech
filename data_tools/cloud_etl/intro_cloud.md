# **Introduction au Cloud Computing**  

# Sommaire

1. [Aperçu Général du Cloud](#aperçu-général-du-cloud)  
2. [Virtualisation et Conteneurisation](#virtualisation-et-conteneurisation)  
3. [Services Cloud Principaux (IaaS, PaaS, SaaS)](#services-cloud-principaux-iaas-paas-saas)  
4. [Modèles de Déploiement](#modèles-de-déploiement)  
5. [Ressources et Liens Utiles](#ressources-et-liens-utiles)

---

## Aperçu Général du Cloud

**Objectif :**  
- Appréhender les bases du Cloud Computing  
- Mettre en évidence les avantages en termes de flexibilité et de coûts  
- Poser les jalons pour approfondir les services et modèles de déploiement  

**Description :**  
Le Cloud Computing représente une approche moderne de la gestion et de l’exploitation des ressources informatiques. Plutôt que d’acquérir et d’entretenir une infrastructure physique (serveurs, baies de stockage, etc.), l’idée est de louer des ressources à la demande auprès de fournisseurs spécialisés (ex. : AWS, Azure, OVH, IBM Cloud, etc.). Cette externalisation autorise un gain de temps, de coûts et de flexibilité :  
- **Accès rapide** à la puissance de calcul et au stockage  
- **Paiement à l’usage** plutôt qu’un investissement lourd en amont  
- **Mises à jour automatiques** et maintenance simplifiée  

**Illustration :**  
```
   [ Utilisateurs ]  
         |  
         v  
   [ Fournisseur Cloud ] -- (Offre de serveurs, bases de données, stockage)  
         |  
         v  
    [ Accès en ligne ]  
```
*(Schéma conceptuel simplifié : les utilisateurs se connectent au fournisseur Cloud pour bénéficier de ressources partagées.)*

---

## Virtualisation et Conteneurisation

**Pourquoi la virtualisation ?**  
- Permettre l’exécution de plusieurs systèmes d’exploitation (Windows, Linux, etc.) sur un unique serveur physique  
- Favoriser l’optimisation des ressources matérielles  
- Simplifier la gestion et la maintenance des infrastructures  

**Hyperviseur :**  
Jouer le rôle d’orchestrateur entre la machine hôte (serveur physique) et les machines virtuelles.  
- **Hyperviseur de type 1 (bare-metal)** : installé directement sur le matériel (ex. : VMware ESXi).  
- **Hyperviseur de type 2 (hosted)** : installé au-dessus d’un système d’exploitation (ex. : VirtualBox).  

**Conteneurisation :**  
Offrir une isolation applicative plus légère et plus rapide à mettre en place qu’une machine virtuelle complète. Les conteneurs partagent le noyau du système d’exploitation, tout en maintenant des environnements cloisonnés pour chaque application.  
- **Exemple :** Docker, qui facilite la création d’images reproductibles et transportables d’une application ou d’un service.  

---

## Services Cloud Principaux (IaaS, PaaS, SaaS)

### IaaS (Infrastructure as a Service)

**Définition :**  
Proposer un accès à la demande à des composants d’infrastructure (serveurs virtuels, stockage, réseaux). L’IaaS se rapproche le plus de l’environnement « on-premise » traditionnel, en confiant la gestion matérielle au fournisseur Cloud.

**Exemples :**  
- **Azure Virtual Machines** (Microsoft) : permettre de déployer et d’administrer des VM Windows ou Linux.  
- **OpenStack** (solution open-source) : proposer une plateforme IaaS pour créer et gérer des clouds privés ou publics.  

**Points forts :**  
- Ajuster dynamiquement la capacité (CPU, RAM, stockage) en fonction de la charge  
- Payer uniquement les ressources réellement utilisées  
- Réduire les coûts de maintenance matérielle  

---

### PaaS (Platform as a Service)

**Définition :**  
Fournir un environnement complet pour développer, tester et déployer des applications sans gérer soi-même l’infrastructure sous-jacente.  
- Mettre à disposition des bibliothèques, bases de données, serveurs web, systèmes d’intégration continue.  
- Simplifier la configuration et la maintenance.  

**Exemples :**  
- **IBM Cloud Foundry** : héberger et exécuter du code dans divers langages (Java, Node.js, Go, etc.) sans se préoccuper des serveurs.  
- **Azure App Service** : plateforme de déploiement pour créer des sites web et des APIs.  

**Avantages :**  
- Gagner en productivité : se concentrer sur le code et l’expérience utilisateur.  
- Accélérer la mise sur le marché (time-to-market) grâce aux outils intégrés de déploiement et de supervision.  

---

### SaaS (Software as a Service)

**Définition :**  
Proposer des applications utilisables directement en ligne (suite bureautique, messagerie, CRM, outils de visioconférence), gérées entièrement par le fournisseur (infrastructure + mises à jour + maintenance).  

**Exemples :**  
- **Salesforce** : gestion de la relation client (CRM) accessible via un simple navigateur.  
- **Asana ou Trello** : plateformes de gestion de projets collaboratifs en ligne.  

**Avantages :**  
- Accéder aux services depuis n’importe quel appareil connecté à Internet  
- Éviter les installations locales et les mises à jour manuelles  
- Bénéficier d’une tarification souvent modulable (forfait mensuel ou annuel)  

---

## Modèles de Déploiement

**Pourquoi distinguer plusieurs modèles ?**  
La sensibilité des données, la conformité réglementaire et la capacité de personnalisation influencent le choix entre différents types de clouds.  

| Type de Cloud    | Description                                                  | Avantages Clés                               |
|------------------|--------------------------------------------------------------|----------------------------------------------|
| **Cloud Public** | Mutualiser l’infrastructure et les services pour plusieurs clients (ex. : Google Cloud). | Réduire les coûts, garantir une scalabilité élevée, bénéficier de mises à jour gérées par le fournisseur. |
| **Cloud Privé**  | Réserver les ressources à une seule organisation (ex. : cloud interne hébergé sur site). | Maîtriser la sécurité, personnaliser en profondeur, contrôler la localisation des données. |
| **Cloud Hybride**| Combiner cloud privé et public en fonction des besoins (par ex. : pic de charge externalisé vers un cloud public). | Tirer parti de la souplesse et de l’évolutivité du public tout en gardant un contrôle strict sur les données sensibles. |
| **Multi-Cloud**  | Exploiter plusieurs fournisseurs de cloud sans intégration obligatoire (ex. : hébergement d’applications chez AWS et sauvegardes chez Azure). | Répartir les risques, choisir le service le plus performant selon l’usage, éviter la dépendance à un seul acteur. |

---

## Ressources et Liens Utiles

- **Documentation Officielle Microsoft Azure** : [https://learn.microsoft.com/fr-fr/azure/](https://learn.microsoft.com/fr-fr/azure/)  
- **Documentation Officielle Google Cloud** : [https://cloud.google.com/docs](https://cloud.google.com/docs)  
- **Site de la Cloud Security Alliance** : [https://cloudsecurityalliance.org/](https://cloudsecurityalliance.org/)  
- **OpenStack** : [https://www.openstack.org/](https://www.openstack.org/)  

---
