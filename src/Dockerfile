FROM maven:3.8-amazoncorretto-17 AS build
WORKDIR /workspace/app
COPY pom.xml .
COPY src ./src/
RUN \
    --mount=type=cache,target=/root/.m2 \
    --mount=type=secret,id=maven_settings,target=/root/.m2/settings.xml \
    mvn clean package -DskipTests

FROM amazoncorretto:17
COPY --from=build /workspace/app/target/*.jar /app/app.jar
ENTRYPOINT ["java", "-jar", "/app/app.jar"]