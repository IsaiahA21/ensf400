# Use an official OpenJDK runtime as a parent image
FROM openjdk:11-jdk-slim

#Set working directory
WORKDIR /app



# Copy just the gradle wrapper files first for better layer caching
COPY gradle gradle
COPY gradlew gradlew
COPY build.gradle build.gradle
COPY gradle.properties gradle.properties

# Make Gradle wrapper executable
RUN chmod +x gradlew

#Copy the current directory content into the container at /app
COPY . .


# Build the project
RUN ./gradlew build

EXPOSE 8080
# Run the application
CMD ["./gradlew", "appRun"]