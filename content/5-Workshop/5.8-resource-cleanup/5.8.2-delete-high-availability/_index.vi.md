---
title : "Xóa hạ tầng Khả dụng cao"
date : "2024-05-15"
weight : 2
chapter : false
pre : " <b> 5.8.2. </b> "
---

1. Đặt Desired = 0 cho ASG `wordpress-asg`, đợi terminate hết instance, rồi xóa ASG.
2. Xóa Load Balancer `wordpress-alb` và Target Group `wordpress-tg`.
3. Xóa Launch Template `wordpress-launch-template` và AMI `wordpress-app-ami-v1` (kèm Snapshot liên quan).
