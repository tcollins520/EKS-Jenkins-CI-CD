FROM maven:3.9.9-eclipse-temurin-21 AS build_image

RUN git clone -b jenkins-cicd https://github.com/tcollins520/ECS-JenkinsCI-CD.git

WORKDIR /ECS-JenkinsCI-CD/vprofile-project

RUN mvn clean package -DskipTests

FROM tomcat:10-jdk21

RUN rm -rf /usr/local/tomcat/webapps/*

COPY --from=build_image /ECS-JenkinsCI-CD/vprofile-project/target/*.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080

CMD ["catalina.sh", "run"]