# Analyse des requêtes SQL - Sujet Bloc 1

## Présentation des requêtes

Chaque requête SQL a été conçue pour répondre précisément aux questions posées. Voici une explication détaillée des démarches suivies pour chaque question.

---

## Requêtes et explications

### Question 1
**Listez tous les produits avec leurs codes produits et noms.**

```sql
SELECT productCode, productName FROM products;
```
**Démarche :** 
- Sélectionner les colonnes `productCode` et `productName` depuis la table `products`.
- Il n'y a pas de jointure nécessaire car toutes les informations se trouvent dans la même table.

---

### Question 2
**Trouvez les noms de tous les clients ainsi que la ville où ils se trouvent.**

```sql
SELECT customerName, city FROM customers;
```
**Démarche :** 
- Récupérer `customerName` et `city` depuis la table `customers`.
- Aucune jointure requise, car toutes les données nécessaires sont dans `customers`.

---

### Question 3
**Récupérez le numéro de commande et la date de commande pour toutes les commandes passées par le client numéro 103.**

```sql
SELECT orderNumber, orderDate FROM orders WHERE customerNumber = 103;
```
**Démarche :** 
- Sélectionner `orderNumber` et `orderDate` dans `orders`.
- Filtrer les résultats avec `WHERE customerNumber = 103` pour ne récupérer que les commandes du client 103.

---

### Question 4
**Affichez les détails des commandes, y compris le code produit et la quantité commandée.**

```sql
SELECT orderNumber, productCode, quantityOrdered FROM orderdetails;
```
**Démarche :** 
- Extraire `orderNumber`, `productCode` et `quantityOrdered` depuis la table `orderdetails`.
- Aucune jointure nécessaire car ces informations sont toutes présentes dans `orderdetails`.

---

### Question 5
**Affichez les commandes avec le nom du client correspondant.**

```sql
SELECT orders.orderNumber, customers.customerName 
FROM orders 
JOIN customers ON orders.customerNumber = customers.customerNumber;
```
**Démarche :** 
- Récupérer `orderNumber` depuis `orders` et `customerName` depuis `customers`.
- Utiliser un `JOIN` sur `customerNumber` pour lier les commandes aux clients.

---

### Question 6
**Trouvez les produits qui n'ont jamais été commandés.**

```sql
SELECT p.productCode, p.productName 
FROM products p 
LEFT JOIN orderdetails o ON p.productCode = o.productCode 
WHERE o.productCode IS NULL;
```
**Démarche :** 
- Utiliser un `LEFT JOIN` entre `products` et `orderdetails`.
- Sélectionner uniquement les produits sans correspondance dans `orderdetails` (`WHERE o.productCode IS NULL`).

---

### Question 7
**Affichez le nombre total de commandes passées par chaque client.**

```sql
SELECT customerNumber, COUNT(orderNumber) AS totalCommandes 
FROM orders 
GROUP BY customerNumber;
```
**Démarche :** 
- Grouper par `customerNumber` pour compter les commandes de chaque client.
- Utiliser `COUNT(orderNumber)` pour obtenir le nombre total de commandes.

---

### Question 8
**Affichez les revenus générés par chaque client.**

```sql
SELECT c.customerName, SUM(od.quantityOrdered * od.priceEach) AS revenu_total 
FROM customers c 
JOIN orders o ON c.customerNumber = o.customerNumber 
JOIN orderdetails od ON o.orderNumber = od.orderNumber 
GROUP BY c.customerName;
```
**Démarche :** 
- Joindre `customers`, `orders`, et `orderdetails`.
- Calculer le revenu en multipliant `quantityOrdered * priceEach`, puis utiliser `SUM()`.
- Grouper par `customerName`.

---

### Question 9
**Listez les clients qui n'ont jamais passé de commande.**

```sql
SELECT c.customerNumber, c.customerName 
FROM customers c 
LEFT JOIN orders o ON c.customerNumber = o.customerNumber 
WHERE o.customerNumber IS NULL;
```
**Démarche :** 
- Utiliser un `LEFT JOIN` entre `customers` et `orders`.
- Sélectionner uniquement les clients qui n'ont pas de correspondance dans `orders`.

---

### Question 10
**Affichez la date de la première commande passée par chaque client.**

```sql
SELECT customerNumber, MIN(orderDate) AS premiereCommande 
FROM orders 
GROUP BY customerNumber;
```
**Démarche :** 
- Grouper par `customerNumber`.
- Utiliser `MIN(orderDate)` pour obtenir la première commande.

---

## Compétences SQL utilisées

- **Sélections spécifiques** : `SELECT column1, column2 FROM table`
- **Jointures** : `JOIN`, `LEFT JOIN`
- **Agrégations** : `COUNT()`, `SUM()`, `MIN()`
- **Filtrage** : `WHERE`, `HAVING`
- **Regroupements** : `GROUP BY`

---

## Questions pièges potentielles et réponses rapides

### 1. Pourquoi utiliser `LEFT JOIN` pour identifier les produits non commandés ?
Il permet d'inclure tous les produits et d'afficher `NULL` pour ceux sans correspondance.

### 2. Pourquoi ne pas utiliser `HAVING` au lieu de `WHERE` pour filtrer des commandes ?
`HAVING` est utilisé pour filtrer après une agrégation (`GROUP BY`), alors que `WHERE` filtre avant.

### 3. Quelle est la différence entre `INNER JOIN` et `LEFT JOIN` ?
`INNER JOIN` ne garde que les correspondances, tandis que `LEFT JOIN` garde tous les enregistrements de la table de gauche.

---

Avec ces explications, tu es prêt pour ta présentation orale !

