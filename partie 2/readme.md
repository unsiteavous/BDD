# Activité : Gestion d'une Base de Données de Magasin en Ligne
Objectif :

Créer une base de données pour un magasin en ligne, y ajouter des données, et exécuter diverses requêtes pour récupérer et manipuler les informations.
Étapes :

## 1. Création de la Base de Données
-  Créez un utilisateur et sa base de données associée nommée ecommerce.
-  Créez le MCD comprenant les tables suivantes :
   - **produits** : Pour stocker les informations sur les produits. Elle aura les attributs suivants : ID, Nom, Prix

   - **categories** : Pour stocker les informations sur les catégories de produits. elle aura deux attributs : ID, Nom

   - **clients** : Pour stocker les informations sur les clients. Elle aura les attributs suivants : ID, Nom, Prénom, Email, date_inscription

   - **commandes** : Pour stocker les informations sur les commandes. Elle aura les attributs suivants : ID, date_commande

   - **details_commandes** : Pour stocker les détails des produits commandés. Elle aura les attributs suivants : ID,quantite
- Ecrivez le code SQL correspondant. 

## 2. Ajout de Données

Ajoutez des données dans les tables categories, produits, clients, commandes, et details_commandes.

### Tableau des Données

#### Table : `categories`
| ID | Nom          |
|----|--------------|
| 1  | Électronique |
| 2  | Vêtements    |
| 3  | Livres       |

#### Table : `produits`
| ID | Nom        | Prix  | categorie_id |
|----|------------|-------|--------------|
| 1  | Smartphone | 599.99| 1            |
| 2  | T-shirt    | 19.99 | 2            |
| 3  | Roman      | 14.99 | 3            |

#### Table : `clients`
| ID | Nom    | Prénom | Email                  | date_inscription |
|----|--------|--------|------------------------|-------------------|
| 1  | Dupont | Alice  | alice.dupont@example.com| 2023-01-01        |
| 2  | Martin | Bob    | bob.martin@example.com  | 2023-02-01        |

#### Table : `commandes`
| ID | client_id | date_commande |
|----|-----------|---------------|
| 1  | 1         | 2023-03-01    |
| 2  | 2         | 2023-03-05    |

#### Table : `details_commandes`
| ID | commande_id | produit_id | quantite |
|----|-------------|------------|----------|
| 1  | 1           | 1          | 1        |
| 2  | 1           | 3          | 2        |
| 3  | 2           | 2          | 3        |


## 3. Requêtes de Sélection
Écrivez des requêtes pour récupérer des informations spécifiques :

- Tous les produits de la catégorie "Électronique".
- Toutes les commandes passées par un client spécifique.
- Tous les produits commandés par un client spécifique.


## 4. Jointures
Écrivez des requêtes utilisant des jointures pour combiner des informations de plusieurs tables :

- Tous les produits avec les noms de leurs catégories.
- Toutes les commandes avec les noms des clients et les détails des produits commandés.


## 5. Mise à Jour et Suppression

Écrivez des requêtes pour mettre à jour et supprimer des enregistrements :

- Mettre à jour le prix d'un produit.
- Supprimer une commande de la base de données.


## 6. Requêtes Avancées
Écrivez des requêtes avancées pour des analyses plus complexes :

- Compter le nombre de produits commandés par chaque client.
- Trouver les produits qui n'ont jamais été commandés.
