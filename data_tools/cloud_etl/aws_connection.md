# Cloud Computing : Premiers pas sur le cloud avec AWS

## Introduction

**Objectif** :  
Découvrir les premières étapes indispensables pour bien démarrer avec Amazon Web Services, le fournisseur de cloud le plus répandu.  
Création d’un compte, présentation des services de base, gestion des accès et de la sécurité… tout y est pour avoir une base solide et éviter les pièges classiques.

---

## Objectifs

- **Saisir l’importance** des principaux services AWS (EC2, S3, RDS, etc.)  
- **Créer et configurer** un compte AWS en toute sérénité  
- **Prendre en main** la console d’administration (AWS Management Console)  
- **Paramétrer la sécurité** avec IAM (création d’utilisateurs, MFA, bonnes pratiques root)  
- **Installer l’AWS CLI** pour une gestion en ligne de commande  

---

## Sommaire

1. [Aperçu d’AWS et de ses Services Clés](#aperçu-daws-et-de-ses-services-clés)  
2. [Création et Configuration de ton Compte AWS](#création-et-configuration-de-ton-compte-aws)  
3. [Navigation dans la Console de Management AWS](#navigation-dans-la-console-de-management-aws)  
4. [Paramétrage Initial du Compte (Budget et Alertes)](#paramétrage-initial-du-compte-budget-et-alertes)  
5. [Installation et Configuration de l’AWS CLI](#installation-et-configuration-de-laws-cli)  
6. [Gestion des Accès et Sécurité avec IAM](#gestion-des-accès-et-sécurité-avec-iam)  

---

## Aperçu d’AWS et de ses Services Clés

**Amazon Web Services (AWS)** propose un large éventail de solutions cloud :  
- **Amazon EC2** : Lancer des machines virtuelles pour des projets de calcul intensif ou d’analyse de données.  
- **Amazon S3** : Stocker de vastes volumes de données (data lake, backups).  
- **Amazon RDS** : Gérer plus facilement des bases de données relationnelles (MySQL, PostgreSQL, SQL Server…).  
- **Amazon Redshift** : Construire un data warehouse rapide et scalable pour requêter des téraoctets/pétaoctets de données.  
- **AWS Glue** : Mettre en place des pipelines ETL sans trop de config, nettoyer et centraliser les données.  
- **Amazon Athena** : Interroger directement des fichiers dans S3 avec du SQL, sans devoir mettre en place un cluster.  

**Pourquoi AWS ?**  
- Énorme catalogue de services, couvrant l’hébergement, l’analytique, le machine learning.  
- Facturation à l’utilisation, simplifiant la maîtrise des coûts.  
- Haute disponibilité, centres de données présents partout dans le monde.  
- Solides outils de sécurité et normes de conformité (GDPR, ISO 27001, etc.).  
- Grande communauté, tutoriels abondants, support technique complet.  

---

## Création et Configuration de ton Compte AWS

1. **Aller sur la plateforme AWS** et cliquer sur « Sign in to the Console ».  
2. **Créer un compte** en indiquant email et identifiants.  
3. **Renseigner les infos de paiement** (même si usage du free tier) pour valider ton identité.  
4. **Choisir le plan de support** : le basique et gratuit pour démarrer.  
5. **Confirmer** et accéder à la console de management.  

*(Attention : respecter les limites du free tier et surveiller la facturation pour éviter toute mauvaise surprise.)*

---

## Navigation dans la Console de Management AWS

Une fois connecté à **[AWS Management Console](https://aws.amazon.com/console/)**, quelques éléments clés :  
- **Search bar** : taper le nom d’un service (S3, EC2, IAM…) pour y accéder en un clic.  
- **Cost Management** : surveiller et gérer en direct la consommation et le budget.  
- **Zone géographique** (Region) : héberger tes ressources dans la région adaptée (latence, conformité).  
- **Compte** : menu d’options, accès à la facturation, support, déconnexion.  
- **CloudShell** : ouvrir un terminal en ligne pour exécuter des commandes AWS CLI sans configurer de client local.

---

## Paramétrage Initial du Compte (Budget et Alertes)

Pour éviter les mauvaises surprises financières :  
1. **Ouvrir** le menu « Billing and Cost Management » via le bouton de compte (en haut à droite).  
2. **Créer un budget** (ex. : Zero Spend Budget) en utilisant la fonctionnalité Budget → Create Budget.  
3. **Configurer des alertes** par email pour être prévenu si un dépassement du free tier se profile.

*(Revoir régulièrement l’état de la consommation pour rester dans la limite du gratuit.)*

---

## Installation et Configuration de l’AWS CLI

L’AWS Command Line Interface (CLI) autorise la gestion des ressources directement via le terminal.

### Sur macOS

1. **Installer Homebrew** (si ce n’est pas déjà fait) :
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   brew update
   ```
2. **Installer awscli** :  
   ```bash
   brew install awscli
   ```
3. **Vérifier** :
   ```bash
   aws --version
   ```

### Sur Windows

1. **Télécharger** l’installateur [AWSCLIV2.msi](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)  
2. **Lancer** l’installation en cliquant sur le fichier .msi et suivre les indications.  
3. **Tester** :
   ```bash
   aws --version
   ```

*(Après l’install, configurer l’awscli en entrant les identifiants IAM via `aws configure`.)*

---

## Gestion des Accès et Sécurité avec IAM

### Principe IAM

**IAM (Identity and Access Management)** permet de contrôler les droits d’accès aux services AWS. Plutôt que d’utiliser le compte root pour tout (dangereux), mieux vaut créer des comptes IAM dédiés.  
- **Utilisateurs** : entités (personnes ou apps) avec identifiants propres.  
- **Groupes** : regrouper plusieurs utilisateurs et appliquer des politiques d’accès à tout le groupe.  
- **Rôles** : attribuer des permissions à un service ou une instance EC2, sans clés d’accès dans le code.  

### Création d’un Utilisateur IAM

1. **Rechercher** IAM depuis la console.  
2. **Cliquer** sur « Users » → « Create User ».  
3. **Définir** un nom d’utilisateur (ex. : “admin-daily”) et cocher l’accès console (autogenerated password).  
4. **Choisir** les permissions : par exemple « AdministratorAccess » (à affiner si besoin).  
5. **Télécharger** les identifiants temporaires (.csv).  
6. **Se déconnecter** du compte root, puis se reconnecter avec ce nouveau compte IAM.  
7. **Changer le mot de passe** dès la première connexion.

### Activer le MFA (Multi-Factor Authentication)

1. **Revenir** sur le compte root (rarement) pour configurer le MFA.  
2. **Aller** dans « My Security Credentials » → « Activate MFA ».  
3. **Choisir** Virtual MFA Device (ex. : Google Authenticator, Authy).  
4. **Scanner** le QR code → saisir deux codes consécutifs pour confirmer.  
5. **Terminer** en validant Assign MFA.  

*(Le compte root ne sert que pour les actions critiques ou la facturation ; pour toutes les tâches quotidiennes, privilégier l’utilisateur IAM.)*
