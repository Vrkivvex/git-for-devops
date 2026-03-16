# Day 5 – Docker Basics

## What is Docker

Docker is a platform that allows applications to run inside *containers*.

A container packages:

- application code
- dependencies
- libraries
- runtime

This ensures the app runs the same everywhere.

Example problem Docker solves:

Developer machine → Python 3.11  
Server → Python 3.8  

Application breaks.

Docker packages the correct environment.

---

## Important Docker Concepts

Image → blueprint/template  
Container → running instance of image  
Docker Hub → public image registry  
Dockerfile → instructions to build images

Example:

nginx image → nginx container

---

## Docker Installation Check

Check Docker version:

docker --version

---

## Running a Container

Run nginx container:

docker run nginx

Docker will:

1. Check if image exists
2. Pull image from Docker Hub
3. Create container
4. Start container

---

## Running Container in Background

docker run -d nginx

-d means *detached mode* (run in background)

---

## Port Mapping

Example:

docker run -d -p 8080:80 nginx

Meaning:

8080 → host port  
80 → container port

Access service via:

http://localhost:8080

---

## List Containers

Running containers:

docker ps

All containers:

docker ps -a

---

## Stop Container

docker stop container_id

---

## Remove Container

docker rm container_id

---

## Docker Images

List images:

docker images

Remove image:

docker rmi image_name

---

## Enter a Container

docker exec -it container_name bash

This opens a shell inside the container.

---

## Docker Volumes

Volumes store persistent data outside containers.

Create volume:

docker volume create myvolume

List volumes:

docker volume ls

Attach volume to container:

docker run -v myvolume:/data nginx

Volumes keep data even if container is deleted.

---

## Docker Compose

Docker Compose manages multiple containers.

Example docker-compose.yml

version: "3"

services:
  web:
    image: nginx
    ports:
      - "8080:80"

Start services:

docker-compose up -d

Stop services:

docker-compose down