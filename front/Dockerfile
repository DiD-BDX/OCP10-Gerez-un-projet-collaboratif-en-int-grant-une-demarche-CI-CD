# Dockerfile for Frontend
FROM node:16-alpine AS build
WORKDIR /app

# Copie uniquement les fichiers nécessaires pour npm install
COPY package.json package-lock.json ./
RUN npm install

# Copie uniquement les fichiers nécessaires pour la construction
COPY src ./src
COPY angular.json ./
COPY tsconfig.json ./
COPY tsconfig.app.json ./

RUN npm run build

FROM nginx:alpine
COPY --from=build /app/dist/bobapp /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]