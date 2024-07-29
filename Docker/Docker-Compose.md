## What is Docker Compose?
**Docker Compose is a tool that allows you to define and manage multi-container Docker applications. 
   It uses a YAML file to configure the application’s services, networks, and volumes, 
   making it easier to deploy and manage applications with multiple interconnected services.**

## Why is Docker Compose Important?
***Simplified Configuration:*** 
- Docker Compose provides a straightforward way to define and configure multiple services in a single file. 
- This reduces the complexity of managing individual Docker commands for each container.

***Multi-Container Applications:*** 
- Many applications consist of multiple components (e.g., a web server, database, and caching server).
- Docker Compose allows you to define and run these components together, ensuring they are properly connected and configured.

***Portability:*** 
-  The Docker Compose file (docker-compose.yml) can be shared with others,
-  making it easy to reproduce the same environment across different machines and development setups.

****Orchestration:*** 
- Docker Compose handles the orchestration of starting, stopping, and managing the lifecycle of containers,
- ensuring that they start in the correct order based on dependencies.

***Isolation:*** 
- Each service defined in Docker Compose runs in its own isolated container, ensuring that dependencies and
- configurations do not conflict with other services or applications on the host system.


**Installation**
````
sudo curl -L "https://github.com/docker/compose/releases/download/v2.21.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
````
````
sudo chmod +x /usr/local/bin/docker-compose
````
````
docker-compose --version
````
**Example**



```yaml
version: '3.8'

services:
  springboot-app:
    image: openjdk:17-jdk-slim
    container_name: springboot-app
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "8080:8080"
    depends_on:
      - mysql-db
    environment:
      SPRING_DATASOURCE_URL: jdbc:mysql://mysql-db:3306/mydatabase
      SPRING_DATASOURCE_USERNAME: exampleuser
      SPRING_DATASOURCE_PASSWORD: examplepass

  mysql-db:
    image: mysql:8.0
    container_name: mysql-db
    environment:
      MYSQL_ROOT_PASSWORD: example
      MYSQL_DATABASE: mydatabase
      MYSQL_USER: exampleuser
      MYSQL_PASSWORD: examplepass
    ports:
      - "3306:3306"
    volumes:
      - mysql_data:/var/lib/mysql

volumes:
  mysql_data:
```
