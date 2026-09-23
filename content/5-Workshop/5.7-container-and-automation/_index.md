---
title : "Containerization & Automation (Docker, ECS, EventBridge)"
date : "2024-05-15"
weight : 7
chapter : false
pre : " <b> 5.7. </b> "
---

### 5.7. Containerization & Automation: Docker, ECS Fargate, EventBridge Scheduler

Decoupled database backup routine packaged as a Docker container running on-demand via ECS Fargate.

#### 5.7.1. Docker Container Packaging
* **Base image**: `debian:bookworm-slim` with `default-mysql-client`, `awscli`, and `gzip`.
* **Execution Script**: Parameterized via environment variables without hardcoded secrets.

> 📷 **Artifact**: Dockerfile specification and successful build transcript.

#### 5.7.2. Image Distribution to Amazon ECR
* **Repository**: `wordpress-backup`.

```bash
aws ecr get-login-password | docker login --username AWS --password-stdin <account>.dkr.ecr.ap-southeast-1.amazonaws.com
docker build -t wordpress-backup .
docker tag wordpress-backup:latest <account>.dkr.ecr.ap-southeast-1.amazonaws.com/wordpress-backup:latest
docker push <account>.dkr.ecr.ap-southeast-1.amazonaws.com/wordpress-backup:latest
```

> 📷 **Artifact**: ECR repository dashboard exhibiting latest image tag.

#### 5.7.3. Scoped Task Execution Roles
* **`ecsTaskExecutionRole`**: Managed policy for ECR authentication and log ingestion.
* **`EcsBackupTaskRole`**: Dedicated policy granting `s3:PutObject` strictly to `backups/` prefix.

> 📷 **Artifact**: IAM role permissions attached to container tasks.

#### 5.7.4. ECS Task Definition on AWS Fargate
* **Cluster**: `wordpress-cluster` (Serverless Fargate launch type).
* **Task Definition**: `wordpress-backup-task`, 0.25 vCPU, 0.5 GB memory.

> 📷 **Artifact**: Task Definition specification showing container and environment variables.

#### 5.7.5. Testing & Debugging MariaDB/MySQL Client Flags
Initial execution failed with Exit code 7 (`mysqldump: unknown variable 'set-gtid-purged=OFF'`) stemming from MariaDB client conventions on Debian. Removed the redundant flag, rebuilt image, and re-pushed to ECR, resulting in Exit code 0 success.

> 📷 **Artifact**: Failed task log vs successful completion with S3 object archive creation.

#### 5.7.6. Scheduled Execution with Amazon EventBridge
* **Schedule**: `wordpress-daily-backup`, Cron expression: `0 2 * * ? *` (2:00 AM daily).
* **Target**: ECS RunTask on Fargate (using roles from section 5.7.3).

> 📷 **Artifact**: Enabled EventBridge schedule and automated ECS task trigger logs.
