# Correction

## 1. Création de la base de données 
```sql
CREATE DATABASE magasin_en_ligne;
USE magasin_en_ligne;

CREATE TABLE categories (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(255) NOT NULL
);

CREATE TABLE produits (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(255) NOT NULL,
    prix DECIMAL(10, 2) NOT NULL,
    categorie_id INT,
    FOREIGN KEY (categorie_id) REFERENCES categories(ID)
);

CREATE TABLE clients (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(255) NOT NULL,
    prenom VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    date_inscription DATE
);

CREATE TABLE commandes (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    client_id INT,
    date_commande DATE,
    FOREIGN KEY (client_id) REFERENCES clients(ID)
);

CREATE TABLE details_commandes (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    commande_id INT,
    produit_id INT,
    quantite INT,
    FOREIGN KEY (commande_id) REFERENCES commandes(ID),
    FOREIGN KEY (produit_id) REFERENCES produits(ID)
);
```

## 2. Ajout des données 

```SQL
INSERT INTO categories (nom) VALUES ('Électronique'), ('Vêtements'), ('Livres');

INSERT INTO produits (nom, prix, categorie_id) VALUES ('Smartphone', 599.99, 1), ('T-shirt', 19.99, 2), ('Roman', 14.99, 3);

INSERT INTO clients (nom, prenom, email, date_inscription) VALUES ('Dupont', 'Alice', 'alice.dupont@example.com', '2023-01-01'), ('Martin', 'Bob', 'bob.martin@example.com', '2023-02-01');

INSERT INTO commandes (client_id, date_commande) VALUES (1, '2023-03-01'), (2, '2023-03-05');

INSERT INTO details_commandes (commande_id, produit_id, quantite) VALUES (1, 1, 1), (1, 3, 2), (2, 2, 3);
```

## 3. Requêtes de Sélection
```sql
SELECT * FROM produits WHERE categorie_id = (SELECT ID FROM categories WHERE nom = 'Électronique');

SELECT * FROM commandes WHERE client_id = 1;

SELECT produits.nom, details_commandes.quantite
FROM details_commandes
INNER JOIN produits ON details_commandes.produit_id = produits.ID
WHERE details_commandes.commande_id IN (SELECT ID FROM commandes WHERE client_id = 1);
```

## 4. Jointures
```sql
SELECT produits.nom, categories.nom AS categorie
FROM produits
INNER JOIN categories ON produits.categorie_id = categories.ID;

SELECT clients.nom, clients.prenom, produits.nom, details_commandes.quantite, commandes.date_commande
FROM commandes
INNER JOIN clients ON commandes.client_id = clients.ID
INNER JOIN details_commandes ON commandes.ID = details_commandes.commande_id
INNER JOIN produits ON details_commandes.produit_id = produits.ID;
```

## 5. Mise à Jour et Suppression

```sql
UPDATE produits SET prix = 549.99 WHERE ID = 1;

DELETE FROM commandes WHERE ID = 2;
```

## 6. Requêtes Avancées
```sql
SELECT clients.nom, clients.prenom, COUNT(details_commandes.ID) AS nombre_produits
FROM clients
LEFT JOIN commandes ON clients.ID = commandes.client_id
LEFT JOIN details_commandes ON commandes.ID = details_commandes.commande_id
GROUP BY clients.ID;

SELECT produits.nom
FROM produits
LEFT JOIN details_commandes ON produits.ID = details_commandes.produit_id
WHERE details_commandes.produit_id IS NULL;
```