# TP2

## Consignes
1. Créez une base de données nommée events
2. Ajoutez une table public_events contenant les colonnes event_date, event_name, event_age_requirement avec les types appropriés
3. Dupliquez cette table dans une nouvelle table private_events
4. Créez un utilisateur event_manager avec le mot de passe password
5. Donnez toutes les permissions à la base de données events à cet utilisateur
6. Créez un utilisateur event_supervisor et donnez lui les droits pour visualiser le contenu de la table public_events
7. Connectez vous en tant que event_manager et ajoutez plusieurs entrées dans les tables public_event et private_event
8. Connectez vous en tant que event_supervisor et listez le contenu de la table public_events
9. En tant que event_supervisor essayez de lister le contenu de la table private_events (pour cette étape donnez moi la commande ainsi que le message d'erreur que vous recevez en retour)
10. Reconnectez vous en tant qu'utilisateur root et supprimez l'utilisateur event_supervisor

## Script SQL
1. Création de la database et USE sur celle-ci
```sql
CREATE DATABASE events;
USE events;
```

2. Ajout d'une table `public_events`
```sql
CREATE TABLE public_events(
    event_date DATE,
    event_name VARCHAR(255),
    event_age_requirement INTEGER
);
```

3. Dupliquez cette table dans une nouvelle table private_events
```sql
CREATE TABLE private_events LIKE public_events;
```

4. Créez un utilisateur event_manager
```sql
CREATE USER 'event_manager'@'localhost' IDENTIFIED BY 'password';
```

5. Lui donner toutes les permissions
```sql
GRANT ALL PRIVILEGES ON events.* TO 'event_manager'@'localhost' IDENTIFIED BY 'password;
```
6. Créez un utilisateur event_supervisor
```sql
CREATE USER 'event_supervisor'@'localhost' IDENTIFIED BY 'password';
```

5. Lui donner toutes le droit de visualiser le contenu de la table public_events
```sql
GRANT SELECT ON events.public_events TO 'event_supervisor'@'localhost' IDENTIFIED BY 'password;
```

6. Valider les droits
```sql
FLUSH PRIVILEGES
```

7. Connectez vous en tant que event_manager et ajoutez plusieurs entrées dans les tables public_event et private_event
```sql
mysql -u event_manager -p
password #(réponse à un input demandant le password)
```

8. Inserez plusieurs entrées
```sql
INSERT INTO public_events (event_name, event_age_requirement, event_date) VALUES ("First event", 14, "2000-01-01");
INSERT INTO private_events (event_name, event_age_requirement, event_date) VALUES ("Second event", 12, "2012-01-01");
```

9. Connectez vous en tant que event_supervisor et listez le contenu de la table public_events
```sql
mysql -u event_supervisor -p
password #(réponse à un input demandant le password)
```

10. Lire le contenu de la table public_events
```sql
SELECT * FROM public_events;
```
```
+----------------+-----------------------+------------+
| event_date     | event_age_requirement | event_name_ |
+----------------+-----------------------+------------+
| First event |                     14 | 2000-01-01    |
+----------------+-----------------------+------------+
1 row in set (0.00 sec)
```

11. En tant que event_supervisor essayez de lister le contenu de la table private_events (pour cette étape donnez moi la commande ainsi que le message d'erreur que vous recevez en retour)
```sql 
SELECT * FROM private_events; 
ERROR 1142 (42000): SELECT command denied to user 'event_supervisor'@'localhost' for table 'private_events'
```

12. Reconnectez vous en tant qu'utilisateur root et supprimez l'utilisateur event_supervisor
```sql
mysql -u root -p
root #(réponse à un input demandant le password)
```
```sql
DROP USER 'event_supervisor'@'localhost'
```