# TP3

## Consignes
1. Écrivez un script pour :
    1. Créer une base de données nommée teams
    2. Cette base contient une table games avec les colonnes match_date, victory, observations avec les types adaptées
    3. Cette base contient une table players avec les colonnes firstname, lastname, start_date avec les types adaptées
    4. Donner tous les droits sur la table games à un nouvel utilisateur manager avec le mot de passe manager_password
    5. Donner les droits d'écriture et de lecture sur la table players à un nouvel utilisateur recruiter avec le mot de passe recruiter_password
    6. Valider ces privilèges
2. Exécutez ce script pour l'utilisateur adéquat
3. Écrivez un script pour ajouter au moins trois lignes dans la table games et exécutez le pour l'utilisateur adéquat

## Script SQL
+ Écrivez un script pour :
    1. création database `teams`
    ```sql
    CREATE DATABASE IF NOT EXISTS teams;
    USE teams;
    ```

    2. Création table games
    ```sql
    CREATE TABLE IF NOT EXISTS games(
        victory INTEGER,
        observations TEXT,
        match_date DATE
    );
    ```

    3. Création table players
    ```sql
    DROP TABLE IF EXISTS players;
    CREATE TABLE players(
        firstname INTEGER,
        lastname TEXT,
        start_date DATE
    );
    ```

    4. Donner tous les droits sur la table games à un nouvel utilisateur manager avec le mot de passe manager_password
    ```sql
    CREATE USER IF NOT EXISTS 'manager'@'localhost' IDENTIFIED BY 'manager_password';
    GRANT ALL ON teams.games TO 'manager'@'localhost';
    ```

    5. Donner les droits d'écriture et de lecture sur la table players à un nouvel utilisateur recruiter avec le mot de passe recruiter_password
    ```sql
    CREATE USER IF NOT EXISTS 'recruiter'@'localhost' IDENTIFIED BY 'recruiter_password';
    GRANT INSERT, SELECT ON teams.players TO 'recruiter'@'localhost';
    ```

    6. Valider ces privilèges
    ```sql
    FLUSH PRIVILEGES;
    ```
+ Exécutez ce script pour l'utilisateur adéquat
```sql
mysql -u root -p < script1.sql
```

+ Écrivez un script pour ajouter au moins trois lignes dans la table games et exécutez le pour l'utilisateur adéquat
```sql
INSERT INTO games (victory, observations, match_date) VALUES (10, "First", "2010-08-01");
INSERT INTO games (victory, observations, match_date) VALUES (11, "Second", "2010-09-01");
INSERT INTO games (victory, observations, match_date) VALUES (12, "Third", "2010-10-01");
```
```sql
mysql -u manager -p < script2.sql
```