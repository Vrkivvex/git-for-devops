# Day 14 – Docker on EC2 (Real Deployment)

## Overview

In this lab, we deployed a Docker container on a cloud server (AWS EC2) and exposed it to the internet.

This simulates real-world application deployment.

---

## Architecture

User (browser)
↓
Public IP
↓
Port 80
↓
EC2 server (Ubuntu)
↓
Docker Engine
↓
nginx container
↓
Web page response

---

## Step 1 – Launch EC2

Configuration:

- OS: Ubuntu
- Instance type: t2.micro (free tier)
- Storage: 8GB
- Public IP: Enabled

Security group:

- Port 22 → SSH access
- Port 80 → HTTP (web access)

---

## Step 2 – Connect via SSH

Command:

chmod 400 my-key.pem

ssh -i my-key.pem ubuntu@PUBLIC_IP

Explanation:

- SSH is used to remotely access the server
- Key pair ensures secure authentication

---

## Step 3 – Install Docker

Update system:

sudo apt update

Install Docker:

sudo apt install docker.io -y

Start Docker:

sudo systemctl start docker

Check status:

systemctl status docker

---

## Step 4 – Run Container

Command:

sudo docker run -d -p 80:80 nginx

---

## Breakdown of Command

docker run → create and start container  
-d → run in background  
-p 80:80 → map host port to container port  
nginx → image name  

---

## Port Mapping Concept

Format:

HOST_PORT : CONTAINER_PORT

Example:

80:80 → access without specifying port  
5000:80 → access using :5000  

---

## Step 5 – Access Application

Open in browser:

http://PUBLIC_IP

Reason:

- HTTP uses port 80 by default
- No need to specify port manually

---

## Networking Flow

Browser → Public IP:80 → EC2 → Docker → Container → nginx → Response

---

## Debugging Approach

If website does not open:

1. Check container:
   docker ps

2. Check port:
   ss -tuln

3. Test locally:
   curl localhost:80

4. Check security group:
   Port 80 allowed?

---

## Key Concepts

### Container vs Host

EC2 (host machine) is separate from Docker container.

Host runs Docker  
Docker runs container  
Container runs application  

---

### Default Ports

HTTP → 80  
HTTPS → 443  
SSH → 22  

---

## Real DevOps Use Case

- Deploy web applications quickly
- Run services in isolated environments
- Scale applications using containers
- Avoid manual installation

---

## Cleanup (CRITICAL)

To avoid charges:

1. Stop instance
2. Terminate instance
3. Verify no running resources

---

## Cost Awareness

Free:

- Key pair
- Security group

Paid:

- Running EC2 instance
- Additional storage

---

## Key Learning

- Cloud server + Docker = real deployment
- Port mapping controls accessibility
- Security groups act as firewall
- Always terminate resources after use