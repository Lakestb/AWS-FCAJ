---
title : "Amazon S3 & Offload Media"
date : "2024-05-15"
weight : 4
chapter : false
pre : " <b> 5.3.4. </b> "
---

1. Vào **S3** → **Create bucket**, đặt tên `my-portfolio-blog-media-635176221447-ap-southeast-1-an`.
2. Trên WordPress, cài plugin **WP Offload Media Lite**, cấu hình trỏ tới bucket vừa tạo, xác thực qua IAM Role (không nhập Access Key).

   ![Cấu hình plugin WP Offload Media Lite kết nối S3 qua IAM Role](/images/5/5.3.4/01-s3-offload-media.png?classes=border,shadow)

   ![Bucket S3 chứa media upload từ WordPress](/images/5/5.3.4/02-s3-bucket-media.png?classes=border,shadow)
