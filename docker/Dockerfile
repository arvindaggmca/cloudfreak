# Use Fedora as the base image
FROM registry.fedoraproject.org/fedora:34

# Install OpenJDK 11
RUN dnf install -y java-11-openjdk

# Create a directory for the application
WORKDIR /app

# Add the application's jar to the container
COPY *.jar app.jar

# Specify the entry point for the container
ENTRYPOINT ["java", "-jar", "app.jar"]
