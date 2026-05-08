# multistage Dockerfile for building and running tomcat application
# mulitistage builds allow us to separate the build environment from the runtime environment, which can help reduce the size of the final image and improve security by only including the necessary runtime dependencies in the final image.

FROM maven:3.9.9-eclipse-temurin-11 AS build_image

WORKDIR /app
COPY . .    
RUN mvn install -DskipTests

# in the second stage, we use the tomcat image to run the application
FROM tomcat:10-jdk21

LABEL "Project"="Vprofile"
LABEL "Author"="Tina"

# remove the default tomcat webapps to avoid conflicts with our application
RUN rm -rf /usr/local/tomcat/webapps/*

# copy the built war file from the first stage to the tomcat webapps default directory
# we just want the war file, so we specify the path to the war file in the build stage and copy it to the webapps directory in the runtime stage
COPY --from=build_image /app/target/*.war /usr/local/tomcat/webapps/ROOT.war

# expose the application on port 8080 and start the tomcat server
EXPOSE 8080
CMD ["catalina.sh", "run"]