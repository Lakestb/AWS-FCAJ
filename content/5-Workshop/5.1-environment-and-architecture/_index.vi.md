---
title : "Chuẩn bị môi trường & Kiến trúc tổng quan"
date : "2024-05-15"
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

### 5.1. Chuẩn bị môi trường & Kiến trúc tổng quan

#### 5.1.1. Lựa chọn Region và khởi tạo tài khoản thực hành
* **Region sử dụng xuyên suốt dự án**: Asia Pacific (Singapore) — `ap-southeast-1`.
* **Tài khoản IAM sử dụng để thao tác**: `cloud-admin` (không dùng tài khoản root cho các thao tác hàng ngày).

> 📷 **Ảnh minh chứng**: Ảnh chọn Region trên Console và thông tin tài khoản IAM đang đăng nhập.

#### 5.1.2. Kiến trúc tổng thể sau khi hoàn thiện
Hệ thống được xây dựng dần theo hướng kết hợp giữa kiến trúc truyền thống (2-Tier: EC2 + RDS) và các thành phần hiện đại (Serverless, Load Balancing, Container hóa), gồm 4 nhóm chính:
* **Compute & Database**: EC2 (WordPress) + RDS (MySQL) + S3 (lưu trữ media/backup).
* **High Availability**: Application Load Balancer + Auto Scaling Group.
* **Serverless Backend**: Lambda + API Gateway + DynamoDB (tính năng Guestbook).
* **Automation & Container**: Docker + ECS Fargate + EventBridge Scheduler (tự động backup).

> 📷 **Ảnh minh chứng**: Sơ đồ kiến trúc tổng thể cuối cùng (vẽ bằng draw.io, thể hiện đủ 4 nhóm trên).
