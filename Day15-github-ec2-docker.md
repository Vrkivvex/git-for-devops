# Day 15 – GitHub → EC2 → Docker (Deployment Flow)

## Overview

This lab demonstrates how code flows from GitHub to a cloud server (EC2) and is then deployed using Docker.

This represents a basic real-world DevOps workflow.

---

## Architecture

Developer
↓
GitHub (code repository)
↓
EC2 server (Ubuntu)
↓
Docker Engine
↓
Container (nginx / app)
↓
Public IP → User (browser)

---

## Step 1 – Launch EC2

Configuration:

- Ubuntu (free tier)
- t2.micro instance
- 8GB storage
- Public IP enabled

Security group:

- Port 22 → SSH
- Port 80 → HTTP

---

## Step 2 – Connect via SSH

chmod 400 my-key.pem

ssh -i my-key.pem ubuntu@PUBLIC_IP

Explanation:

- SSH allows remote access to the server
- Key pair ensures secure login

---

## Step 3 – Install Git

sudo apt update  
sudo apt install git -y  

Verify:

git --version  

Purpose:

- Allows server to pull code from GitHub

---

## Step 4 – Clone Repository

git clone REPO_URL  
cd REPO_NAME  

Explanation:

- Copies code from GitHub to EC2 server
- This is the deployment source

---

## Step 5 – Install Docker

sudo apt install docker.io -y  
sudo systemctl start docker  

Verify:

systemctl status docker  

---

## Step 6 – Run Container

sudo docker run -d -p 80:80 nginx  

---

## Important Concept

Cloning a repository does NOT deploy it.

The container must use the repository content.

---

## Why nginx showed default page

Because:

- nginx container serves its own default files
- repo files are not connected to container

---

## Connecting Repo to Container

Command:

sudo docker run -d -p 80:80 \
-v $(pwd):/usr/share/nginx/html \
nginx

Explanation:

- $(pwd) → current repo folder
- Mounted into nginx container
- nginx now serves repo content

---

## Port Mapping

Format:

HOST_PORT : CONTAINER_PORT

Example:

80:80 → default HTTP  
5000:80 → custom port  

---

## Networking Flow

Browser → Public IP → EC2 → Docker → Container → nginx → Response

---

## Debugging Workflow

1. Check repo:
   ls

2. Check container:
   docker ps

3. Check logs:
   docker logs container_id

4. Check ports:
   ss -tuln

5. Check security group:
   Port 80 allowed?

---

## Real DevOps Workflow

1. Developer pushes code to GitHub
2. Server pulls code (git clone / git pull)
3. Docker builds/runs application
4. Application exposed to users

---

## Key Concepts

GitHub → code storage  
EC2 → server  
Docker → runtime  
nginx → web server  

---

## Cleanup (CRITICAL)

1. Stop instance
2. Terminate instance
3. Verify no running resources

---

## Key Learning

- GitHub is source of truth
- EC2 runs the application
- Docker runs the container
- Repo must be connected to container to deploy app