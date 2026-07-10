# Build stage - Upgrade to Java 17
FROM maven:3.9.6-eclipse-temurin-17-alpine AS build

WORKDIR /app

COPY pom.xml .
COPY src ./src

# The handshake error should resolve with the updated CA certificates in this image
RUN mvn -q -DskipTests package

# Runtime stage - Upgrade to Java 17
FROM eclipse-temurin:17-jre-alpine

WORKDIR /app

COPY --from=build /app/target/aegira-loan-service-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]