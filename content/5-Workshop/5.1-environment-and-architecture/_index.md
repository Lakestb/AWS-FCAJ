---
title : "Environment Setup & Architectural Overview"
date : "2024-05-15"
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

### 5.1. Environment Setup & Architectural Overview

#### 5.1.1. Region Selection & Administrative Setup
* **Region**: Asia Pacific (Singapore) — `ap-southeast-1`.
* **IAM Account**: `cloud-admin` (adhering to best practices avoiding root usage for operational tasks).

> 📷 **Artifact**: Console screenshot demonstrating Region selection and logged-in IAM entity.

#### 5.1.2. Complete Target Architecture
A modern decoupled architecture blending 2-tier infrastructure with serverless and container capabilities across 4 pillars:
* **Compute & Database**: EC2 (WordPress) + RDS (MySQL) + S3 (media/backup storage).
* **High Availability**: Application Load Balancer + Auto Scaling Group.
* **Serverless Backend**: Lambda + API Gateway + DynamoDB (Guestbook service).
* **Automation & Container**: Docker + ECS Fargate + EventBridge Scheduler (scheduled backups).

> 📷 **Artifact**: Comprehensive architectural diagram created in draw.io reflecting all 4 functional tiers.
