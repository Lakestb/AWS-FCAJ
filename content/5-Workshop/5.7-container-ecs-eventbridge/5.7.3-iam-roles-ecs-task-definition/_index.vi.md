---
title : "IAM Roles & ECS Task Definition"
date : "2024-05-15"
weight : 3
chapter : false
pre : " <b> 5.7.3. </b> "
---

1. Tạo Role `ecsTaskExecutionRole`, gắn policy có sẵn `AmazonECSTaskExecutionRolePolicy`.
2. Tạo Policy `EcsBackupTaskPolicy` (chỉ cho phép `s3:PutObject` vào đúng thư mục `backups/`), tạo Role `EcsBackupTaskRole` gắn policy này.
3. Vào **ECS** → **Clusters** → **Create cluster**, tên `wordpress-cluster`, Infrastructure: **AWS Fargate**.

   ![IAM Roles và ECS Cluster Fargate ở trạng thái Active](/images/5/5.7.3/01-iam-roles-ecs-cluster.png?classes=border,shadow)

4. Vào **Task definitions** → **Create**, tên `wordpress-backup-task`, CPU 0.25 vCPU, Memory 0.5 GB, Task execution role và Task role chọn 2 role vừa tạo.
5. Container: image URI của ECR ở mục 5.7.2, thêm đủ 5 biến môi trường (`DB_HOST`, `DB_USER`, `DB_PASSWORD`, `DB_NAME`, `S3_BUCKET`).

   ![Cấu hình chi tiết ECS Task Definition wordpress-backup-task](/images/5/5.7.3/02-ecs-task-def.png?classes=border,shadow)
