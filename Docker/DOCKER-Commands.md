# Docker Commands Reference

This document provides a quick reference for common Docker commands, organized by function.

---

## 1. Container Management

| Command | Description |
|---------|-------------|
| `docker run [OPTIONS] IMAGE` | Runs a command in a new container. |
| `docker start [OPTIONS] CONTAINER` | Starts one or more stopped containers. |
| `docker stop [OPTIONS] CONTAINER` | Stops one or more running containers. |
| `docker rm [OPTIONS] CONTAINER` | Removes one or more containers. |
| `docker ps` | Lists all running containers. |
| `docker ps -a` | Lists all containers, including stopped ones. |
| `docker exec -it CONTAINER COMMAND` | Runs a command inside a running container. |
| `docker logs [OPTIONS] CONTAINER` | Fetches the logs of a container. |

---

## 2. Image Management

| Command | Description |
|---------|-------------|
| `docker build [OPTIONS] PATH` | Builds an image from a Dockerfile. |
| `docker images` | Lists all local Docker images. |
| `docker pull [OPTIONS] NAME[:TAG]` | Pulls an image or a repository from a registry. |
| `docker rmi [OPTIONS] IMAGE` | Removes one or more images. |
| `docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]` | Creates a tag `TARGET_IMAGE` that refers to `SOURCE_IMAGE`. |

---

## 3. Network Management

| Command | Description |
|---------|-------------|
| `docker network ls` | Lists all Docker networks. |
| `docker network create [OPTIONS] NAME` | Creates a new network. |
| `docker network connect NETWORK CONTAINER` | Connects a container to a network. |
| `docker network disconnect NETWORK CONTAINER` | Disconnects a container from a network. |
| `docker network inspect NETWORK` | Displays detailed information on a network. |

---

## 4. Volume Management

| Command | Description |
|---------|-------------|
| `docker volume ls` | Lists all Docker volumes. |
| `docker volume create [OPTIONS] NAME` | Creates a new volume. |
| `docker volume inspect [OPTIONS] VOLUME` | Displays detailed information on a volume. |
| `docker volume rm [OPTIONS] VOLUME` | Removes one or more volumes. |
| `docker volume prune` | Removes all unused local volumes. |

---

## 5. System Commands

| Command | Description |
|---------|-------------|
| `docker info` | Displays system-wide information. |
| `docker system prune` | Removes unused Docker data (containers, networks, images, volumes). |
| `docker login` | Logs into a Docker registry. |
| `docker logout` | Logs out from a Docker registry. |

---
