# Projet IoT 2 - Gestion des Bases de Données

Ce projet fait partie du projet **IoT 2**, qui vise à optimiser la gestion des transports en commun en utilisant des technologies IoT, des bases de données et des systèmes d'authentification sécurisée.

## Contenu du Projet
Le projet comprend plusieurs bases de données essentielles à la gestion du système :

## Architecture
Les bases de données sont hébergées sur Azure. Pour une question de coût, il a été décidé d'héberger toutes les base de données sur le même serveur.

![architecture db](architecture%20bd.png)
### Création des Utilisateurs SQL et NoSQL
#### MySQL
```sh
sudo mysql -u root -p
CREATE USER 'xxxxxxxxxxx'@'%' IDENTIFIED BY 'xxxxxxxxxxxxxxxxxxxx'; 
GRANT ALL PRIVILEGES ON *.* TO 'xxxxxxxxx'@'%' WITH GRANT OPTION; 
FLUSH PRIVILEGES;
```

#### MongoDB
```js
use admin  // Se connecter à la base de données admin
db.createUser({
  user: "xxxxxxxxxx", 
  pwd: "xxxxxxxxxxxxxxxxxx", 
  roles: [{ role: "root", db: "admin" }]
})
```

## Installation et Utilisation
1. Clonez le répertoire :
   ```sh
   git clone https://github.com/gaetus44/db_iot2
   cd db_iot2
   ```
2. Assurez-vous que votre application accède correctement aux bases de données configurées.


### Bases de Données et Schémas

1. **Database Service**
   - Contenu : Gère les services, les clients, les produits,...
   - Schéma : ![Database Service](table%20dbservices.drawio.png)
2. **Database Transactions**
   - Contenu : Gère les commandes clients,...
   - Schéma : ![Database Transactions](table%20db%20transac.png)
3. **Database Bank 1**
   - Contenu : Base de données bancaire de la banque 1.
   - Schéma : ![Database Bank 1](table%20bank%201.png)
4. **Database Bank 2**
   - Contenu : Base de données bancaire de la banque 1.
   - Schéma : ![Database Bank 2](table%20bank%202.png)

### Scripts SQL de Création des Bases de Données
Les scripts de création des bases de données sont disponibles dans le répertoire principal :
- `commande sql db bank 1`
- `commande sql db bank 2`
- `commande sql db service `
- `commande sql db transac`

