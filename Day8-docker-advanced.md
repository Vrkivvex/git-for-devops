# Day 8 – Docker Advanced

## Environment Variables

docker run -e MY_NAME=value image

docker-compose:

environment:
  - KEY=value

## Restart Policy

restart: always

Containers restart automatically if they stop.

## Logs

View logs:

docker logs container_name

Follow logs:

docker logs -f container_name

Logs help debug applications.