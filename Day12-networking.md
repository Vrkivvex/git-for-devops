# Day 12 – Networking (DevOps Level Detailed)

## What is a Port

A port is a communication endpoint used by services.

Think of it as a "door" through which traffic enters a system.

Examples:

22 → SSH (remote access)  
80 → HTTP (web traffic)  
443 → HTTPS (secure web)  
6379 → Redis  
3306 → MySQL  

---

## How Ports Work

Example:

http://localhost:8080

Breakdown:

localhost → your machine (127.0.0.1)  
8080 → port number  
Service → application listening on that port  

Flow:

Browser → localhost:8080 → service → response

---

## Checking Open Ports

Command:

ss -tuln

Example output:

tcp   LISTEN   0   128   0.0.0.0:8080

Meaning:

tcp → protocol  
LISTEN → service waiting for connections  
8080 → port number  

---

## Real Example from Your System

8080 → nginx container  
53 → DNS resolver  
631 → printing service  

---

## curl (Client URL)

curl is used to send HTTP requests from terminal.

### Test local service

curl localhost:8080

Output:

HTML page from server

Meaning:

Service is running and responding.

---

### Test external website

curl google.com

Returns HTML response.

---

### Check headers only

curl -I google.com

Example:

HTTP/1.1 301 Moved Permanently  
HTTP/2 200 OK  

Meaning:

301 → redirect  
200 → success  

---

## API Testing with curl

Command:

curl http://httpbin.org/get

Output:

JSON response

Use case:

Testing backend APIs without browser.

---

## Networking Debugging Workflow (Very Important)

### Scenario: Website not working

Step 1 – Check container:

docker ps

If not running → start container

---

Step 2 – Check port:

ss -tuln | grep 8080

If not listening → app not running

---

Step 3 – Test locally:

curl localhost:8080

If no response → issue inside app

---

Step 4 – Check internet:

ping google.com

If fails → network issue

---

## Real DevOps Scenario

User says:

"Website is down"

Engineer checks:

1. Service running?
2. Port open?
3. App responding?
4. Network working?

This systematic approach is used in real production systems.

---

## Key Learning

- Ports connect users to services  
- curl tests service responses  
- ss checks open ports  
- Debugging must follow a step-by-step process  

This is a core DevOps troubleshooting skill.