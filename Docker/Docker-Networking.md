# Docker Networking: 

- **Docker networking allows containers to communicate with each other, with the host system, and with external networks.**
- **Understanding Docker networking is essential for developing and deploying containerized applications effectively.**


1. [Introduction](#introduction)
2. [Types of Docker Networks](#key-types-of-docker-networks)
    - [Bridge Network](#1-bridge-network)
    - [Host Network](#2-host-network)
    - [Overlay Network](#3-overlay-network)
    - [Macvlan Network](#4-macvlan-network)
    - [None Network](#5-none-network)
3. [When to Use Each Network](#when-to-use-each-network)
4. [Conclusion](#conclusion)

## Introduction

Docker networking is a crucial component for connecting and managing containers within a Docker environment. It enables communication between containers, between containers and the host system, and between containers and external networks.

## Key Types of Docker Networks

### 1. Bridge Network

- **Default network type.**
- Connects containers on the same host.
- Suitable for simple applications needing container-to-container communication.

**Example:** Two containers on the same machine can talk to each other.
```sh
docker run -d --network bridge my-image
