DDL (Data Definition Language) sert à définir ou modifier la structure de la base de données (par exemple CREATE, ALTER, DROP). DDL crée et modifie le schéma et est généralement irréversible sans commandes spécifiques [ex: ALTER TABLE].

DML (Data Manipulation Language) sert à manipuler les données stockées dans les tables (par exemple INSERT, UPDATE, DELETE, SELECT). DML agit sur les lignes et peut être annulé/rollback dans les transactions selon le SGBD [ex: UPDATE, DELETE] [ex: DDL crée/modifie des objets, DML change le contenu des objets]


Création:

CREATE TABLE Produit (
id SERIAL PRIMARY KEY,
nom VARCHAR(100) NOT NULL,
prix DECIMAL(10, 2) NOT NULL,
stock INT NOT NULL
);

Insertion (avec id auto-incrémenté si SERIAL используется):

INSERT INTO Produit (nom, prix, stock) VALUES
('Stylo bleu', 1.50, 100),
('Carnet A5', 2.75, 50),
('Trousse cuir', 12.00, 20);

Mise à jour:

UPDATE Produit
SET prix = prix * 1.10
WHERE id = 2;

Suppression:

DELETE FROM Produit
WHERE stock = 0;