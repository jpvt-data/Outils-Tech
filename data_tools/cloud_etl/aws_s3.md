# Cloud Computing : Présentation de S3

## Introduction

**Amazon S3 (Simple Storage Service)** est l’un des services phares d’AWS pour stocker ses données en mode objet. Contrairement à un stockage de fichiers classique, S3 adopte une logique de *buckets* et *d’objets*, assurant une **scalabilité énorme**, une **disponibilité élevée** et une **durabilité** redoutable. Cette fiche explique les fondements de S3, comment l’utiliser (par la console web et la CLI), et donne quelques clés sur la gestion des accès et de la sécurité.

---

## Objectifs

- **Comprendre** le principe de stockage d’objets et la notion de bucket  
- **Découvrir** l’interface S3 : création, configuration, et propriétés importantes  
- **Uploader et télécharger** des objets via la console ou la CLI  
- **Mettre en place les policies** et configurer les accès  
- **Appréhender** les options de sécurité : blocage de l’accès public, versioning, chiffrement, etc.  
- **Effectuer** le nettoyage final (suppression des fichiers et du bucket)

---

## Sommaire

1. [Présentation d’Amazon S3](#présentation-damazon-s3)  
   - [Buckets et Noms Uniques](#buckets-et-noms-uniques)  
   - [Scalabilité, Disponibilité, Durabilité](#scalabilité-disponibilité-durabilité)  
   - [Sécurité et Conformité](#sécurité-et-conformité)  
   - [Performance](#performance)  
2. [Prise en Main d’Amazon S3](#prise-en-main-damazon-s3)  
   - [Méthode AWS Console Management](#méthode-aws-console-management)  
   - [Méthode AWS CLI](#méthode-aws-cli)  
3. [Uploader et Télécharger des Fichiers](#uploader-et-télécharger-des-fichiers)  
   - [Via la Console](#méthode-aws-console-management-1)  
   - [Via la CLI](#méthode-aws-cli-1)  
   - [Métadonnées dans S3](#explication-des-métadonnées-dun-objet-dans-s3)  
4. [Cleanup (Suppression)](#cleanup)  
   - [Console AWS](#1-utiliser-aws-management-console)  
   - [CLI AWS](#2-utiliser-aws-cli)  

---

## Présentation d’Amazon S3

### Buckets et Noms Uniques

Un **bucket** est comme un « conteneur » où sont stockés les objets. Chaque bucket doit porter un nom **unique**, au moins à l’échelle de la région AWS choisie.  
- **Exemple** : un objet nommé `mon-objet` dans le bucket `exemple-bucket` en région `us-west-2` aurait comme URL :  
  ```
  https://exemple-bucket.s3.us-west-2.amazonaws.com/mon-objet
  ```

### Scalabilité, Disponibilité, Durabilité

- **Scalabilité** : ne plus se soucier de la taille. S3 tolère des pétaoctets de données ou plus, sans configuration complexe.  
- **Durabilité de 99.999999999% (11 9)** : réplication automatique des objets dans plusieurs centres de données.  
- **Disponibilité de 99.99%** : garantissant un accès fiable, même si un data center tombe en panne.

### Sécurité et Conformité

- **Chiffrement** possible au repos (SSE-S3, SSE-KMS) et en transit (HTTPS).  
- **Politiques de contrôle d’accès (policies)** pour gérer qui peut lire, écrire ou lister les objets.  
- **Conformité** : S3 répond aux normes HIPAA, PCI-DSS, RGPD, SOC, etc.  

### Performance

Conçu pour supporter un grand volume de requêtes simultanées, S3 est adapté aux applications exigeant un accès rapide et à grande échelle.

---

## Prise en Main d’Amazon S3

### Méthode AWS Console Management

1. **Se connecter** en tant qu’utilisateur IAM.  
2. **Choisir la Région** (menu déroulant en haut à droite).  
3. **Rechercher « S3 »** dans la barre de recherche, puis sélectionner le service.  
4. **Créer un nouveau bucket** via le bouton « Create bucket ».  
   - **Nom du Bucket** : unique et global.  
   - **Région** : localisation (ex. : `eu-west-3` pour Paris).  
   - **Blocage de l’accès public** : par défaut, l’accès est bloqué. À débloquer si besoin (pour un hébergement public de fichiers).  
   - **Versioning** (optionnel) : conserver l’historique des modifications.  
   - **Tags** (optionnel) : paires clé-valeur pour organiser les ressources.  
   - **Encryption** : activer SSE-S3 ou SSE-KMS pour chiffrer.  
5. **Valider**. Le nouveau bucket apparaît alors dans la liste.

### Méthode AWS CLI

#### 1) Configurer l’AWS CLI

1. **Générer** des clés d’accès IAM depuis la console (IAM → Users → onglet « Security credentials » → Create access key).  
2. **Configurer la CLI** en local :  
   ```bash
   aws configure
   ```
   - **Access Key ID**  
   - **Secret Access Key**  
   - **Default region** (ex.: `eu-west-3`)  
   - **Default output format** (JSON recommandé)  

3. **Vérifier** :  
   ```bash
   aws s3 ls
   ```
   (Liste les buckets si tout est bien configuré)

#### 2) Créer un Bucket avec la CLI

```bash
aws s3api create-bucket \
  --bucket mon-bucket-exemple \
  --region eu-west-3 \
  --create-bucket-configuration LocationConstraint=eu-west-3
```
- *mon-bucket-exemple* : nom globalement unique.  
- *LocationConstraint* obligatoire si la région n’est pas `us-east-1`.

---

## Uploader et Télécharger des Fichiers

### Méthode AWS Console Management

1. **Ouvrir S3** → cliquer sur le bucket souhaité.  
2. **Upload** :  
   - Bouton « Upload » → « Add files » (ou « Add folder ») → sélectionner le fichier local.  
   - Définir les options (chiffrement, permissions) → lancer l’upload.  
3. **Download** :  
   - Cocher l’objet → « Download ».

### Méthode AWS CLI

**Upload** :
```bash
aws s3 cp fichier_local.txt s3://nom-du-bucket/
```
**Download** :
```bash
aws s3 cp s3://nom-du-bucket/fichier_local.txt ./destination_locale/
```

---

### Explication des Métadonnées d’un Objet dans S3

- **Object Key** : chemin et nom de l’objet dans le bucket (ex. : `images/photo.jpg`).  
- **Size** : taille en octets.  
- **Last Modified** : date/heure de dernière modification.  
- **Content-Type** : type MIME (ex. : `image/jpeg`).  
- **Version ID** : identifiant si le versioning est activé.  
- **Encryption** : information sur le chiffrement.  
- **Etag** : hash (MD5) utilisé pour vérifier l’intégrité des données.  
- **Object URL** : lien d’accès direct (utilisable si le fichier est rendu public ou si l’on a des credentials).

---

## Cleanup

### 1) Utiliser AWS Management Console

1. **Supprimer les objets**  
   - Sélectionner les objets dans le bucket → bouton « Delete » → taper « permanently delete ».  
2. **Supprimer le bucket**  
   - Sur la page principale S3, sélectionner le bucket → « Delete bucket » → saisir le nom du bucket → valider.

### 2) Utiliser AWS CLI

1. **Vider le bucket** :  
   ```bash
   aws s3 rm s3://nom-du-bucket --recursive
   ```
2. **Supprimer le bucket** :  
   ```bash
   aws s3 rb s3://nom-du-bucket
   ```
*(Veiller à ce que le bucket soit vide avant cette opération.)*
