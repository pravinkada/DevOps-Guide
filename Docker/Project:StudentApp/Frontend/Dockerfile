FROM centos:7
LABEL APP="StudentAppF"
LABEL User="Abhi"


RUN yum install httpd -y
COPY index.html /var/www/html/index.html

EXPOSE 80
CMD ["httpd", "-D", "FOREGROUND"]
