# Day 13 – AWS EC2 (Cloud Basics + Deployment)

## What is EC2

Amazon EC2 (Elastic Compute Cloud) is a virtual server in the cloud.

It allows you to create and manage remote machines over the internet.

---

## Local vs Cloud

Local machine:
- Runs on your laptop
- Private access

EC2:
- Runs on AWS cloud
- Accessible via public IP

---

## Key Concepts

### 1. Instance

A virtual machine (server) running in AWS.

Example:
Ubuntu server running on cloud.

---

### 2. Public IP

Used to access the server from internet.

Example:
http://3.x.x.x

---

### 3. Private IP

Used for internal communication inside AWS network.

Example:
172.x.x.x

---

### 4. Key Pair

Used for secure SSH login.

- Private key (.pem) → stored on your laptop
- Public key → stored in AWS

Command:

ssh -i my-key.pem ubuntu@PUBLIC_IP

---

### 5. Security Group

Acts as a firewall.

Controls which ports are open.

Example rules:

Port 22 → SSH access  
Port 80 → HTTP (website)

---

## Launching EC2 (Safe Setup)

- OS: Ubuntu (free tier)
- Instance type: t2.micro / t3.micro
- Storage: 8GB
- Auto-assign public IP: Enabled

Security group:
- Allow SSH (port 22)
- Allow HTTP (port 80) when needed

---

## Connecting to EC2

### Browser method:
EC2 Instance Connect

### SSH method (real usage):

chmod 400 my-key.pem  
ssh -i my-key.pem ubuntu@PUBLIC_IP  

---

## Installing Web Server (nginx)

Update system:

sudo apt update

Install nginx:

sudo apt install nginx -y

Start service:

sudo systemctl start nginx

Check status:

systemctl status nginx

---

## Access Website

Open in browser:

http://PUBLIC_IP

---

## Ports Used

22 → SSH  
80 → HTTP (website)

---

## Networking Flow

User (browser)
↓
Public IP
↓
Port 80
↓
EC2 server
↓
nginx
↓
Web page

---

## Cleanup (VERY IMPORTANT)

To avoid charges:

1. Stop instance:
   Instance state → Stop

2. Terminate instance:
   Instance state → Terminate

3. Verify:
   State = terminated

---

## Cost Awareness

Free:
- Key pair
- Security group

Paid:
- Running EC2 instance
- Extra storage (EBS)

---

## Real DevOps Use Case

- Deploy web apps
- Host backend APIs
- Run Docker containers
- Manage servers remotely using SSH

---

## Key Learning

- EC2 = cloud server
- SSH = remote access
- Security groups = firewall
- Ports = service entry points
- Always terminate resources after use