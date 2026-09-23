---
title : "Proposal"
date : "2024-05-15"
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

### Project Proposal: Comprehensive WordPress Infrastructure on AWS: From 2-Tier to Serverless, High Availability, and Containerization

---

### 1. Executive Summary

This proposal presents a solution for modernizing WordPress web systems on the AWS cloud platform. Instead of an all-in-one monolith deployment on a single instance that poses security risks and single points of failure, this project designs a layered architecture following the AWS Well-Architected Framework:

* **Decoupled 2-Tier & Storage**: Decouple the web server (EC2) from the database (RDS MySQL) and offload static media to Amazon S3.
* **Elastic Scalability (High Availability)**: Implement an Application Load Balancer (ALB) and Auto Scaling Group (ASG) to dynamically balance load and scale based on traffic.
* **Serverless Backend**: Build a standalone Guestbook service using API Gateway, Lambda, and DynamoDB.
* **Container Automation**: Package automated database backups into Docker containers executed serverless on ECS Fargate via EventBridge Scheduler, replacing legacy local crons.

---

### 2. Problem Statement

#### Current Pain Points
* **Single Point of Failure (SPOF)**: Hosting both web server and database on a single instance leads to complete downtime during memory exhaustion or CPU spikes.
* **Security Vulnerabilities**: Direct exposure of database and SSH ports to the public internet; hardcoding static access keys inside application source code poses credential leakage risks.
* **Lack of Elasticity**: Monolithic instances cannot automatically scale during traffic surges, causing network bottlenecks or service outages.
* **Brittle Local Backups**: Backup cron jobs running directly on EC2 instances mean that instance termination or disk failure destroys both backup routines and local archive files.

#### Proposed Solution
A modern hybrid architecture combining decoupled multi-tier topology with Serverless and Container technologies:
* **Core Flow (2-Tier & Storage)**: Place web servers on EC2 in Public Subnets and databases on RDS in isolated Private Subnets; attach IAM Roles for seamless S3 media offloading without static keys.
* **High Availability Flow (ALB & ASG)**: ALB distributes incoming traffic across an Auto Scaling Group, dynamically provisioning or terminating instances based on CPU metrics.
* **Serverless Flow (Guestbook Service)**: Decouple feedback workflows into a fully serverless pipeline (API Gateway → Lambda → DynamoDB).
* **Container Flow (Automated Scheduled Backup)**: Containerize database backup routines with Docker, push images to Amazon ECR, and execute on-demand via ECS Fargate triggered by EventBridge.

---

### 3. Solution Architecture

#### Overall Architecture Diagram
*(Architecture diagram placeholder)*

#### 4 Core Processing Flows:
1. **Web & Decoupled Data Flow (EC2 + RDS + S3)**
   * End-users access WordPress via the public DNS/IP of the EC2 Web Server.
   * EC2 reads and writes structured data to an isolated Amazon RDS MySQL instance in the Private Subnet over port 3306.
   * All media uploads are automatically offloaded directly to Amazon S3 through an attached IAM Instance Profile.

2. **High Availability Flow (ALB + ASG)**
   * Application Load Balancer terminates HTTP/HTTPS traffic at the edge and forwards requests across healthy EC2 targets.
   * Auto Scaling Group replaces unhealthy instances automatically and scales out when average CPU utilization exceeds 70%.

3. **Serverless Guestbook Flow (API Gateway + Lambda + DynamoDB)**
   * Embedded frontend forms submit POST requests to Amazon API Gateway.
   * API Gateway invokes AWS Lambda (Python 3.12) to validate data and persist records into Amazon DynamoDB.
   * Lambda triggers real-time email notifications via Amazon SNS upon receiving new entries.

4. **Containerized Scheduled Backup Flow (Docker + ECS Fargate + EventBridge)**
   * Amazon EventBridge Scheduler fires scheduled backup events daily at 02:00 AM.
   * ECS Fargate pulls the backup container image from Amazon ECR, executes `mysqldump`, compresses files, and uploads archives to the `backups/` prefix on S3.

#### AWS Services Utilized
* **Amazon VPC**: Isolated networking with 2 Public Subnets and 2 Private Subnets spanning 2 Availability Zones.
* **Amazon EC2 & Auto Scaling**: Elastic compute infrastructure.
* **Amazon RDS (MySQL)**: Managed relational database tier.
* **Amazon S3**: Scalable object storage for media and automated database backups.
* **Application Load Balancer**: Layer 7 load balancing across multiple AZs.
* **API Gateway, Lambda, DynamoDB**: Event-driven serverless feedback backend.
* **Amazon ECR & ECS Fargate**: Serverless container hosting and task orchestration.
* **CloudWatch, SNS & CloudTrail**: Monitoring metrics, alerting, and governance auditing.

---

### 4. Technical Implementation

#### Implementation Phases
* **Phase 1: VPC Networking & Security Baseline**
  * Provision VPC `10.0.0.0/16` with dual Public and Private Subnets across `ap-southeast-1a` and `ap-southeast-1b`.
  * Attach Internet Gateway to Public Subnets; restrict Private Subnets to local routing. Harden SSH security group ingress rules.
* **Phase 2: 2-Tier Foundation & Media Offloading**
  * Install LAMP stack and WordPress on EC2.
  * Launch Amazon RDS MySQL within a private DB Subnet Group.
  * Create Amazon S3 bucket and attach IAM Instance Profile to EC2 for media offloading.
* **Phase 3: Observability, Alerting & Auditing**
  * Build CloudWatch Dashboard monitoring `CPUUtilization` and `DatabaseConnections`.
  * Configure SNS-backed alarms triggering alerts when CPU utilization reaches $\ge$ 80%.
  * Audit control-plane operations via CloudTrail Event History.
* **Phase 4: Serverless Feature Extension (Guestbook)**
  * Create `GuestbookMessages` table in DynamoDB (Provisioned mode).
  * Develop AWS Lambda handler (Python 3.12) and expose via CORS-enabled REST API Gateway.
  * Embed frontend form into WordPress theme to consume backend endpoints.
* **Phase 5: High Availability (ALB + ASG)**
  * Create customized AMI from EC2 instance and formulate Launch Template.
  * Provision ALB, configure Target Group health checks (`/`), and register with Auto Scaling Group.
* **Phase 6: Containerized Backup Automation**
  * Craft Dockerfile packaging database backup scripts and push image to Amazon ECR.
  * Configure ECS Fargate Task Definition and schedule automated cron execution via EventBridge.

---

### 5. Roadmap & Milestones

```text
+-----------------------------------------------------------------------------------+
| Weeks 1 - 3: VPC Architecture & 2-Tier Foundation                                 |
|   - Design VPC, Subnets, Routing, and secure Security Groups                     |
|   - Deploy EC2 (LAMP), establish RDS MySQL connectivity, configure S3 Offload    |
+-----------------------------------------------------------------------------------+
                                  │
                                  ▼
+-----------------------------------------------------------------------------------+
| Weeks 4 - 5: Serverless Backend & Operational Observability                       |
|   - Develop API Gateway + Lambda + DynamoDB for Guestbook service                |
|   - Build CloudWatch Dashboards, SNS Alarms, and configure CloudTrail audits      |
+-----------------------------------------------------------------------------------+
                                  │
                                  ▼
+-----------------------------------------------------------------------------------+
| Weeks 6 - 8: High Availability, Container Automation & Final Wrap-up              |
|   - Create AMI, deploy Application Load Balancer and Auto Scaling Group           |
|   - Containerize backup scripts, deploy on ECR/ECS Fargate with EventBridge       |
|   - End-to-end integration testing, evaluation, and resource cleanup              |
+-----------------------------------------------------------------------------------+
```

---

### 6. Budget & Cost Estimation

The project is aligned with AWS Free Tier and Always Free allowances:

| AWS Service | Configuration / Usage Scale | Estimated Monthly Cost (USD) |
| :--- | :--- | :--- |
| **Amazon EC2** | 1 instance t3.micro (750 hours/month) | \$0.00 (Free Tier) |
| **Amazon RDS** | 1 instance db.t4g.micro, 20GB SSD | \$0.00 (Free Tier) |
| **Amazon S3** | Media and backup storage (< 5GB) | \$0.00 (Free Tier) |
| **AWS Lambda** | < 10,000 requests/month | \$0.00 (Always Free) |
| **Amazon DynamoDB** | Provisioned mode: 5 RCU / 5 WCU | \$0.00 (Always Free) |
| **Amazon ECS Fargate** | 0.25 vCPU / 0.5 GB RAM, ~2 mins/day | < \$0.05 |
| **CloudWatch & CloudTrail** | 1 Dashboard, 1 Alarm, 90-day Event History | \$0.00 (Free Tier) |
| **Application Load Balancer** | Short-term testing and artifact verification | ~\$0.50 - \$1.00 |
| **Estimated Total** | **Full development and testing environment** | **< \$1.50 USD / Month** |

---

### 7. Risk Assessment & Mitigation

| Potential Risk | Impact | Probability | Mitigation Strategy |
| :--- | :--- | :--- | :--- |
| **Unexpected AWS Charges** | High | Medium | Configure AWS Budget alerts at \$5.00/month. Delete ALBs and teardown testing workloads immediately after review. |
| **ALB Target Group Empty (0 targets)** | Medium | Medium | Verify Load Balancing integrations in ASG settings to ensure proper Target Group association. |
| **Database Client Version Mismatch** | Low | Low | Tailor `mysqldump` flags in Docker container to maintain compatibility with MySQL 8.0 / MariaDB. |
| **IAM Permission Denied Errors** | Medium | Low | Maintain correct Trust Policies for `scheduler.amazonaws.com` and enforce Least Privilege. |

---

### 8. Expected Outcomes

* **Robust, Production-Grade Architecture**: Successfully operationalize a resilient, self-healing, decoupled WordPress deployment on AWS.
* **Demonstrated Multi-Domain Competency**: Proven hands-on proficiency across VPC networking, EC2 compute, RDS databases, S3 object storage, Serverless functions, and Container orchestration.
* **Audit-Ready Internship Deliverables**: Comprehensive technical documentation, version-controlled infrastructure code, and rigorous cost-optimization strategies.
