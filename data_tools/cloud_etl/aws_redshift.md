# Cloud Computing : AWS Redshift

## Objectifs
- Comprendre ce qu’est Amazon Redshift et son rôle dans l’écosystème AWS.  
- Découvrir le fonctionnement d’Amazon Redshift, y compris son architecture et ses concepts clés.  
- Identifier les avantages d’Amazon Redshift pour l’analyse de données à grande échelle.  
- Créer une instance Amazon Redshift Serverless et la configurer selon les meilleures pratiques.  
- Paramétrer les identifiants d’accès à Redshift en utilisant AWS Secrets Manager.  
- Configurer un Security Group pour sécuriser l’accès TCP à l’instance Redshift.  
- Charger des données dans Redshift avec SQLAlchemy et vérifier le bon fonctionnement de l’instance.

---

## Sommaire
1. [Présentation d’Amazon Redshift](#présentation-damazon-redshift)  
   - [Qu’est-ce qu’Amazon Redshift ?](#quest-ce-quamazon-redshift-)  
   - [Comment fonctionne Amazon Redshift ?](#comment-fonctionne-amazon-redshift-)  
2. [Prise en main d’Amazon Redshift Serverless](#prise-en-main-damazon-redshift-serverless)  
   - [Création d’une instance Redshift Serverless](#création-dune-instance-redshift-serverless)  
   - [Paramétrage des identifiants avec AWS Secrets Manager](#paramétrage-des-identifiants-avec-aws-secrets-manager)  
   - [Configuration du Security Group](#configuration-du-security-group)  
   - [Pourquoi ces configurations sont importantes](#pourquoi-ces-configurations-sont-importantes)  
   - [Chargement et test de données avec SQLAlchemy](#chargement-et-test-de-données-avec-sqlalchemy)  
   - [Vérification de l’Importation des Données dans Redshift](#vérification-de-limportation-des-données-dans-redshift)  
3. [Nettoyage des Ressources AWS](#nettoyage-des-ressources-aws)  
   - [1. Supprimer le Workgroup Redshift Serverless](#1-supprimer-le-workgroup-redshift-serverless)  
   - [2. Supprimer le Namespace Redshift Serverless](#2-supprimer-le-namespace-redshift-serverless)  
   - [3. Supprimer le Secret dans AWS Secrets Manager](#3-supprimer-le-secret-dans-aws-secrets-manager)  
   - [4. Vérifier les Clés dans AWS Key Management Service (KMS)](#4-vérifier-les-clés-dans-aws-key-management-service-kms)

---

## Présentation d’Amazon Redshift

### Qu’est-ce qu’Amazon Redshift ?
Amazon Redshift est un service d’entrepôt de données (data warehouse) entièrement géré, conçu pour le stockage et l’analyse de grandes quantités de données. Basé sur PostgreSQL, il est spécialement optimisé pour les charges de travail OLAP (Online Analytical Processing), ce qui en fait un choix adapté pour les contextes exigeant des analyses complexes à grande échelle.

Son architecture de traitement massivement parallèle (MPP) permet d’exécuter des requêtes jusqu’à dix fois plus vite que d’autres data warehouses. Ce modèle distribue la charge de travail à travers plusieurs nœuds de calcul, renforçant l’efficacité et la rapidité d’exécution. Redshift stocke également les données en colonnes, ce qui réduit la quantité de données à parcourir et améliore considérablement les performances pour les requêtes analytiques lourdes.

La tarification “pay as you go” permet de payer uniquement les ressources réellement utilisées. De plus, l’intégration avec des outils de Business Intelligence (BI) comme Amazon QuickSight ou Tableau facilite l’exploration et la visualisation des données. Grâce à ces fonctionnalités, Amazon Redshift propose une solution performante et flexible pour stocker, analyser et extraire des insights d’importants volumes de données.

> **Rappel sur le stockage en colonne** : Le stockage en colonne (columnar storage) organise les données par colonne plutôt que par ligne, ce qui est très efficace pour les requêtes analytiques puisqu’il devient possible de lire uniquement les colonnes nécessaires.

---

### Comment fonctionne Amazon Redshift ?
Amazon Redshift s’appuie sur plusieurs composants clés : le Leader Node, les Compute Nodes et les Slices. Lorsqu’une requête est envoyée à Redshift, les étapes suivantes sont réalisées :

1. **Leader Node**  
   - Réception et planification : Le Leader Node reçoit la requête SQL, l’analyse et crée un plan d’exécution définissant la stratégie de filtrage, d’agrégation et de regroupement.  
   - Distribution des tâches : Le Leader Node répartit le travail en plusieurs segments, attribués aux Compute Nodes.

2. **Compute Nodes**  
   - Filtrage des données : Chaque Compute Node reçoit sa portion de données (appelée Slice) et applique les filtres définis (par exemple, restreindre la plage de dates).  
   - Agrégation locale : Les Compute Nodes calculent localement les sommes ou autres mesures demandées (ex. `SUM(montant)` pour chaque produit).

3. **Combinaison des résultats**  
   - Agrégation globale : Les résultats partiels sont renvoyés au Leader Node, qui les fusionne pour produire la réponse finale à la requête.

4. **Envoi de la réponse**  
   - Le Leader Node retourne le résultat complet à l’émetteur de la requête.

---

## Prise en main d’Amazon Redshift Serverless

### Création d’une instance Redshift Serverless
1. Ouvrir la console AWS et rechercher **Amazon Redshift**.  
2. Accéder à l’option **Serverless** (cliquer sur “Try Redshift Serverless free trial” si proposé).  
3. Créer un **Namespace** (par exemple `my-redshift-namespace`), définir une base de données (par exemple `db_redshift`) et des identifiants d’administration (nom d’utilisateur, mot de passe).  
4. Créer un **Workgroup** (par exemple `my-serverless-workgroup`) en limitant la capacité maximale (par exemple 32 RPUs) pour contrôler les coûts.  
5. Choisir un **VPC**, configurer les sous-réseaux et groupes de sécurité (AWS peut en générer par défaut).  
6. Vérifier les paramètres et cliquer sur **Create** pour finaliser la création.  
7. Consulter le **tableau de bord** Redshift Serverless pour visualiser les métriques, l’état du Namespace et du Workgroup.

---

### Paramétrage des identifiants avec AWS Secrets Manager
1. Accéder à **AWS Secrets Manager** depuis la console AWS.  
2. Créer un nouveau secret en choisissant **Credentials for Amazon Redshift**.  
3. Renseigner les paires `username` / `password` et sélectionner le workgroup Redshift correspondant.  
4. Nommer le secret (par exemple `redshift/credentials`), éventuellement ajouter des tags, et stocker le secret.  
5. Récupérer le secret dans les scripts Python en utilisant Boto3 (ex. `client.get_secret_value(SecretId='redshift/credentials')`).

**Avantages** :  
- Sécurité renforcée : Les identifiants ne sont pas en clair dans le code.  
- Automatisation : Possibilité de faire tourner la rotation automatique des mots de passe.  

---

### Configuration du Security Group
1. Depuis la console Redshift, sélectionner le **Workgroup** et ouvrir la section **Network and Security**.  
2. Cliquer sur le groupe de sécurité (ex. `sg-xxxxxx`) pour accéder aux **Inbound rules**.  
3. Ajouter une nouvelle règle pour autoriser le protocole TCP sur le **port 5439** (port Redshift) depuis la source `My IP`.  
4. Activer l’option **Publicly accessible** si l’accès doit être autorisé depuis Internet public.

---

### Pourquoi ces configurations sont importantes
- Autoriser explicitement l’adresse IP sur le port Redshift restreint l’accès à l’instance.  
- Rendre l’instance **Publicly accessible** est nécessaire si elle n’est pas appelée depuis d’autres ressources internes AWS.  
- Stocker les identifiants dans Secrets Manager évite de compromettre la sécurité en les plaçant dans le code ou les variables d’environnement.

---

### Chargement et test de données avec SQLAlchemy

**Préparation** :  
- Dans un environnement Python, installer les dépendances nécessaires :  
  ```bash
  pip install boto3 pandas==2.1.4 sqlalchemy-redshift psycopg2-binary
  ```

**Exemple de script** (fichier `import_redshift.py`) :

```python
import boto3
import json
import pandas as pd
from sqlalchemy import create_engine
from botocore.exceptions import ClientError

def get_secret() -> dict[str, str]:
    secret_name = "redshift/credentials"
    region_name = "eu-west-3"
    session = boto3.session.Session()
    client = session.client(service_name="secretsmanager", region_name=region_name)

    try:
        get_secret_value_response = client.get_secret_value(SecretId=secret_name)
    except ClientError as e:
        raise e

    secret = get_secret_value_response["SecretString"]
    secret_dict = json.loads(secret)
    return secret_dict

if __name__ == "__main__":
    secret = get_secret()
    username = secret.get("username")
    password = secret.get("password")
    host = secret.get("host")
    port = secret.get("port")
    database = "pokemondb"  # Changer le nom de la base ici

    engine = create_engine(
        f"redshift+psycopg2://{username}:{password}@{host}:{port}/{database}"
    )

    data = {
        "id": [1, 2, 3],
        "name": ["Alice", "Bob", "Charlie"],
        "age": [25, 30, 35]
    }
    df = pd.DataFrame(data)

    df.to_sql("test_table", engine, if_exists="replace", index=False, schema="public")
    print("Données importées avec succès dans la table 'test_table'.")
```

---

### Vérification de l’Importation des Données dans Redshift
1. Dans la console Redshift, sélectionner **Query Data**.  
2. Se connecter en utilisant les informations issues de Secrets Manager ou en saisissant manuellement l’hôte, le port, l’utilisateur et le mot de passe.  
3. Exécuter une requête de test :

```sql
SELECT *
FROM test_table;
```

4. Vérifier que les lignes insérées (Alice, Bob, Charlie) apparaissent correctement.

---

## Nettoyage des Ressources AWS

### 1. Supprimer le Workgroup Redshift Serverless
- **CLI** :  
  ```bash
  aws redshift-serverless delete-workgroup --workgroup-name <nom_workgroup>
  ```
- **Console** :  
  - Ouvrir Redshift Serverless.  
  - Sélectionner le workgroup.  
  - Choisir **Delete** dans le menu d’actions.

---

### 2. Supprimer le Namespace Redshift Serverless
- **CLI** :  
  ```bash
  aws redshift-serverless delete-namespace --namespace-name <nom_namespace>
  ```
- **Console** :  
  - Sélectionner le namespace dans Redshift Serverless.  
  - Cliquer sur **Delete**.

---

### 3. Supprimer le Secret dans AWS Secrets Manager
- **CLI** :  
  ```bash
  aws secretsmanager delete-secret --secret-id <identifiant_du_secret>
  ```
- **Console** :  
  - Ouvrir Secrets Manager.  
  - Sélectionner le secret.  
  - Cliquer sur **Delete**.

---

### 4. Vérifier les Clés dans AWS Key Management Service (KMS)
- Ouvrir KMS depuis la console AWS.  
- Vérifier l’existence de clés et, si nécessaire, les désactiver ou les supprimer (après avoir pris en compte les ressources qui pourraient en dépendre).

---

