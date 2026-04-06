Day 22 – Auto Scaling + Load Balancer

---

Full Architecture:
User (browser)
   ↓
Load Balancer (ALB)
   ↓
Target Group
   ↓
EC2 Instances (managed by ASG)
   ↓
Nginx (web server)

---

What each part does (deep):

User:
- Sends HTTP request (website open)

---

Load Balancer (ALB):
- Entry point of system
- Receives all incoming traffic
- Decides WHICH EC2 should handle request
- Works at Layer 7 (HTTP/HTTPS)

Important:
- Must be Internet-facing → for public access
- If Internal → only works inside VPC (your mistake)

Needs:
- At least 2 public subnets (different AZ)
Reason:
- High availability (if one AZ fails → other works)

---

Target Group:
- Middle layer between LB and EC2
- Contains list of EC2 instances

Main job:
- LB sends request → Target Group
- Target Group forwards to EC2

Also does:
- Health checks (very important)

---

Auto Scaling Group (ASG):
- Automatically manages EC2 instances

Responsibilities:
- Launch new instances
- Terminate old instances
- Replace unhealthy instances
- Maintain desired number

---

ASG Concepts:

Min:
- Minimum instances always running

Desired:
- Target number of instances

Max:
- Upper limit of instances

Example:
Min = 1
Desired = 1
Max = 3

Meaning:
- Always at least 1 instance
- Normally 1 running
- Can go up to 3 if needed

---

Launch Template:
- Blueprint for EC2 creation

Contains:
- AMI (OS)
- Instance type (t2.micro)
- Key pair (SSH access)
- Security group
- User Data script

Important:
ASG NEVER creates EC2 manually
→ It ALWAYS uses Launch Template

---

Flow (real request):

1. User opens website
2. Request hits Load Balancer
3. LB checks Target Group
4. Target Group selects healthy EC2
5. Request goes to EC2
6. Nginx processes request
7. Response goes back to user

---

Key Understanding:

Load Balancer = traffic controller  
Target Group = connection bridge  
ASG = server manager  
Launch Template = server blueprint  

---

Very Important Rule:

LB DOES NOT talk to EC2 directly  
It ALWAYS goes through Target Group

---

Health Checks (VERY IMPORTANT):

Load Balancer does NOT blindly send traffic.
It first checks if EC2 is working.

---

How it works:

LB → sends request to EC2 on:
Protocol: HTTP
Port: 80
Path: /

If response OK → healthy ✔
If no response → unhealthy ❌

---

Health States:

initial:
- Instance just launched
- Still being tested

healthy:
- Working properly
- Receives traffic ✔

unhealthy:
- Not responding
- Removed from traffic ❌

---

Why instance becomes UNHEALTHY:

1. Nginx not installed
2. Nginx not running
3. Port 80 blocked (security group)
4. App not responding

---

Your case:

Instance was UNHEALTHY because:
- Nginx not installed ❌

Fix:
- Install nginx manually OR
- Use User Data (better)

---

User Data (VERY IMPORTANT):

This script runs when EC2 launches.

Purpose:
- Automate setup
- No manual work needed

---

Script used:

#!/bin/bash
apt update
apt install nginx -y
systemctl start nginx
systemctl enable nginx

---

What it does:

1. Updates system
2. Installs nginx
3. Starts nginx
4. Enables nginx on boot

---

Without User Data:

ASG creates EC2
→ EC2 empty
→ No nginx
→ Health check fails ❌

---

With User Data:

ASG creates EC2
→ nginx auto installed ✔
→ Health check passes ✔

---

Real Debugging Steps (what you did):

Step 1:
Target group had NO targets ❌
→ Cause: ASG not attached

Fix:
Attach target group in ASG

---

Step 2:
Instance UNHEALTHY ❌
→ Cause: nginx not running

Fix:
Install/start nginx

---

Step 3:
Could not SSH ❌
→ Cause: No public IP

Fix:
Enable auto-assign public IP

---

Step 4:
LB not opening ❌
→ Cause: Internal Load Balancer

Fix:
Create Internet-facing LB

---

Important Learning:

Problem ≠ random  
Each issue has specific layer:

Network issue → public IP / LB type  
App issue → nginx  
Connection issue → security group  
Routing issue → target group  

---

Golden Rule:

If LB not working:
1. Check Target Group
2. Check Health status
3. Check EC2 (nginx)
4. Check Security Group
5. Check LB type (internal/public)

---

Auto Scaling (ASG):

Purpose:
Automatically manage EC2 instances based on load.

Capacity terms:
Min = minimum instances (never go below)
Desired = current running instances
Max = maximum limit

Example:
Min = 1
Desired = 1
Max = 3

Scaling logic:
CPU > 50% → new instance created
CPU < 50% → instance removed

Flow when new instance is created:
1. ASG needs instance
2. Uses Launch Template
3. EC2 is launched
4. User Data runs (nginx installed)
5. Instance added to Target Group
6. Health check runs
7. If healthy → receives traffic

Flow when instance is removed:
1. Load decreases
2. ASG selects instance
3. Removes it from Target Group
4. Terminates EC2

Important roles:
ASG = creates/removes instances
Load Balancer = sends traffic
Target Group = connects LB and EC2

High availability:
ASG launches instances in multiple subnets (AZs)
If one AZ fails → other still works

Explanation:

Auto Scaling is automatic server management.

Instead of manually creating EC2 when traffic increases,
AWS checks CPU and decides when to add or remove servers.

If traffic increases → more servers are created.
If traffic decreases → extra servers are removed to save cost.

Everything works automatically once configured.

ASG does not handle traffic.
Load Balancer does not create instances.

Each service has a separate role and works together.

---

Cost awareness:

Paid resources:
EC2 instances → charged when running
Load Balancer → charged per hour
Elastic IP → charged if unused
NAT Gateway → very expensive (not used here)

Free resources:
Launch Template
Target Group
Security Groups

Important:
Even if you are not using the system,
running resources will still cost money.

---

Cleanup steps:

1. Delete Load Balancer
2. Delete Auto Scaling Group
3. Terminate EC2 instances
4. Delete Target Group
5. Release Elastic IP (if any)
6. Delete unused Volumes

Always verify:
Instances = 0
Load Balancers = 0
ASG = 0
Target Groups = 0

---

What you learned:

- How Load Balancer works
- How Target Group connects services
- How Auto Scaling manages EC2
- How User Data automates setup
- How real debugging is done

---

Mistakes you faced:

- No public IP → could not SSH
- ASG not attached → no targets
- Nginx not installed → unhealthy
- Internal LB → not accessible

---

Key understanding:

System is divided into parts:

Load Balancer → handles traffic
Target Group → connects components
Auto Scaling → manages servers
Launch Template → defines server setup

Each service has its own role.

---

Real-world thinking:

In production, everything is automated.

You do not manually create servers.
System automatically:
- scales up when traffic increases
- scales down when traffic decreases
- replaces failed instances

Goal:
High availability + low cost + no downtime

---

Final understanding:

This setup is a basic production architecture.

User → Load Balancer → Target Group → EC2 (Auto Scaling)

This is how real applications are deployed in cloud.