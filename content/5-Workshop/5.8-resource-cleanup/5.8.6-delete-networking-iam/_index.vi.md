---
title : "Xóa hạ tầng mạng & IAM"
date : "2024-05-15"
weight : 6
chapter : false
pre : " <b> 5.8.6. </b> "
---

1. Xóa Security Groups (`ec2-web-sg`, `RDS-SG`).
2. Xóa 4 Subnet, Route Table, Internet Gateway, sau đó xóa VPC `my-project-vpc`.
3. Cuối cùng, xóa toàn bộ IAM Role và Policy đã tạo (`EventBridgeSchedulerECSRole`, `ecsTaskExecutionRole`, `EcsBackupTaskRole`, `GuestbookLambdaRole`, Role gắn cho EC2) sau khi chắc chắn không còn tài nguyên nào tham chiếu tới.
