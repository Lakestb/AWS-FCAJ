---
title : "Security Groups"
date : "2024-05-15"
weight : 4
chapter : false
pre : " <b> 5.2.4. </b> "
---

1. Tạo Security Group `ec2-web-sg`: Inbound cho phép HTTP (80) từ `0.0.0.0/0`, HTTPS (443) từ `0.0.0.0/0`, SSH (22) chỉ từ IP quản trị cá nhân (`/32`).

   ![Cấu hình Inbound rules cho ec2-web-sg](/images/5/5.2.4/01-sg-ec2-web.png?classes=border,shadow)

2. Tạo Security Group `RDS-SG`: Inbound chỉ cho phép MySQL/Aurora (3306) với Source là chính `ec2-web-sg`.

   ![Cấu hình Inbound rules cho RDS-SG](/images/5/5.2.4/02-sg-rds.png?classes=border,shadow)
