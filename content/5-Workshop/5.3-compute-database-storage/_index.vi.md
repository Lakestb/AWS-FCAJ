---
title : "Nền tảng Compute, Database & Storage"
date : "2024-05-15"
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

### 5.3. Nền tảng Compute, Database & Storage: EC2, RDS, S3, IAM

#### 5.3.1. Web/Application Tier (Amazon EC2)
* **Hệ điều hành**: Ubuntu Server 24.04 LTS, **Instance type**: `t3.micro` (Free Tier).
* **Tech stack LAMP**: Apache 2.4, PHP 8.3, WordPress (CMS).
* **IAM Role** gắn vào EC2 Instance Profile để truy cập S3 mà không cần lưu Access Key trong code/file cấu hình.

> 📷 **Ảnh minh chứng**: Giao diện WordPress chạy thành công qua IP công khai của EC2.

#### 5.3.2. Database Tier (Amazon RDS for MySQL)
* **Engine**: MySQL Community (Managed), **Instance class**: `db.t4g.micro` (Free Tier).
* **Endpoint**: `wordpress-db.cnwgwiseq95o.ap-southeast-1.rds.amazonaws.com`, **Database name**: `wordpress`.
* Đặt trong Private Subnet, không cấp Public IP, chỉ nhận kết nối từ `ec2-web-sg`.

> 📷 **Ảnh minh chứng**: Trang Configuration/Connectivity của RDS thể hiện endpoint và trạng thái Available.

#### 5.3.3. Lưu trữ tài nguyên tĩnh (Amazon S3)
* **Bucket**: `my-portfolio-blog-media-635176221447-ap-southeast-1-an`.
* Tích hợp qua plugin WP Offload Media Lite, ảnh upload từ WordPress tự động đồng bộ lên S3.

> 📷 **Ảnh minh chứng**: Nội dung bucket S3 với các file media đã upload từ WordPress.

#### 5.3.4. Bảo mật quyền truy cập (IAM)
* IAM Role gắn cho EC2 tuân thủ nguyên tắc Least Privilege, tránh dùng chính sách quyền rộng không cần thiết.

> 📷 **Ảnh minh chứng**: Chính sách IAM Role gắn cho EC2 (Permissions tab).
