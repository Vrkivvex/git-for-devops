# Day 20 – Public vs Private Subnet & NAT Gateway

---

## What is a Subnet

A subnet is a logical subdivision of a VPC network.

It allows you to divide your VPC into smaller networks for better organization, security, and control.

---

## Types of Subnets

### 1. Public Subnet

A public subnet is a subnet that has direct access to the internet.

---

## How Public Subnet Works

A subnet becomes "public" when:

1. It is associated with a route table
2. That route table contains:
   0.0.0.0/0 → Internet Gateway (IGW)

---

## Key Characteristics of Public Subnet

- Instances can have public IP addresses
- Accessible directly from the internet
- Can send and receive traffic from internet

---

## Use Cases

- Bastion Host (jump server)
- Load Balancers
- Frontend web servers

---

## Example Flow

User → Internet → IGW → Public Subnet → EC2

---

## 2. Private Subnet

A private subnet is a subnet that does NOT have direct internet access.

---

## How Private Subnet Works

- No route to Internet Gateway
- Route table does NOT contain IGW
- Instances do NOT have public IP

---

## Key Characteristics of Private Subnet

- Cannot be accessed from internet
- More secure
- Used for internal services

---

## Use Cases

- Backend application servers
- Databases (RDS)
- Internal services

---

## Example Flow

Public EC2 → Private EC2 (via internal network)

---

## Key Difference

| Feature | Public Subnet | Private Subnet |
|--------|--------------|---------------|
| Internet Access | Yes | No |
| Public IP | Yes | No |
| Security | Less | More |
| Usage | Frontend | Backend |

---

## Important Concept

Subnet is NOT public or private by default.

It becomes public/private based on:

- Route Table configuration
- Internet Gateway connection

---

## NAT Gateway (Network Address Translation)

### Definition

NAT Gateway allows instances in a private subnet to access the internet
WITHOUT allowing the internet to access them.

---

## Why NAT is Needed

Problem:

- Private subnet has no internet access
- But instances need:
  - Software updates (apt, yum)
  - API calls
  - Download packages

---

## Solution

Use NAT Gateway.

---

## How NAT Works

Private EC2 → NAT Gateway → Internet ✔  
Internet → Private EC2 ❌ (blocked)

---

## Key Concept

NAT provides:

- Outbound internet access ✔
- No inbound access ❌

This ensures security.

---

## Where NAT is Placed

NAT Gateway is created in:

- Public Subnet ✔

Reason:
- It needs access to Internet Gateway

---

## Requirements for NAT Gateway

1. Must be inside Public Subnet
2. Must have Elastic IP
3. VPC must have Internet Gateway

---

## Route Table Configuration (IMPORTANT)

For Private Subnet:

0.0.0.0/0 → NAT Gateway

---

## Complete Flow

Private EC2
→ Route Table (0.0.0.0/0 → NAT)
→ NAT Gateway (Public Subnet)
→ Internet Gateway
→ Internet

---

## What You Did Practically

1. Created Private Subnet
2. Created Elastic IP
3. Created NAT Gateway (in public subnet)
4. Created new route table
5. Added route:
   0.0.0.0/0 → NAT Gateway
6. Associated route table with private subnet
7. Launched EC2 in private subnet
8. Verified internet using ping

---

## Testing Results

- Private instance had NO public IP ✔
- Could NOT be accessed directly ✔
- Could access internet via NAT ✔

---

## Security Benefit

- Internal servers are hidden
- No direct attack surface
- Controlled access via Bastion Host

---

## Important Note (Cost)

- NAT Gateway is NOT free
- Charges per hour + data usage

---

## Summary

- NAT enables internet for private subnet
- Keeps instances secure
- Used in real-world production architectures

---

## Bastion Host (Jump Server)

### Definition

A Bastion Host is a server in the public subnet used to securely access
instances in a private subnet.

---

## Why Bastion Host is Needed

Problem:

- Private instances have no public IP
- Cannot be accessed directly from internet

---

## Solution

Use a Bastion Host.

---

## How it Works

Laptop → Public EC2 (Bastion) → Private EC2

---

## Steps Performed

1. Launched public EC2 (with public IP)
2. Connected from local machine using SSH
3. Copied private key to public instance
4. SSH from public instance to private instance

---

## Key Concept

Bastion Host acts as a secure entry point to private network.

---

## Security Benefit

- Only one server exposed to internet
- Private servers remain hidden
- Reduced attack surface

---

## Full Architecture (What You Built)

Internet
→ Internet Gateway
→ Public Subnet
   → Bastion Host (Public EC2)
   → NAT Gateway
→ Private Subnet
   → Private EC2

---

## Traffic Flow

### Inbound (User Access)

User → Bastion Host → Private Server

---

### Outbound (Internet Access)

Private Server → NAT → Internet

---

## Important Concepts

### 1. Layered Security

- Public layer (Bastion)
- Private layer (Application, DB)

---

### 2. Least Exposure

- Only required resources exposed
- Everything else hidden

---

### 3. Separation of Concerns

- Public subnet → external communication
- Private subnet → internal logic

---

## Real World Usage

Production systems use this architecture:

- Web servers → public subnet
- App servers → private subnet
- Databases → private subnet

---

## Key Learnings

- Public subnet gives direct internet access
- Private subnet is secure and isolated
- NAT allows outbound internet only
- Bastion enables controlled access

---

## Summary

- Secure architecture requires separation
- NAT ensures safe internet access
- Bastion provides controlled entry
- This is standard AWS production design

---