FROM tomcat:9
EXPOSE 8080
RUN rm -rf /usr/local/tomcat/webapps/ROOT && \
    mv /usr/local/tomcat/webapps.dist/ROOT /usr/local/tomcat/webapps
ADD https://s3-us-west-2.amazonaws.com/studentapi-cit/student.war /usr/local/tomcat/webapps
ADD https://s3-us-west-2.amazonaws.com/studentapi-cit/mysql-connector.jar /usr/local/tomcat/lib
COPY context.xml /usr/local/tomcat/conf/context.xml
CMD ["catalina.sh", "run"]
