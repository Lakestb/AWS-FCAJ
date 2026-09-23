---
title : "Resource Cleanup"
date : "2024-05-15"
weight : 8
chapter : false
pre : " <b> 5.8. </b> "
---

### 5.8. Resource Cleanup

Conducted in reverse sequence of provisioning (Modules 5.7 → 5.1) to release all allocated AWS resources post-grading and avoid recurring costs.

#### 5.8.1. Delete EventBridge Schedules
* Delete `wordpress-daily-backup` schedule to prevent recurring container executions.

#### 5.8.2. Teardown ECS Tasks, Clusters, and ECR Repositories
* Deregister `wordpress-backup-task` Task Definition.
* Delete `wordpress-cluster` ECS cluster.
* Remove `wordpress-backup` ECR repository along with all container tags.

#### 5.8.3. Dismantle High Availability Infrastructure
* Delete Auto Scaling Group `wordpress-asg` (set Desired to 0 first, wait for termination, then delete).
* Remove ALB `wordpress-alb` and Target Group `wordpress-tg`.
* Delete Launch Template and deregister `wordpress-app-ami-v1` AMI (including backing EBS snapshots).

#### 5.8.4. Remove Serverless Stack
* Delete API Gateway `GuestbookAPI`.
* Delete Lambda Function `GuestbookHandler`.
* Delete DynamoDB table `GuestbookMessages`.
* Delete SNS Topic `guestbook-new-message` (if configured).

#### 5.8.5. Teardown Observability Resources
* Delete CloudWatch Alarm `EC2-High-CPU-Utilization` and Dashboard `WordPress-Production-Dashboard`.
* Delete SNS Topic `ec2-high-cpu-alert`.

#### 5.8.6. Delete Database Tier
* Create final snapshot of RDS `wordpress-db` (optional) and delete RDS instance.

#### 5.8.7. Terminate Compute & Clear Storage
* Terminate all remaining EC2 instances.
* Delete Security Groups: `ec2-web-sg`, `RDS-SG`, `ALB-SG`.
* Empty and delete S3 bucket `my-portfolio-blog-media-...`.

#### 5.8.8. Teardown Networking (VPC)
* Delete Subnets, Route Tables, and detach/delete Internet Gateway.
* Delete VPC `my-project-vpc`.

#### 5.8.9. Delete IAM Roles & Policies (Final Step)
* Delete IAM Roles (`EventBridgeSchedulerECSRole`, `ecsTaskExecutionRole`, `EcsBackupTaskRole`, `GuestbookLambdaRole`, EC2 Role).
* Delete corresponding customer-managed policies.
