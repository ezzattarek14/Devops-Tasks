
FROM maven:3.9.4-eclipse-temurin-17 AS builder

WORKDIR /app

# Copy pom.xml and download dependencies first (caching step)
COPY pom.xml .
RUN mvn dependency:go-offline -B


COPY src ./src
RUN mvn package -DskipTests

FROM eclipse-temurin:17-jdk-jammy

WORKDIR /app

COPY --from=builder /app/target/*.jar app.jar


EXPOSE 8080


ENTRYPOINT ["java", "-jar", "app.jar"]
