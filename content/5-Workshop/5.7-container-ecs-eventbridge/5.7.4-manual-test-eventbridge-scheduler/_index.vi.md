---
title : "Chạy thử và Amazon EventBridge Scheduler"
date : "2024-05-15"
weight : 4
chapter : false
pre : " <b> 5.7.4. </b> "
---

1. Chạy thử thủ công: **Task definitions** → `wordpress-backup-task` → **Deploy** → **Run task**, chọn cluster, Launch type Fargate, 1 Public Subnet, Security group `ec2-web-sg`, Public IP: Turned on.
2. Kiểm tra CloudWatch Logs (`/ecs/wordpress-backup-task`) và file backup mới trên S3 để xác nhận chạy thành công (Exit code 0).

   ![Task ECS Fargate chạy thành công với Exit code 0](/images/5/5.7.4/01-ecs-run-task-success.png?classes=border,shadow)

   ![File backup nén cơ sở dữ liệu hiển thị an toàn trên S3 Bucket](/images/5/5.7.4/02-s3-backup-file.png?classes=border,shadow)

3. Vào **EventBridge** → **Scheduler** → **Create schedule**, tên `wordpress-daily-backup`, Recurring schedule, Cron-based: `0 2 * * ? *`.
4. Target: Templated targets → **Amazon ECS RunTask**, chọn cluster/task definition, cấu hình network giống bước chạy thử.
5. Permissions: tạo Role `EventBridgeSchedulerECSRole` (Custom trust policy cho `scheduler.amazonaws.com`, policy cho phép `ecs:RunTask` và `iam:PassRole`).
   * **Kết quả**: Schedule ở trạng thái Enabled, tự động chạy backup lúc 2:00 sáng hàng ngày.

   ![EventBridge Scheduler wordpress-daily-backup ở trạng thái Enabled](/images/5/5.7.4/03-eventbridge-scheduler.png?classes=border,shadow)
