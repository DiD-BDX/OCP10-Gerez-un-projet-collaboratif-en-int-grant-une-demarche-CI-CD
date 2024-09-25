# Utiliser une image de base Maven avec JDK 11 pour la construction
FROM maven:3.6.3-jdk-11-slim AS build

# Créer un répertoire de travail dans le conteneur
RUN mkdir -p /workspace

# Définir le répertoire de travail dans le conteneur
WORKDIR /workspace

# Copier le fichier pom.xml dans le répertoire de travail
COPY pom.xml /workspace

# Copier le répertoire src dans le répertoire de travail
COPY src /workspace/src

# Exécuter la commande Maven pour nettoyer et empaqueter le projet, en sautant les tests
RUN mvn -B -f pom.xml clean package -DskipTests

# Utiliser une image de base OpenJDK 11 pour exécuter l'application
FROM openjdk:11-jdk-slim

# Copier le fichier JAR construit depuis l'étape de build vers le répertoire de travail
COPY --from=build /workspace/target/*.jar app.jar

# Exposer le port 8080 pour accéder à l'application
EXPOSE 8080

# Définir le point d'entrée pour exécuter l'application Java
ENTRYPOINT ["java", "-jar", "app.jar"]