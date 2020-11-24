# TP1

## Consignes
1. Créez une table **client** qui doit pouvoir contenir un nom, un prénom, une date de naissance et un code postal
2. Insérez 3 lignes dans cette table
3. Affichez seulement les prénoms et codes postaux

## Script SQL
1. Création de la database et USE celle-ci
```sql
CREATE DATABASE first_database;
USE first_database;
``` 

2. Création de la table `client`  
```sql
CREATE TABLE clients(
    last_name VARCHAR(255),
    first_name VARCHAR(255),
    birthday DATE,
    postal_code VARCHAR(255)
);
```

3. Insertion de 3 données
```sql
INSERT INTO clients (last_name, first_name, birthday, postal_code) VALUES ("Toto", "Tata", "2000-01-01", "33370");
INSERT INTO clients (last_name, first_name, birthday, postal_code) VALUES ("Tutu", "Titi", "2010-10-10", "33100");
INSERT INTO clients (last_name, first_name, birthday, postal_code) VALUES ("Tete", "Toutou", "2020-12-12", "33000");
```

4. Affichage des prénoms et codes postaux  
```sql
SELECT first_name, postal_code FROM clients;
```