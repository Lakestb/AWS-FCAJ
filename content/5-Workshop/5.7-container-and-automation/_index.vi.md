---
title : "Container hóa & Tự động hóa: Docker, ECS, EventBridge"
date : "2024-05-15"
weight : 7
chapter : false
pre : " <b> 5.7. </b> "
---

### 5.7. Container hóa & Tự động hóa: Docker, ECS Fargate, EventBridge Scheduler

Tách logic sao lưu cơ sở dữ liệu (trước đây chạy bằng cron trên EC2) thành một tác vụ độc lập, đóng gói bằng Docker và chạy theo lịch trên ECS Fargate — không phụ thuộc vòng đời của EC2.

#### 5.7.1. Đóng gói Docker Image
* **Base image**: `debian:bookworm-slim`, cài đặt `default-mysql-client`, `awscli`, `gzip`.
* **Script `backup_db.sh`**: đọc cấu hình qua biến môi trường (`DB_HOST`, `DB_USER`, `DB_PASSWORD`, `DB_NAME`, `S3_BUCKET`) — không hardcode thông tin nhạy cảm trong code.

> 📷 **Ảnh minh chứng**: Dockerfile và kết quả `docker build` chạy thành công.

#### 5.7.2. Đẩy Image lên Amazon ECR
* **Repository**: `wordpress-backup`.

```bash
aws ecr get-login-password | docker login --username AWS --password-stdin <account>.dkr.ecr.ap-southeast-1.amazonaws.com
docker build -t wordpress-backup .
docker tag wordpress-backup:latest <account>.dkr.ecr.ap-southeast-1.amazonaws.com/wordpress-backup:latest
docker push <account>.dkr.ecr.ap-southeast-1.amazonaws.com/wordpress-backup:latest
```

> 📷 **Ảnh minh chứng**: Repository wordpress-backup trên ECR Console với image tag latest.

#### 5.7.3. IAM Roles cho ECS Task
* **`ecsTaskExecutionRole`**: gắn policy có sẵn `AmazonECSTaskExecutionRolePolicy`, cho phép kéo image từ ECR và ghi log.
* **`EcsBackupTaskRole`**: gắn policy tự viết `EcsBackupTaskPolicy`, chỉ cho phép `s3:PutObject` vào đúng thư mục `backups/` của bucket — nguyên tắc Least Privilege.

> 📷 **Ảnh minh chứng**: 2 IAM Role và policy đã gắn.

#### 5.7.4. ECS Cluster & Task Definition
* **Cluster**: `wordpress-cluster` (AWS Fargate — serverless, không cần quản lý máy chủ).
* **Task Definition**: `wordpress-backup-task`, 0.25 vCPU / 0.5 GB, container `backup-container`, image lấy từ ECR.
* **Biến môi trường**: `DB_HOST`, `DB_USER`, `DB_PASSWORD`, `DB_NAME`, `S3_BUCKET` — cấu hình trực tiếp trong Task Definition, tách biệt khỏi source code.

> 📷 **Ảnh minh chứng**: Cấu hình Task Definition, đặc biệt phần Environment variables (che mờ giá trị mật khẩu khi chụp ảnh).

#### 5.7.5. Kiểm thử thủ công và xử lý sự cố
Lần chạy thử đầu tiên thất bại với Exit code 7, log CloudWatch ghi rõ lỗi: `mysqldump: unknown variable 'set-gtid-purged=OFF'`. Nguyên nhân: gói `default-mysql-client` trên Debian cài đặt MariaDB client, vốn không hỗ trợ tùy chọn `--set-gtid-purged` đặc thù của MySQL. Khắc phục bằng cách loại bỏ tùy chọn này khỏi script (không cần thiết cho một tác vụ backup đơn giản, không dùng replication), build lại image, đẩy lại lên ECR. Lần chạy thử thứ hai cho kết quả Exit code 0 — thành công.

> 📷 **Ảnh minh chứng**: Task chạy lỗi (Exit code 7, log lỗi mysqldump) và Task chạy thành công sau khi sửa (Exit code 0), cùng file backup mới xuất hiện trên S3.

#### 5.7.6. Lên lịch tự động với Amazon EventBridge Scheduler
* **Schedule**: `wordpress-daily-backup`, Cron: `0 2 * * ? *` (2:00 sáng hàng ngày, giờ Việt Nam).
* **Target**: ECS RunTask trên `wordpress-cluster` / `wordpress-backup-task`, mạng: Public Subnet 1, Security Group `ec2-web-sg`, Auto-assign Public IP: Enabled.
* **Execution Role riêng**: `EventBridgeSchedulerECSRole` (Custom trust policy cho `scheduler.amazonaws.com`, gắn policy `EventBridgeSchedulerEcsPolicy` cho phép `ecs:RunTask` và `iam:PassRole` trên 2 Role ở mục 5.7.3).
* Đã kiểm thử bằng cách tạm đổi giờ chạy sang thời điểm gần, xác nhận Task tự động xuất hiện trong ECS (cột Started by ghi `scheduler.amazonaws.com`) và chạy thành công, trước khi đổi lại đúng lịch 2h sáng.

> 📷 **Ảnh minh chứng**: Schedule ở trạng thái Enabled, và Task được khởi chạy tự động bởi Scheduler (cột Started by).
