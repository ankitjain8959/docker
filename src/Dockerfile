# Use Maven with Amazon Corretto 17 (a distribution of OpenJDK) for building the Java application
FROM maven:3.8-amazoncorretto-17 AS build

# Set the working directory in the container. All subsequent commands will be run from this directory
WORKDIR /workspace/app

# Copy the dependency files and source code from the host machine to the container's working directory
COPY pom.xml .
COPY src ./src/

# Indicates the port(s) on which the container listens for incoming connections. It is primarily used for documentation purposes and does not actually publish the port. To make the port accessible, you need to use the -p or -P flag with docker run.
EXPOSE 8080

# Build the application using Maven
# Use a cache for Maven dependencies to speed up subsequent builds and securely mounts a secret for Maven settings file into the container
RUN \
    --mount=type=cache,target=/root/.m2 \
    --mount=type=secret,id=maven_settings,target=/root/.m2/settings.xml \
    mvn clean package -DskipTests

# Use Amazon Corretto 17 for running the application
FROM amazoncorretto:17

# Specifies the user under which the container will run. By default, containers run as the root user i.e. `USER 0`, but it's recommended to run applications as a non-root user that has limited privileges to enhance security.
USER 1000

# Copy the built JAR file from the build stage to the app directory
COPY --from=build /workspace/app/target/*.jar /app/app.jar

# Specifies the command that always runs when the container starts.
ENTRYPOINT ["java", "-jar", "/app/app.jar"]

# Specifies the default arguments for the ENTRYPOINT commandm if no arguments are provided during docker run.
CMD ["-Dspring.profiles.active=local"]
# So, when running docker run <image_name>, the container executes `java -jar /app/app.jar -Dspring.profiles.active=local`


# Multi-stage builds allow you to define multiple stages in a single Dockerfile, each with its own FROM instruction.
# These stages are used to separate the build process into distinct steps, often for optimizing the final image size or improving security.