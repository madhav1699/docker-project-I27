#multistage Dockerfile

#Build the application with maven
FROM maven:3.9-eclipse-temurin-17 as builder
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

#Run the application with java process
FROM eclipse-temurin:17-alpine
WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar
EXPOSE 8082
ENTRYPOINT ["sh", "-c", "java -jar app.jar"]
