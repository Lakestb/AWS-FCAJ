---
title : "Khả dụng cao: ALB & Auto Scaling"
date : "2024-05-15"
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

### 5.6. Khả dụng cao: Application Load Balancer & Auto Scaling

#### 5.6.1. Đóng gói EC2 hiện tại thành AMI
* **AMI**: `wordpress-app-ami-v1`, tạo từ EC2 WordPress đang chạy ổn định.

> 📷 **Ảnh minh chứng**: Trạng thái AMI chuyển sang Available trong EC2 → AMIs.

#### 5.6.2. Launch Template
* **Template**: `wordpress-launch-template` — dùng AMI trên, instance type `t3.micro`, Security Group `ec2-web-sg`, key pair `my-ec2-key`.

> 📷 **Ảnh minh chứng**: Chi tiết cấu hình Launch Template.

#### 5.6.3. Application Load Balancer & Target Group
* **ALB**: `wordpress-alb`, Internet-facing, 2 Availability Zones (Public Subnet 1 & 2).
* **Target Group**: `wordpress-tg`, HTTP:80, Health check path `/`, ngưỡng 5 lần thành công/thất bại liên tiếp, interval 30s.

> 📷 **Ảnh minh chứng**: DNS name của ALB và cấu hình Target Group/Health check.

#### 5.6.4. Auto Scaling Group
* **ASG**: `wordpress-asg`, Desired = 1, Min = 1, Max = 2.
* **Scaling Policy**: Target tracking theo Average CPU Utilization, ngưỡng 70%.
* **Health check type**: EC2, ELB — kết hợp cả kiểm tra trạng thái máy ảo lẫn kết quả Health Check từ Target Group.

> 📷 **Ảnh minh chứng**: Cấu hình Desired/Min/Max và Scaling Policy của ASG.

#### 5.6.5. Kiểm thử và xử lý sự cố thực tế
Trong quá trình kiểm thử, phát hiện Target Group liên tục báo 0 target dù instance đã ở trạng thái Healthy trong ASG. Qua kiểm tra Activity History, Instance Management và đối chiếu cấu hình, xác định nguyên nhân: ASG được tạo ra nhưng thiếu bước gắn Target Group (mục Load balancing trong tab Integrations của ASG để trống). Khắc phục bằng cách vào ASG → Integrations → Edit → gắn đúng Target Group `wordpress-tg`, sau đó instance được tự động đăng ký và chuyển sang trạng thái Healthy.

> 📷 **Ảnh minh chứng**: Target Group trước khi sửa (0 targets) và sau khi sửa (1 Healthy), cùng ảnh trang web WordPress truy cập thành công qua DNS của ALB.
