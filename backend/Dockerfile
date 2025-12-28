# Stage 1 — Build the Spring Boot app
FROM maven:3.9.2-eclipse-temurin-17 AS build

# Set working directory inside container
WORKDIR /app

# Copy only pom.xml & download deps (cache optimization)
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Copy source and build
COPY src ./src
RUN mvn clean package -DskipTests

# Stage 2 — Run the app
FROM eclipse-temurin:17-jre

WORKDIR /app

# Copy built jar from build stage
COPY --from=build /app/target/*.jar app.jar

# Expose Spring Boot default port
EXPOSE 8080

# Default command to run the application
ENTRYPOINT ["java","-jar","app.jar"]
