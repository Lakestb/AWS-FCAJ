---
title : "Amazon S3 & Offload Media"
date : "2024-05-15"
weight : 4
chapter : false
pre : " <b> 5.3.4. </b> "
---

1. Navigate to **S3** → **Create bucket**, name it `my-portfolio-blog-media-635176221447-ap-southeast-1-an`.
2. In WordPress, install **WP Offload Media Lite** plugin, configure target bucket, authenticated via IAM Role (without hardcoding Access Keys).

   ![WP Offload Media Lite configuration using IAM Role](/images/5/5.3.4/01-s3-offload-media.png?classes=border,shadow)

   ![S3 Bucket storing media offloaded from WordPress](/images/5/5.3.4/02-s3-bucket-media.png?classes=border,shadow)
