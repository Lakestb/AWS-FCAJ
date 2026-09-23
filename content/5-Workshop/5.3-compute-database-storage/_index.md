---
title : "Compute, Database & Storage (EC2, RDS, S3, IAM)"
date : "2024-05-15"
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

### 5.3. Compute, Database & Storage: EC2, RDS, S3, IAM

#### 5.3.1. Web/Application Tier (Amazon EC2)
* **OS**: Ubuntu Server 24.04 LTS, **Instance type**: `t3.micro`.
* **LAMP Stack**: Apache 2.4, PHP 8.3, WordPress.
* Attached **IAM Instance Profile** for passwordless, credential-free S3 media synchronization.

> 📷 **Artifact**: WordPress administrative home page resolving via EC2 public IP.

#### 5.3.2. Database Tier (Amazon RDS for MySQL)
* **Engine**: MySQL Community, **Instance class**: `db.t4g.micro`.
* **Endpoint**: `wordpress-db.cnwgwiseq95o.ap-southeast-1.rds.amazonaws.com`, **Database**: `wordpress`.
* Hosted strictly within Private Subnets without Public IP assignment.

> 📷 **Artifact**: RDS Configuration and Connectivity dashboard showing Available status.

#### 5.3.3. Static Asset Storage (Amazon S3)
* **Bucket**: `my-portfolio-blog-media-635176221447-ap-southeast-1-an`.
* Synchronized through WP Offload Media Lite plugin.

> 📷 **Artifact**: S3 bucket object list containing offloaded WordPress media files.

#### 5.3.4. Access Security & IAM Roles
* EC2 IAM Role scoped according to Least Privilege principles.

> 📷 **Artifact**: IAM Role permissions policy configuration attached to EC2.
