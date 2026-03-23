# E-Commerce Microservices Project

Ce projet est une plateforme e-commerce basée sur une architecture microservices (Node.js, Vue.js, MongoDB) entièrement conteneurisée avec Docker.

## Prérequis : Cloner le projet
```bash
git clone git@github.com:MathurinChrist/ecommerce.git
cd ecommerce
```

## Installation Locale (Développement)

### Option A : Via Docker Compose 
Cette méthode est la plus simple car elle lance automatiquement les microservices, les bases de données et le frontend en une seule commande.
```bash
docker compose up --build
```
*L'application sera accessible sur [http://localhost:8080](http://localhost:8080).*

### Initialisation des Données
Une fois l'application lancée, remplissez votre catalogue avec :
```bash
chmod +x ./scripts/init-products.sh
./scripts/init-products.sh

## Environnement de Production (Docker Swarm)

Pour un déploiement robuste en production, nous utilisons Docker Swarm et le fichier `docker-compose.prod.yml`.

### Prérequis :
- Docker installé sur le serveur.
- Accès SSH au serveur.

### 1. Initialiser Docker Swarm
```bash
docker swarm init
```

### 2. Créer le secret JWT (Sécurité)
```bash
echo "votre_secret_jwt" | docker secret create jwt_secret -
```

### 3. Déployer la Stack en Production
```bash
docker stack deploy -c docker-compose.prod.yml e-commerce
```

### 4. Vérifier le Déploiement
```bash
docker stack services e-commerce
```
