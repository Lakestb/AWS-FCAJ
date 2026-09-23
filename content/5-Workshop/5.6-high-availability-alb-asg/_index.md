---
title : "High Availability (ALB & Auto Scaling)"
date : "2024-05-15"
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

### 5.6. High Availability: Application Load Balancer & Auto Scaling

#### 5.6.1. Golden AMI Packaging
* **AMI**: `wordpress-app-ami-v1`, created from the functional baseline EC2 instance.

> 📷 **Artifact**: AMI management console with Available state.

#### 5.6.2. EC2 Launch Template Configuration
* **Template**: `wordpress-launch-template` configured with `t3.micro`, `ec2-web-sg`, and designated key pair.

> 📷 **Artifact**: Launch Template configuration details.

#### 5.6.3. ALB & Target Group Topology
* **ALB**: `wordpress-alb`, Internet-facing, dual Availability Zones.
* **Target Group**: `wordpress-tg`, HTTP:80, Health check path `/`.

> 📷 **Artifact**: ALB DNS name and Target Group health check configurations.

#### 5.6.4. Auto Scaling Group Deployment
* **ASG**: `wordpress-asg`, Desired: 1, Min: 1, Max: 2.
* **Policy**: Target tracking scaling at 70% average CPU utilization.

> 📷 **Artifact**: ASG capacity metrics and target tracking policies.

#### 5.6.5. Real-World Troubleshooting & Root Cause Analysis
During integration testing, Target Group registered 0 active targets despite healthy instance execution within ASG. Inspection of Activity History pinpointed missing Target Group associations in ASG Load Balancing integrations. Resolved by attaching `wordpress-tg` directly under ASG Integrations, immediately registering healthy targets.

> 📷 **Artifact**: Target Group status before (0 targets) vs after remediation (1 Healthy), alongside WordPress resolution over ALB DNS.
