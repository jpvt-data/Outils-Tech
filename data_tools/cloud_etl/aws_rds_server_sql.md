# Installer une base de données RDS sur AWS

## Sommaire
1. **Introduction**
2. **Création de la base de données RDS**
3. **Configuration de la base de données**
4. **Accès et connexion à la base de données**
5. **Recommandations importantes**

---

## 1. Introduction

AWS RDS (Relational Database Service) permet de déployer facilement une base de données relationnelle dans le cloud. Cette fiche technique vous guide étape par étape pour configurer une base de données MySQL en utilisant l'offre gratuite AWS.

---

## 2. Création de la base de données RDS

### Étapes :
1. **Accéder à AWS RDS** :
   - Connectez-vous à la console AWS.
   - Naviguez vers le service **RDS**.

2. **Créer une base de données** :
   - Cliquez sur **Créer une base de données**.
   - Sélectionnez le moteur **MySQL** (compatible avec l'offre gratuite).

3. **Choisir les options de l'offre gratuite** :
   - Laissez les options par défaut et vérifiez que l'offre gratuite est activée.

4. **Configurer les identifiants** :
   - Donnez un nom à votre base de données.
   - Définissez un utilisateur principal et un mot de passe sécurisé.

---

## 3. Configuration de la base de données

### Étapes supplémentaires :
1. **VPC et groupe de sécurité** :
   - Créez un nouveau **VPC** (Virtual Private Cloud).
   - Configurez un **groupe de sécurité** personnalisé pour autoriser les connexions.

2. **Paramètres d'accès** :
   - Configurez l'accès public si vous souhaitez vous connecter depuis l'extérieur.
   - Désactivez l'option "connecter à EC2" pour cette étape (sauf si nécessaire).

3. **Validation et création** :
   - Confirmez les paramètres et lancez la création de la base de données.
   - Patientez jusqu'à ce que la base soit prête (statut visible dans la console).

---

## 4. Accès et connexion à la base de données

1. **Récupérer les informations de connexion** :
   - Une fois la base créée, cliquez sur le nom de la base de données pour voir :
     - Le nom de l'hôte
     - L'utilisateur principal
     - Le mot de passe (défini lors de la création)

2. **Utiliser un outil de connexion** :
   - Exemple : **MySQL Workbench** ou tout autre client MySQL.
   - Entrez les informations de connexion pour accéder à la base.

3. **Charger des données** :
   - Importez un fichier CSV (comme `bd.csv`) pour créer ou remplir une table SQL sur le serveur MySQL RDS.

---

## 5. Recommandations importantes

1. **Gestion des coûts** :
   - **Fermez toutes les instances** après utilisation pour éviter des frais inattendus.

2. **Sécurité** :
   - Évitez de configurer un accès public à moins que cela ne soit absolument nécessaire.
   - Protégez vos identifiants (mot de passe, utilisateur).

3. **Sauvegarde** :
   - Activez les sauvegardes automatiques si vous prévoyez d'utiliser la base sur le long terme.

---

## Ressources supplémentaires

- [Documentation officielle AWS RDS](https://aws.amazon.com/rds/)
- [Tutoriels AWS gratuits](https://aws.amazon.com/training/)
- [Guide MySQL Workbench](https://dev.mysql.com/doc/workbench/en/)
