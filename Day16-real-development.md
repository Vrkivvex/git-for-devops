# Day 16 – Real Deployment (GitHub Project → Docker → EC2)

## Overview

In this lab, we deployed a real-world website project from GitHub onto an AWS EC2 server using Docker and nginx.

This represents an actual DevOps deployment workflow used in production.

---

## Architecture

Developer
↓
GitHub (project repository)
↓
EC2 server (Ubuntu)
↓
Docker Engine
↓
nginx container
↓
User (browser via Public IP)

---

## Step 1 – Launch EC2

Configuration:

- OS: Ubuntu
- Instance: t2.micro (free tier)
- Storage: 8GB
- Public IP: Enabled

Security Group:

- Port 22 → SSH
- Port 80 → HTTP

---

## Step 2 – Connect to Server

chmod 400 my-key.pem

ssh -i my-key.pem ubuntu@PUBLIC_IP

Purpose:

- Secure remote access using SSH
- Key-based authentication

---

## Step 3 – Install Tools

sudo apt update
sudo apt install git docker.io -y
sudo systemctl start docker

Verify:

systemctl status docker

---

## Step 4 – Clone Real Project

git clone https://github.com/StartBootstrap/startbootstrap-creative.git

cd startbootstrap-creative

---

## Step 5 – Understand Project Structure

Important:

- nginx serves files from root directory
- project may have subfolder (e.g., dist/) containing index.html

Find index file:

find . -name "index.html"

Navigate to correct folder:

cd dist

---

## Step 6 – Run Docker Container

Stop and remove old containers:

sudo docker rm -f $(sudo docker ps -aq)

Run container:

sudo docker run -d -p 80:80 \
-v $(pwd):/usr/share/nginx/html \
nginx

---

## Key Concept – Volume Mounting

-v $(pwd):/usr/share/nginx/html

Explanation:

- $(pwd) → current project folder
- /usr/share/nginx/html → nginx web root
- This connects project files to container

---

## Networking Flow

Browser → Public IP → Port 80 → EC2 → Docker → nginx → HTML files → Response

---

## Debugging Issues

### 1. 403 Forbidden

Cause:
- index.html not found in root folder

Fix:
- Navigate to correct folder (e.g., dist/)

---

### 2. Port already allocated

Cause:
- Another container or service using port 80

Fix:
sudo docker rm -f $(sudo docker ps -aq)

---

### 3. Container not working

Check:

docker ps  
docker logs <container_id>  
ss -tuln  

---

## Important Concepts

### GitHub

- Stores project code
- Source of truth
- Used for deployment

---

### EC2

- Cloud server
- Runs application

---

### Docker

- Runs containerized applications
- Ensures consistent environment

---

### nginx

- Web server
- Serves static files

---

## Real DevOps Workflow

1. Developer pushes code to GitHub
2. Server pulls latest code
3. Docker runs application
4. Application exposed via port
5. Users access via browser

---

## Cleanup (CRITICAL)

To avoid charges:

1. Stop instance
2. Terminate instance
3. Verify no running resources

---

## Key Learning

- Real deployment requires connecting code to container
- File structure matters (index.html location)
- Only one service can use a port at a time
- Debugging is core DevOps skill
- Docker + EC2 = production-level deployment