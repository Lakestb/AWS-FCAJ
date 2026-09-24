---
title : "Manual Run & EventBridge Scheduler"
date : "2024-05-15"
weight : 4
chapter : false
pre : " <b> 5.7.4. </b> "
---

1. Manual test execution: **Task definitions** → `wordpress-backup-task` → **Deploy** → **Run task**, select cluster, Fargate launch type, 1 Public Subnet, Security group `ec2-web-sg`, Public IP: Turned on.
2. Inspect CloudWatch Logs (`/ecs/wordpress-backup-task`) and S3 bucket to verify successful run (Exit code 0).

   ![ECS Fargate task completed successfully with Exit code 0](/images/5/5.7.4/01-ecs-run-task-success.png?classes=border,shadow)

   ![Compressed database backup archive persisted on S3 Bucket](/images/5/5.7.4/02-s3-backup-file.png?classes=border,shadow)

3. Navigate to **EventBridge** → **Scheduler** → **Create schedule**, name `wordpress-daily-backup`, Recurring schedule, Cron-based: `0 2 * * ? *`.
4. Target: Templated targets → **Amazon ECS RunTask**, select cluster/task definition, configure matching network settings.
5. Permissions: create Role `EventBridgeSchedulerECSRole` (trust policy for `scheduler.amazonaws.com`, granting `ecs:RunTask` and `iam:PassRole`).
   * **Result**: Schedule set to Enabled, automating backup executions at 02:00 AM daily.

   ![EventBridge Scheduler schedule enabled and active](/images/5/5.7.4/03-eventbridge-scheduler.png?classes=border,shadow)
