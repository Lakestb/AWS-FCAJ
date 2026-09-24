---
title : "CloudWatch Dashboard & Alarm"
date : "2024-05-15"
weight : 1
chapter : false
pre : " <b> 5.4.1. </b> "
---

1. Navigate to **CloudWatch** → **Dashboards** → **Create dashboard**, name it `WordPress-Production-Dashboard`.
2. Add monitoring widgets for EC2 `CPUUtilization` and RDS `DatabaseConnections`.

   ![CloudWatch Dashboard monitoring EC2 and RDS metrics](/images/5/5.4.1/01-cloudwatch-dashboard.png?classes=border,shadow)

3. Navigate to **Alarms** → **Create alarm**, select EC2 `CPUUtilization` metric, threshold >= 80%, name it `EC2-High-CPU-Utilization`.

   ![CloudWatch Alarm configuration for EC2 CPU threshold](/images/5/5.4.1/02-cloudwatch-alarm.png?classes=border,shadow)
