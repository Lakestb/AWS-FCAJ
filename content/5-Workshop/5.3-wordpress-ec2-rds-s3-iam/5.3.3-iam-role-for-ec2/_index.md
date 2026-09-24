---
title : "IAM Role for EC2 (Least Privilege)"
date : "2024-05-15"
weight : 3
chapter : false
pre : " <b> 5.3.3. </b> "
---

1. Navigate to **IAM** → **Roles** → **Create role**, Trusted entity: AWS service → **EC2**.
2. Attach policy granting `s3:PutObject`, `s3:GetObject`, `s3:ListBucket` strictly scoped to the S3 bucket created next.

   ![Least Privilege IAM Policy configuration for S3](/images/5/5.3.3/01-iam-role.png?classes=border,shadow)

3. Name the role, return to EC2 → **Actions** → **Security** → **Modify IAM role**, attach the created role to instance.

   ![IAM Role attached to EC2 instance](/images/5/5.3.3/02-iam-role-attached.png?classes=border,shadow)
