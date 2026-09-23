---
title : "Networking Infrastructure (VPC, Subnet, IGW)"
date : "2024-05-15"
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

### 5.2. Networking Infrastructure: VPC, Subnet, Internet Gateway

#### 5.2.1. VPC Creation
* **VPC**: `my-project-vpc` (`vpc-0b489eb298393e445`), CIDR block `10.0.0.0/16`.

#### 5.2.2. Multi-Tier Subnet Topology
* **Public Subnet 1**: `subnet-011686e77c0d42601` — `10.0.0.0/20` — `ap-southeast-1a` (hosts EC2, ALB, and ECS Tasks).
* **Public Subnet 2**: `subnet-037a8c50b5e7ec755` — `10.0.16.0/20` — `ap-southeast-1b` (ALB multi-AZ requirement).
* **Private Subnet 1**: `subnet-008f0d773c67a3970` — `10.0.128.0/20` — `ap-southeast-1a` (hosts RDS MySQL).
* **Private Subnet 2**: `subnet-0a953901b7b370b78` — `10.0.144.0/20` — `ap-southeast-1b` (DB Subnet Group secondary AZ).

> 📷 **Artifact**: VPC Subnets console view detailing configured CIDRs and Availability Zones.

#### 5.2.3. Internet Gateway & Routing Tables
* Internet Gateway associated with VPC; Public Route Table routes `0.0.0.0/0` via IGW.
* Private Route Table restricted exclusively to `local` routes, isolating database instances.

> 📷 **Artifact**: Route table rules for both Public and Private subnets.

#### 5.2.4. Security Groups
* **`ec2-web-sg`** (`sg-043b5223abc256608`): Ingress HTTP (80) & HTTPS (443) from `0.0.0.0/0`, SSH (22) strictly whitelisted to administrative `/32` IP.
* **`RDS-SG`**: Restricts MySQL port 3306 ingress strictly from `ec2-web-sg`.

> 📷 **Artifact**: Inbound security group rules showing locked-down SSH and database permissions.
