---
title : "Chuẩn bị môi trường & Chọn Region"
date : "2024-05-15"
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

1. Đăng nhập AWS Console bằng tài khoản IAM `cloud-admin` (không dùng tài khoản root cho thao tác hàng ngày).

   ![Đăng nhập tài khoản IAM cloud-admin](/images/5/5.1/01-iam-signin.png?classes=border,shadow)

2. Tại góc trên phải Console, chọn Region Asia Pacific (Singapore) — `ap-southeast-1`.
3. Tạo Key Pair mới: vào **EC2** → **Key Pairs** → **Create key pair**, đặt tên `my-ec2-key`, định dạng `.pem`, tải file về máy để dùng SSH sau này.

   ![Tạo EC2 Key Pair my-ec2-key](/images/5/5.1/02-create-keypair.png?classes=border,shadow)
