# Docker Networking: 

- **Docker networking is a crucial component for connecting and managing containers within a Docker environment.**
- **It enables communication between containers, between containers and the host system, and between containers and external networks.**


1. [Introduction](#introduction)
2. [Types of Docker Networks](#key-types-of-docker-networks)
    - [Bridge Network](#1-bridge-network)
    - [Host Network](#2-host-network)
    - [Overlay Network](#3-overlay-network)
    - [Macvlan Network](#4-macvlan-network)
    - [None Network](#5-none-network)
3. [When to Use Each Network](#when-to-use-each-network)
4. [Conclusion](#conclusion)





## Types of Docker Networks

### 1. Bridge Network

- **Default network type.**
- Connects containers on the same host.
- Suitable for simple applications needing container-to-container communication.

**Example:** Two containers on the same machine can talk to each other.
```sh
docker run -d --network bridge my-image
```

### 2. Host Network
- **Shares the host's network.**
- No network isolation.
- Ideal for high-performance applications needing low latency.
**Example:** A container uses the host’s network directly.
```sh
docker run -d --network host my-image
```
### 3. Overlay Network
- **Connects containers across multiple hosts.**
- Used in Docker Swarm or Kubernetes setups.
- Good for distributed applications.
**Example:** Services in a cluster communicate with each other.
```sh
docker network create --driver overlay my-overlay-network
```
### 4. Macvlan Network
- **Gives each container a unique MAC address.**
- Containers appear as physical devices on the network.
- Useful for legacy applications needing direct network access.
Example: Containers have their own IP addresses on the local network.
```sh
docker network create -d macvlan --subnet=192.168.1.0/24 --gateway=192.168.1.1 -o parent=eth0 my-macvlan-network
```

### 5. None Network
- **No network access.**
- Completely isolates the container.
- Used for security-sensitive applications.
**Example:** A container runs without any network connection.
```sh
docker run -d --network none my-image
```


