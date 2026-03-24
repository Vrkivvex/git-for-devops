# Day 11 – Linux Services & Logs

## What is a Service

A service is a background process that runs continuously in Linux.

Examples:

- docker → container engine
- ssh → remote login
- nginx → web server

Services are managed using systemctl.

---

## systemctl Commands

Check service status:

systemctl status docker

Start service:

sudo systemctl start docker

Stop service:

sudo systemctl stop docker

Restart service:

sudo systemctl restart docker

---

## Service Status Meaning

active (running) → service is working  
inactive (dead) → service stopped  
failed → error in service  

---

## Enable Service at Boot

sudo systemctl enable docker

Check:

systemctl is-enabled docker

Meaning:

Service will start automatically when system boots.

---

## Docker Service vs Socket

docker.service → main service  
docker.socket → auto-start trigger  

Even if docker is stopped, socket can restart it.

---

## Logs (journalctl)

View logs of a service:

journalctl -u docker

View last logs:

journalctl -u docker -n 20

Live logs:

journalctl -u docker -f

---

## Real DevOps Use Case

If a service fails:

1. Check status:
   systemctl status docker

2. Check logs:
   journalctl -u docker

3. Identify issue and fix

---

## Key Learning

Services are critical in Linux servers.

Used for:

- running applications
- managing background processes
- debugging system issues using logs