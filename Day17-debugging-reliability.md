# Day 17 – Debugging & Reliability in Docker (Production Thinking)

## Overview

In this lab, we focused on handling failures, debugging issues, and making applications reliable using Docker.

This represents real-world DevOps responsibilities.

---

## Architecture

User → Public IP → EC2 → Docker → Container → Application

---

## Scenario 1 – Container Not Running

### Problem

Website is not opening.

### Debug Steps

1. Check running containers:

docker ps

2. If no container is running:

Root cause:
- Application container stopped

---

### Fix

Restart container:

docker start <container_id>

OR run new container:

docker run -d -p 80:80 nginx

---

### Learning

- First step in debugging: check container status
- No container = no application

---

## Scenario 2 – Wrong Port Mapping

### Problem

Application running but not accessible

### Cause

Container started on wrong port

Example:

docker run -d -p 5000:80 nginx

---

### Fix

Access using correct port:

http://PUBLIC_IP:5000

---

### Learning

- Port mapping is critical
- Default HTTP port is 80

---

## Scenario 3 – Logs (Core Debugging Tool)

### Commands

View logs:

docker logs <container_id>

Live logs:

docker logs -f <container_id>

---

### Purpose

- Identify application errors
- Understand why container failed

---

### Learning

Logs are the first place to check when debugging issues.

---

## Scenario 4 – Restart Policies

### Command

docker run -d --restart always -p 80:80 nginx

---

### Meaning

- Container automatically restarts if:
  - It crashes
  - Docker service restarts
  - System reboots

---

### Important Behavior

Restart does NOT always happen if:

- Container is manually stopped (docker stop)
- Container is manually killed (docker kill)

---

### Correct Testing Method

Restart Docker service:

sudo systemctl restart docker

Check:

docker ps

---

### Learning

- Restart policies ensure high availability
- Used in production environments

---

## Debugging Workflow (Real DevOps Approach)

1. Check container:

docker ps

2. Check logs:

docker logs <container_id>

3. Check ports:

ss -tuln

4. Check application response:

curl localhost:80

5. Fix issue and restart service

---

## Key Concepts

### Container Lifecycle

- Created
- Running
- Stopped
- Removed

---

### Reliability

Ensuring application:

- Restarts automatically
- Remains available
- Recovers from failures

---

### Difference Between Failure vs Manual Stop

Failure:
- Application crash
- System reboot
→ Auto restart ✔

Manual stop:
- docker stop
- docker kill
→ No restart ❌

---

## Real DevOps Responsibilities

- Monitor application health
- Debug issues quickly
- Ensure uptime
- Maintain service reliability

---

## Cleanup (CRITICAL)

1. Stop instance
2. Terminate instance
3. Verify no running resources

---

## Key Learning

- Debugging is a core DevOps skill
- Logs provide root cause of issues
- Restart policies improve reliability
- Not all failures behave the same
- Production systems must recover automatically