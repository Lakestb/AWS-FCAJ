---
title : "IAM Role cho EC2 (Least Privilege)"
date : "2024-05-15"
weight : 3
chapter : false
pre : " <b> 5.3.3. </b> "
---

1. Vào **IAM** → **Roles** → **Create role**, Trusted entity: AWS service → **EC2**.
2. Gắn policy cho phép `s3:PutObject`, `s3:GetObject`, `s3:ListBucket` trên đúng bucket S3 sẽ tạo ở bước sau.

   ![Cấu hình Policy IAM Least Privilege cho S3](/images/5/5.3.3/01-iam-role.png?classes=border,shadow)

3. Đặt tên role, quay lại EC2 → **Actions** → **Security** → **Modify IAM role**, gắn role vừa tạo vào instance.

   ![IAM Role đã gắn vào EC2 Instance](/images/5/5.3.3/02-iam-role-attached.png?classes=border,shadow)
