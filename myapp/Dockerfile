FROM maven:3.8.5-eclipse-temurin-17 AS builder

WORKDIR /app

COPY pom.xml .
RUN mvn dependency:go-offline -B

COPY src ./src

RUN mvn clean package -DskipTests

FROM eclipse-temurin:17-jre-jammy As runtime

RUN useradd -m -u 1000 appuser

WORKDIR /app

COPY --from=builder /app/target/*.jar /app/app.jar

RUN chown -R appuser:appuser /app

USER appuser

EXPOSE 8989

ENTRYPOINT ["java", "-jar", "/app/app.jar"]
