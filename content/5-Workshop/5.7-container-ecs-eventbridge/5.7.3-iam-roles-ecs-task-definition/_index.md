---
title : "IAM Roles & ECS Task Definition"
date : "2024-05-15"
weight : 3
chapter : false
pre : " <b> 5.7.3. </b> "
---

1. Create Role `ecsTaskExecutionRole`, attach managed policy `AmazonECSTaskExecutionRolePolicy`.
2. Create Policy `EcsBackupTaskPolicy` (granting `s3:PutObject` scoped to `backups/` prefix), create Role `EcsBackupTaskRole` attaching this policy.
3. Navigate to **ECS** → **Clusters** → **Create cluster**, name `wordpress-cluster`, Infrastructure: **AWS Fargate**.

   ![IAM Roles and Active ECS Fargate Cluster](/images/5/5.7.3/01-iam-roles-ecs-cluster.png?classes=border,shadow)

4. Navigate to **Task definitions** → **Create**, name `wordpress-backup-task`, CPU 0.25 vCPU, Memory 0.5 GB, assign task execution role and task role.
5. Container: ECR image URI from step 5.7.2, inject all 5 required environment variables (`DB_HOST`, `DB_USER`, `DB_PASSWORD`, `DB_NAME`, `S3_BUCKET`).

   ![Detailed ECS Task Definition configuration for backup routine](/images/5/5.7.3/02-ecs-task-def.png?classes=border,shadow)
