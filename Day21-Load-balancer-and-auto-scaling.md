# Day 21 – Load Balancer & Auto Scaling

---

## What is a Load Balancer

A Load Balancer is a service that distributes incoming traffic across multiple servers.

---

## Why Load Balancer is Needed

Problem without LB:

- Single EC2 handles all traffic
- If it crashes → application down
- Cannot handle high load

---

## Solution

Use Load Balancer to:

- Distribute traffic
- Improve availability
- Increase scalability

---

## Types of Load Balancers in AWS

1. Application Load Balancer (ALB) – HTTP/HTTPS (Layer 7)
2. Network Load Balancer (NLB) – TCP/UDP (Layer 4)
3. Gateway Load Balancer – advanced use

---

## We Used

Application Load Balancer (ALB)

---

## How ALB Works

User → Load Balancer → Target Group → EC2

---

## Components

### 1. Load Balancer

- Entry point for users
- Has DNS name
- Distributes traffic

---

### 2. Target Group

- Contains EC2 instances
- LB sends traffic here

---

### 3. Listener

- Defines protocol and port (HTTP:80)
- Forwards traffic to target group

---

## Important Requirement

ALB requires:

- At least 2 subnets in different Availability Zones

Reason:

- High availability
- Fault tolerance

---

## Health Checks (VERY IMPORTANT)

ALB continuously checks if EC2 is healthy.

---

### Health Check Details

- Protocol: HTTP
- Path: /
- Interval: 30 sec
- Timeout: 5 sec

---

## Behavior

- Healthy → receives traffic ✔
- Unhealthy → removed automatically ❌

---

## Security Group

Must allow:

- HTTP (port 80) from 0.0.0.0/0

---

## What You Did Practically

1. Created target group
2. Created ALB
3. Selected 2 public subnets
4. Attached target group
5. Registered EC2
6. Tested via DNS

---

## Result

Accessing LB DNS → nginx page opened ✔

---

## What is Auto Scaling

Auto Scaling is a service that automatically adjusts the number of EC2 instances
based on demand.

---

## Why Auto Scaling is Needed

Problem:

- Traffic is not constant
- Sometimes low, sometimes high

Without Auto Scaling:

- Too many servers → waste money ❌
- Too few servers → app crash ❌

---

## Solution

Auto Scaling dynamically:

- Adds instances (scale out) ✔
- Removes instances (scale in) ✔

---

## Key Components

### 1. Launch Template

Defines how EC2 should be created:

- AMI (OS)
- Instance type
- Security group
- Key pair

---

### 2. Auto Scaling Group (ASG)

Group of EC2 instances managed automatically.

---

### 3. Scaling Policy

Rules that define when to scale.

---

## Types of Scaling

### 1. Dynamic Scaling

Based on metrics (like CPU usage)

Example:
- CPU > 70% → add instance
- CPU < 30% → remove instance

---

### 2. Scheduled Scaling

Scale at specific time

Example:
- Increase servers at 9 AM
- Decrease at night

---

### 3. Manual Scaling

User manually changes capacity

---

## Important Terms

### Minimum Capacity

Minimum number of instances always running

---

### Desired Capacity

Target number of instances

---

### Maximum Capacity

Maximum limit of instances

---

## Example

Min = 1  
Desired = 2  
Max = 5  

→ System maintains 2 instances normally  
→ Can scale up to 5 if needed  

---

## How It Works with Load Balancer

User → Load Balancer → Auto Scaling Group → EC2

---

## Behavior

- New instances auto-register to target group ✔
- Failed instances replaced automatically ✔

---

## High Availability

- Instances spread across multiple AZs
- If one AZ fails → others still work

---

## Real-World Example

E-commerce site:

- Sale time → high traffic → scale up
- Night → low traffic → scale down

---

## Benefits

- Cost optimization ✔
- High availability ✔
- Fault tolerance ✔
- Automation ✔

---

## Key Learning

- Auto Scaling removes manual work
- Ensures app is always available
- Works together with Load Balancer

---

## Summary

- Load Balancer → distributes traffic
- Auto Scaling → manages servers
- Together → scalable + reliable system