# To-Do List Application

## Introduction

L'objectif de ce projet est de développer une application To-Do List en utilisant des technologies modernes de développement web. L'application permet aux utilisateurs de créer, modifier, supprimer et visualiser des tâches.

**Technologies Utilisées :**
- **Frontend:** React, Material-UI
- **Backend:** Node.js, Express
- **Base de Données:** PostgreSQL
- **Tests:** Jest, Supertest
- **Conteneurisation:** Docker, Docker Compose

## Configuration de l'Environnement

### Prérequis
- Node.js et npm
- Docker et Docker Compose

### Instructions d'Installation

1. Clonez le dépôt :
   ```sh
   git clone https://github.com/votre-utilisateur/todo-app.git
   cd todo-app

    Installez les dépendances pour le backend :

    sh

cd backend
npm install

Installez les dépendances pour le frontend :

sh

    cd ../frontend
    npm install

Configuration des Fichiers

Créez un fichier .env dans le répertoire backend et ajoutez les lignes suivantes :

env

DATABASE_URL=postgres://postgres:password@db:5432/todolist
FRONTEND_URL=http://localhost:3000

Développement de l'Application
Backend

    Configuration d'Express et des Routes :
        Configurez les routes pour gérer les tâches : création, mise à jour, suppression, et récupération des tâches.
        Utilisez winston pour la journalisation et sequelize pour l'interaction avec PostgreSQL.

Frontend

    Configuration de React et des Composants :
        Utilisez Material-UI pour une interface utilisateur esthétique et professionnelle.
        Créez des composants réutilisables pour afficher et gérer les tâches.


Instructions pour Exécuter les Tests

    Exécutez les tests pour le backend :

    sh

cd backend
npm test

Exécutez les tests pour le frontend :

sh

    cd frontend
    npm test

Déploiement
Utilisation de Docker et Docker Compose

    Build et Lancement des Conteneurs :
        Utilisez Docker Compose pour créer et lancer les conteneurs.
        Assurez-vous que tous les services (base de données, backend, frontend) sont correctement configurés et communiquent entre eux.

    Commandes pour Docker Compose :

    sh

    docker-compose up --build

Documentation et Rapport

    Documenter le Code :
        Utilisez des commentaires clairs et détaillés dans le code pour expliquer les fonctionnalités et les décisions de conception.
    Rédaction du Rapport :
        Incluez une introduction, les technologies utilisées, les étapes de développement, les tests effectués, et les instructions de déploiement.
        Expliquez les défis rencontrés et comment ils ont été surmontés.

