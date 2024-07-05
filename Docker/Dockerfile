# DockerFile-StudyCyle
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY target/target/StudyCycle-0.0.1-SNAPSHOT.jar  /app/StudyCycle-0.0.1-SNAPSHOT.jar
EXPOSE 8080
CMD ["java", "-jar", "StudyCycle-0.0.1-SNAPSHOT.jar"]

# DockerFile-Nginx
FROM ubuntu:20.04
RUN apt-get update \
    && apt-get install -y nginx 
COPY index.html /var/www/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

# DockerFile-Httpd
FROM amazonlinux:2
RUN yum update -y && \
    yum install -y httpd 
COPY index.html /var/www/html/index.html
EXPOSE 80
CMD ["httpd", "-D", "FOREGROUND"]

# DockerFile-Tomcat
FROM ubuntu:20.04
RUN apt update -y
RUN apt install  openjdk-11-jdk -y
WORKDIR /opt/tomcat
EXPOSE 8080 
ADD https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.90/bin/apache-tomcat-9.0.90.tar.gz  /opt/tomcat
RUN tar -xzf apache-tomcat-9.0.90.tar.gz -C /opt/tomcat
ADD https://s3-us-west-2.amazonaws.com/studentapi-cit/student.war /opt/tomcat/apache-tomcat-9.0.90/webapps/
CMD ["apache-tomcat-9.0.90/bin/catalina.sh","run"]

#DockerFile-DB
FROM mariadb
WORKDIR /usr/local/bin/
ENV MARIADB_ROOT_PASSWORD=1234
COPY student-rds.sql /docker-entrypoint-initdb.d/
CMD ["mariadbd"]


