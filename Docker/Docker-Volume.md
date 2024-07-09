## Docker Volumes
**What are Docker Volumes?**
- Docker volumes are a way to persist data generated and used by Docker containers. 
- They allow data to persist beyond the lifetime of a single container instance and enable data sharing between containers.

***Types of Docker Volumes***

**Named Volumes:**
- Managed by Docker, named volumes are easy to use and work well for most use cases.

**Host-mounted Volumes:** 
- Uses a directory from the host filesystem and can be specified with absolute paths on the host.

**Anonymous Volumes:**
- Automatically created and managed by Docker, primarily used for temporary or disposable data.

**Benefits of Using Docker Volumes**
- **Persistence:** Data persists even if containers are stopped or removed.
- **Sharing:** Volumes can be shared among containers.
- **Backup and Restore:** Easier backup and restore operations for container data.
  
### Docker Volume Commands

Create a Named Volume:
```sh
docker volume create my_volume
```
List All Volumes:
```sh
docker volume ls
```

Inspect a Volume:

 
```sh
docker volume inspect my_volume
```
Remove a Volume:
```sh  
docker volume rm my_volume
```
Run a Container with a Volume:
```sh
docker run -d --name my_container -v my_volume:/path/in/container my_image
```
**mount volume**
```sh
docker run -d --mount source=<volume_name>,target=<container_path> <image_name>
```
**Example** 
To run a MySQL database container with a named volume for data persistence:

 ```sh
docker volume create mysql_data
docker run -d --name mysql_db -v mysql_data:/var/lib/mysql mysql:latest
```
