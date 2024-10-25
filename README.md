# RESTAPI

## Documentation de l’API Restaurant

### Introduction

Ce projet consiste en une API REST conçue pour gérer des éléments, des catégories et des formules dans un restaurant. Développée avec Node.js, Express et MySQL, cette API intègre un contrôle d’accès basé sur les rôles et utilise une authentification basique pour certaines opérations. Elle permet également de filtrer les requêtes GET et d’effectuer des opérations CRUD (Création, Lecture, Mise à jour, Suppression), dont certaines sont réservées aux administrateurs.

### Prérequis

1. **Docker** : on l'utilise pour gérer la base de données MySQL et phpMyAdmin.  On utilise également Docker. [Télécharger Docker](https://www.docker.com/products/docker-desktop)
2. **Node.js** : L'API est construite avec Node.js. [Installer Node.js](https://nodejs.org/en)
3. **Postman** : on l'utilise pour tester les routes de l'API. On télécharge Postman afin de pouvoir tester les routes configurées.

### Installation et Configuration

#### Étape 1 : Installer les dépendances Node.js

Pour démarrer, on installe les dépendances nécessaires grâce aux commandes suivantes : 

```bash
npm init -y
 
npm install express
 
npm install mysql2
```

#### Étape 2 : Configuration de MySQL et phpMyAdmin avec Docker

On utilise Docker pour effectuer la configuration de MySQL et phMyAdmin

  1. on télécharge le fichier `docker-compose.yml` dans le répertoire racine du projet.
  2. on lance Docker pour configurer MySQL et phpMyAdmin :

```bash
docker-compose up -d
```

  3. on accède à phpMyAdmin via [http://localhost:6060](http://localhost:6060) et on se connecte avec les identifiants suivants :
    - **Nom d'utilisateur** : `root`
    - **Mot de passe** : `teo`

  La base de données `restaurantapi` sera déjà créée et on pourra y gérer les tables et données via phpMyAdmin.

#### Étape 3 : Démarrer le Serveur API

Une fois la base de données opérationnelle, on démarre le serveur API avec :

```bash
node index.js
```

L'API sera disponible à l'adresse [http://localhost:3000](http://localhost:3000).

### Authentification

L'API utilise une authentification basique pour protéger certaines routes, en particulier celles réservées aux administrateurs. Deux comptes utilisateurs sont configurés :

- **Admin** :
  - Nom d'utilisateur : `admin`
  - Mot de passe : `admin1234`
  - Rôle : `admin`
  
- **Client** :
  - Nom d'utilisateur : `client`
  - Mot de passe : `client1234`
  - Rôle : `client`

Ces identifiants sont utilisés pour accéder aux routes protégées.

### Endpoints de l'API

#### Items

- `GET /items` : Récupérer tous les items.
- `GET /items/:id` : Récupérer un item par son ID.
- `POST /items` : Ajouter un nouvel item (réservé aux administrateurs).
- `PUT /items/:id` : Mettre à jour un item par son ID (réservé aux administrateurs).
- `DELETE /items/:id` : Supprimer un item par son ID (réservé aux administrateurs).

#### Catégories

- `GET /categories` : Récupérer toutes les catégories.
- `GET /categories/:id` : Récupérer une catégorie par son ID.
- `POST /categories` : Ajouter une nouvelle catégorie (réservé aux administrateurs).
- `PUT /categories/:id` : Mettre à jour une catégorie par son ID (réservé aux administrateurs).
- `DELETE /categories/:id` : Supprimer une catégorie par son ID (réservé aux administrateurs).

#### Formules

- `GET /formulas` : Récupérer toutes les formules (filtrage par nom, prix, et catégorie disponible).
- `GET /formulas/:id` : Récupérer une formule par son ID.
- `POST /formulas` : Ajouter une nouvelle formule (réservé aux admins).
- `PUT /formulas/:id` : Mettre à jour une formule par son ID (réservé aux admins).
- `DELETE /formulas/:id` : Supprimer une formule par son ID (réservé aux admins).

#### Filtrage 
- `GET /item?parameters=` : Filtrer les items en fonction du paramètre (nom, prix et catégorie).
- `GET /formulas?parameters=` : Filtrer les formules en fonction du paramètre (nom, prix et catégorie)

### Tester l'API avec Postman

Pour tester l'API dans Postman :

1. on ajoute l'URL de base `http://localhost:3000` dans les requêtes.
2. Pour les routes protégées par rôle administrateur, on suit ces étapes :
  - on va dans l'onglet **Authorization**.
  - on sélectionne **Basic Auth**.
  - on entre les identifiants du rôle qu'on souhaite utiliser (par exemple, `admin` ou `client`).
