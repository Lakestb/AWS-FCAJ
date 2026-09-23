---
title : "Hạ tầng mạng (VPC, Subnet, IGW)"
date : "2024-05-15"
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

### 5.2. Hạ tầng mạng (Networking): VPC, Subnet, Internet Gateway

#### 5.2.1. Khởi tạo VPC
* **VPC**: `my-project-vpc` (`vpc-0b489eb298393e445`), CIDR `10.0.0.0/16`.

#### 5.2.2. Thiết kế Subnet theo mô hình đa tầng (Multi-Tier)
* **Public Subnet 1**: `subnet-011686e77c0d42601` — `10.0.0.0/20` — `ap-southeast-1a` (chứa EC2, sau này chứa cả ALB/ECS Task).
* **Public Subnet 2**: `subnet-037a8c50b5e7ec755` — `10.0.16.0/20` — `ap-southeast-1b` (dùng cho ALB, đảm bảo yêu cầu tối thiểu 2 AZ).
* **Private Subnet 1**: `subnet-008f0d773c67a3970` — `10.0.128.0/20` — `ap-southeast-1a` (chứa RDS).
* **Private Subnet 2**: `subnet-0a953901b7b370b78` — `10.0.144.0/20` — `ap-southeast-1b` (DB Subnet Group, dự phòng Multi-AZ).

> 📷 **Ảnh minh chứng**: Bảng danh sách Subnet trong VPC Console, thể hiện đủ CIDR và AZ như trên.

#### 5.2.3. Internet Gateway & Route Table
* Internet Gateway gắn vào VPC, Route Table của Public Subnet có tuyến `0.0.0.0/0` trỏ tới IGW.
* Route Table của Private Subnet chỉ có tuyến `local`, không có đường ra Internet — cô lập tầng Database.

> 📷 **Ảnh minh chứng**: Route Table của Public Subnet (có route tới IGW) và Private Subnet (chỉ có local route).

#### 5.2.4. Security Groups
* **`ec2-web-sg`** (`sg-043b5223abc256608`): mở HTTP (80) từ `0.0.0.0/0`, HTTPS (443) từ `0.0.0.0/0`, SSH (22) chỉ cho phép từ IP quản trị cá nhân (`/32`) — không mở SSH cho toàn Internet.
* **`RDS-SG`**: chỉ cho phép port 3306 từ nguồn là chính `ec2-web-sg` (không mở theo IP tĩnh).

> 📷 **Ảnh minh chứng**: Cấu hình Inbound rules của `ec2-web-sg` (đặc biệt rule SSH giới hạn theo IP) và `RDS-SG`.
