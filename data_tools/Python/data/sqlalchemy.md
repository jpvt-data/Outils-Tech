# SQLAlchemy : Faire du SQL avec Python

## Objectif
- Faire des requêtes SQL en utilisant Python.

---

## Sommaire
1. [Introduction](#introduction)  
2. [Pré-requis](#pré-requis)  
3. [Ressources](#ressources)  
4. [Qu’est-ce qu’un ORM ?](#quest-ce-quun-orm-)  
5. [Installation de SQLAlchemy](#installation-sqlalchemy)  
6. [Les concepts clés de SQLAlchemy](#les-concepts-clés-de-sqlalchemy)  
   - [Le noyau](#le-noyau)  
   - [Le langage SQL](#le-langage-sql)  
   - [Le composant "Expression Language"](#le-composant-expression-language)  
7. [Utilisation de SQLAlchemy](#utilisation-de-sqlalchemy)  
   - [La classe Engine : administrer la base de données](#la-classe-engine--administrer-la-base-de-données)  
   - [La classe Metadata : créer la base de données](#la-classe-metadata--créer-la-base-de-données)  
   - [La classe Table : créer les tables](#la-classe-table--créer-les-tables)  
   - [INSERT : ajouter des valeurs](#insert--ajouter-des-valeurs)  
   - [SELECT : requêter la base](#select--requêter-la-base)  
   - [FETCHONE : afficher les résultats](#fetchone--afficher-les-résultats)  
   - [WHERE : appliquer une condition](#where--appliquer-une-condition)  
   - [UPDATE : mettre à jour une table](#update--mettre-à-jour-une-table)  
   - [DELETE : supprimer une table](#delete--supprimer-une-table)  
   - [La liaison par clé : connecter les tables](#la-liaison-par-clé--connecter-les-tables)  
   - [Les jointures : joindre les tables entre elles](#les-jointures--joindre-les-tables-entre-elles)  

---

## Introduction
SQLAlchemy est un outil Python SQL et un Object Relational Mapper (ORM) proposant toute la puissance de SQL. Il fournit un ensemble complet de modèles de persistance pour accéder efficacement à des bases de données, le tout dans un langage de domaine cohérent intégré à Python.  

---

## Pré-requis
- Connaissance du langage Python.  
- Notions de bases de données relationnelles, DB-API et SQL.  

---

## Ressources
- Documentation officielle : [https://www.sqlalchemy.org/](https://www.sqlalchemy.org/)  
- Tutoriels et guides : [SQLAlchemy Tutorials](https://docs.sqlalchemy.org/en/20/tutorial/index.html)  

---

## Qu’est-ce qu’un ORM ?
Un **Object Relational Mapping** (ORM) établit une correspondance entre un objet Python et une requête SQL. Cela permet de manipuler des données dans un style orienté objet, sans écrire la plupart du code SQL répétitif. Le système ORM assure la traduction automatique des objets Python en types primitifs pour la base de données, et inversement.  

---

## Installation SQLAlchemy
1. Dans un terminal ou un notebook, exécuter :  
   ```bash
   pip install sqlalchemy
   ```
2. Vérifier l’installation :  
   ```python
   import sqlalchemy
   print(sqlalchemy.__version__)
   ```  

---

## Les concepts clés de SQLAlchemy

### Le noyau
Le noyau de SQLAlchemy (SQLAlchemy Core) inclut :
- Le moteur de rendu SQL.  
- L’intégration DB-API (accès bas niveau à la base).  
- La gestion des transactions.  
- La description de schéma (définition des tables, colonnes).  

Ce noyau s’appuie sur le **SQL Expression Language**, qui permet de construire des requêtes SQL en Python.  

### Le langage SQL
SQLAlchemy fournit un **langage d’expression SQL** permettant de représenter directement les constructions d’une base relationnelle (tables, colonnes, jointures, etc.). Cette approche donne la **souplesse** du SQL brut, tout en restant agnostique vis-à-vis du moteur de base de données (SQLite, MySQL, PostgreSQL, etc.).  

### Le composant "Expression Language"
Le langage d’expression est un composant central :  
- Permet de spécifier des instructions SQL en Python.  
- Traduit ensuite ces instructions en SQL brut selon le dialecte de la base.  
- Sert de fondation au mode “Core” et à l’ORM.  

---

## Utilisation de SQLAlchemy

### La classe Engine : administrer la base de données
La classe **Engine** gère la connectivité et le comportement envers la base de données. Elle se crée via la fonction `create_engine()` :

```python
from sqlalchemy import create_engine

engine = create_engine('sqlite:///entreprise.db', echo=True)
```

- `'sqlite:///entreprise.db'` : base SQLite nommée “entreprise.db”.  
- `echo=True` : affiche les requêtes SQL générées dans la console.

Pour MySQL :

```python
engine = create_engine("mysql://user:pwd@localhost/entreprise", echo=True)
```

Principales méthodes :
- `connect()`, `execute()`, `begin()`, `dispose()`.  
- `table_names()` pour lister les noms de tables.  

---

### La classe Metadata : créer la base de données
**Metadata** stocke la description du schéma : tables, vues, contraintes, etc.  
```python
from sqlalchemy import MetaData

meta = MetaData()
```
Les définitions de tables se rassemblent dans `meta`. L’appel `meta.create_all(engine)` crée réellement les tables dans la base.  

---

### La classe Table : créer les tables
Un objet **Table** représente une table SQL :

```python
from sqlalchemy import Table, Column, Integer, String

employes = Table(
    'employes', meta,
    Column('id', Integer, primary_key=True),
    Column('nom', String),
    Column('prenom', String),
    Column('email', String),
    Column('office_code', Integer),
    Column('jobTitle', String)
)

meta.create_all(engine)
```
Ce code exécute un `CREATE TABLE` en arrière-plan.  

---

### INSERT : ajouter des valeurs
Pour insérer des données :

```python
ins = employes.insert().values(
    id=1,
    nom='Doe',
    prenom='John',
    email='jdoe@example.com',
    office_code=101,
    jobTitle='Developer'
)

conn = engine.connect()
conn.execute(ins)
```
SQLAlchemy construit et exécute la requête `INSERT INTO employes (...) VALUES (...)`.  

---

### SELECT : requêter la base
Sélectionner toutes les colonnes :
```python
s = employes.select()
result = conn.execute(s)
```
`employes.select()` génère l’équivalent de `SELECT * FROM employes`.  

---

### FETCHONE : afficher les résultats
`result` est similaire à un curseur DB-API. Récupérer une ligne :
```python
row = result.fetchone()
print(row)
```
Boucler sur toutes les lignes :
```python
for row in result:
    print(row)
```

---

### WHERE : appliquer une condition
Appliquer une condition, par exemple “id > 2” :

```python
s = employes.select().where(employes.c.id > 2)
result = conn.execute(s)
for row in result:
    print(row)
```
`employes.c.id` fait référence à la colonne “id”.

---

### UPDATE : mettre à jour une table
```python
stmt = employes.update().where(employes.c.nom == 'Doe').values(nom='Kasparov')
conn.execute(stmt)
```
Génère `UPDATE employes SET nom='Kasparov' WHERE employes.nom = 'Doe'`.

---

### DELETE : supprimer une table
```python
stmt = employes.delete().where(employes.c.id > 2)
conn.execute(stmt)
```
Supprime les employés dont l’id est supérieur à 2.  

---

### La liaison par clé : connecter les tables
Créer deux tables, l’une référence l’autre via une clé étrangère :

```python
from sqlalchemy import ForeignKey

addresses = Table(
    'addresses', meta,
    Column('id', Integer, primary_key=True),
    Column('emp_id', Integer, ForeignKey('employes.id')),
    Column('postal_add', String),
    Column('email_add', String)
)

meta.create_all(engine)
```
Cette construction spécifie que `addresses.emp_id` fait référence à `employes.id`.

---

### Les jointures : joindre les tables entre elles
Exemple de jointure automatique sur la clé étrangère partagée :

```python
from sqlalchemy.sql import select

j = employes.join(addresses, employes.c.id == addresses.c.emp_id)
stmt = select([employes, addresses]).select_from(j)
result = conn.execute(stmt)
for row in result:
    print(row)
```
Cela construit un `SELECT` avec `JOIN employes ON employes.id = addresses.emp_id`.
