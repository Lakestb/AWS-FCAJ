---
title : "CloudWatch Dashboard & Alarm"
date : "2024-05-15"
weight : 1
chapter : false
pre : " <b> 5.4.1. </b> "
---

1. Vào **CloudWatch** → **Dashboards** → **Create dashboard**, đặt tên `WordPress-Production-Dashboard`.
2. Thêm widget theo dõi `CPUUtilization` của EC2 và `DatabaseConnections` của RDS.

   ![CloudWatch Dashboard theo dõi metrics EC2 và RDS](/images/5/5.4.1/01-cloudwatch-dashboard.png?classes=border,shadow)

3. Vào **Alarms** → **Create alarm**, chọn metric `CPUUtilization` của EC2, ngưỡng >= 80%, đặt tên `EC2-High-CPU-Utilization`.

   ![Cấu hình CloudWatch Alarm EC2-High-CPU-Utilization](/images/5/5.4.1/02-cloudwatch-alarm.png?classes=border,shadow)
