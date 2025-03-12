FROM gradle:7.4-jdk11-alpine AS build
COPY --chown=gradle:gradle . /home/gradle/src
WORKDIR /home/gradle/src

# make gradlew executablez in the container
RUN chmod +x ./gradlew

RUN ./gradlew build --no-daemon

# helpful link: https://forums.docker.com/t/solved-copy-files-into-a-tomcat-image/71728/4

FROM tomcat:9.0-jdk11-openjdk-slim

# Remove the default Tomcat applications
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy the WAR file to Tomcat's webapps directory as ROOT.war
COPY --from=build /home/gradle/src/build/libs/*.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080

CMD ["catalina.sh", "run"]