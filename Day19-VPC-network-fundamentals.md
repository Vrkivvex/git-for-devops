# Day 19 – VPC (Virtual Private Cloud)

---

## What is VPC

VPC is a private network inside AWS where you launch your resources.

It isolates your infrastructure from other users.

---

## Key Idea

Internet does not directly connect to EC2.

Flow:

Internet → Internet Gateway → VPC → Subnet → EC2

---

## Why VPC is Important

- Provides network isolation
- Allows control over traffic
- Used in all real-world AWS architectures

---

## Default VPC vs Custom VPC

Default VPC:
- Pre-configured by AWS
- Easy to use
- No learning of internals

Custom VPC:
- Created manually
- Full control over network
- Used in real production environments

---

## VPC Creation

- Name: my-devops-vpc
- CIDR: 10.0.0.0/16

---

## CIDR Explanation

CIDR defines IP range of network.

Example:
10.0.0.0/16 → allows ~65,000 IP addresses

---

## Key Concept

VPC = large network block

---

## Subnet

Subnet is a smaller network inside a VPC.

It divides the VPC into segments.

---

## Subnet Creation

- Name: my-public-subnet
- CIDR: 10.0.1.0/24

---

## CIDR Meaning

10.0.1.0/24 → ~256 IP addresses

---

## Types of Subnets

Public Subnet:
- Has internet access

Private Subnet:
- No direct internet access

---

## Key Concept

VPC = big network  
Subnet = smaller network inside VPC

---

## Internet Gateway (IGW)

Internet Gateway connects your VPC to the internet.

---

## Steps Performed

1. Created IGW (my-igw)
2. Attached IGW to VPC

---

## Key Concept

VPC alone = isolated network ❌  
VPC + IGW = internet access possible 

---

## Route Table

Route Table defines how traffic flows inside the network.

---

## Route Added

Destination: 0.0.0.0/0  
Target: Internet Gateway (my-igw)

---

## Meaning

0.0.0.0/0 → all internet traffic

This rule tells AWS:
Send all internet-bound traffic to the Internet Gateway.

---

## Subnet Association

Route table must be linked to subnet.

Steps:
- Open Route Table
- Go to Subnet Associations
- Select my-public-subnet
- Save

---

## Key Concept

Route table without association = no effect ❌  
Route table + subnet association = active routing ✔

---

## Security Group

Acts as a firewall for EC2.

Rules added:
- SSH (22) → for terminal access
- HTTP (80) → for web access

---

## Final Network Flow

Internet
→ Internet Gateway
→ Route Table (0.0.0.0/0)
…
