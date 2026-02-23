# ===== Etapa 1: Build con Maven + JDK 8 =====
FROM maven:3.8.7-eclipse-temurin-8 AS build

WORKDIR /app

# Copiamos pom y fuentes
COPY pom.xml .
COPY src ./src

# Compilar JAR (packaging Spring Boot)
RUN mvn clean package -DskipTests

# ===== Etapa 2: Runtime con JRE 8 =====
FROM eclipse-temurin:8-jre

WORKDIR /app

# Copiamos el JAR generado desde la etapa de build
COPY --from=build /app/target/*.jar app.jar

# Puerto de tu app (según application.properties)
EXPOSE 8888

# Volúmenes para Derby y logs (ajusta rutas si hace falta)
VOLUME ["/app/work", "/app/work/logs"]

ENTRYPOINT ["java", "-jar", "app.jar"]
