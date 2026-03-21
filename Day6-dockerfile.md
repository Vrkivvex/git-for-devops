# Day 6 – Dockerfile

## Dockerfile

Dockerfile is used to create custom images.

Example:

FROM nginx
COPY index.html /usr/share/nginx/html

## Build Image

docker build -t mywebsite .

## Run Container

docker run -d -p 8080:80 mywebsite

## Key Concept

Dockerfile allows packaging applications with custom configuration.