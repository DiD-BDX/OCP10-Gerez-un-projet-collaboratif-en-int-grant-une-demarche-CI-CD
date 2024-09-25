# Dockerfile for Frontend

# Étape 1 : Utiliser une image de base Node.js pour la construction
FROM node:16-alpine AS build

# Définir le répertoire de travail dans le conteneur
WORKDIR /app

# Copier les fichiers package.json et package-lock.json dans le conteneur
COPY package.json package-lock.json ./

# Installer les dépendances du projet sans exécuter les scripts définis dans les paquets
RUN npm install --ignore-scripts

# Copier les fichiers sources et les fichiers de configuration Angular dans le conteneur
COPY src ./src
COPY angular.json ./
COPY tsconfig.json ./
COPY tsconfig.app.json ./

# Construire l'application Angular
RUN npm run build

# Étape 2 : Utiliser une image de base Nginx pour servir l'application
FROM nginx:alpine

# Copier les fichiers construits depuis l'étape de build vers le répertoire de Nginx
COPY --from=build /app/dist/bobapp /usr/share/nginx/html

# Exposer le port 80 pour accéder à l'application
EXPOSE 80

# Démarrer Nginx en mode non-démon
CMD ["nginx", "-g", "daemon off;"]