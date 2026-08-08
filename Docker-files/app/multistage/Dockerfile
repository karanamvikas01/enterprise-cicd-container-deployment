# Stage 1 - Build the application
FROM maven:3.9.6-eclipse-temurin-21 AS BUILD_IMAGE

RUN git clone https://github.com/devopshydclub/vprofile-project.git

RUN mv /vprofile-project /usr/local/src/maven

WORKDIR /usr/local/src/maven

RUN mvn install -DskipTests

# Stage 2 - Runtime Image
FROM tomcat:9-jdk21-temurin

RUN rm -rf /usr/local/tomcat/webapps/*

COPY --from=BUILD_IMAGE \
/usr/local/src/maven/target/vprofile-v2.war \
/usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080

CMD ["catalina.sh", "run"]