# Day 7 – Docker Compose Networking

## Multi-container Setup

Docker Compose can run multiple containers.

Example:

- nginx (web)
- redis (database)

## docker-compose.yml

version: "3"

services:
  web:
    image: nginx
    ports:
      - "8080:80"

  redis:
    image: redis

## Key Concept

Containers can communicate using service names.

Example:

ping redis

## Networking

Docker Compose automatically creates a network.

All services can talk to each other.