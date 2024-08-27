# Stage 1: Build
FROM openjdk:11 AS BUILD_IMAGE

# Install Maven
RUN apt update && apt install maven -y

# Clone the repository and build the project
RUN git clone https://github.com/Pomanekgatla/vprofile-project.git \
    && cd vprofile-project \
    && git checkout docker \
    && mvn install

# Stage 2: Create the final image
FROM tomcat:9-jre11

# Remove the default web apps
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy the WAR file from the build stage to Tomcat's webapps directory
COPY --from=BUILD_IMAGE /vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

# Expose port 8080
EXPOSE 8080

# Start Tomcat
CMD ["catalina.sh", "run"]