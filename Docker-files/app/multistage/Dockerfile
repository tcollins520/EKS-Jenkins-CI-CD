FROM maven:3.9.9-eclipse-temurin-21 AS build_image

RUN git clone https://github.com/tcollins520/ECS-JenkinsCI-CD.git

WORKDIR /ECS-JenkinsCI-CD

RUN git checkout jenkins-cicd

RUN mvn clean package -DskipTests

FROM tomcat:10-jdk21

RUN rm -rf /usr/local/tomcat/webapps/*

COPY --from=build_image /ECS-JenkinsCI-CD/target/*.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080

CMD ["catalina.sh", "run"]