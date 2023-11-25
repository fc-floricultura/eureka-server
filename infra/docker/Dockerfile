FROM maven:3.9.2 AS builder
WORKDIR /tmp/app

COPY pom.xml .
COPY src src

RUN --mount=type=cache,target=/root/.m2 mvn install -DskipTests

FROM amazoncorretto:8

WORKDIR /workspace
EXPOSE 8761

COPY --from=builder /tmp/app/target/*.jar app.jar

ENTRYPOINT ["java", "-jar", "app.jar"]
