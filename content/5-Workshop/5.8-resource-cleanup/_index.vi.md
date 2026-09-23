---
title : "Dọn dẹp tài nguyên (Resource Cleanup)"
date : "2024-05-15"
weight : 8
chapter : false
pre : " <b> 5.8. </b> "
---

### 5.8. Dọn dẹp tài nguyên (Resource Cleanup)

Thực hiện sau khi đã hoàn tất chụp đầy đủ minh chứng và được xác nhận đã chấm điểm, nhằm tránh phát sinh chi phí duy trì không cần thiết trên tài khoản AWS. Thứ tự xóa đi theo chiều ngược lại với thứ tự tạo (mục 5.7 → 5.1), đảm bảo không xóa nhầm tài nguyên đang được tài nguyên khác phụ thuộc.

#### 5.8.1. Xóa EventBridge Scheduler
* Xóa Schedule `wordpress-daily-backup` trước tiên, để không còn tác vụ nào tự động kích hoạt ECS trong lúc dọn dẹp các bước sau.

#### 5.8.2. Xóa ECS Task Definition, Cluster và ECR Repository
* Deregister Task Definition `wordpress-backup-task`.
* Xóa Cluster `wordpress-cluster` (Fargate không có instance nền tảng cần tắt riêng).
* Xóa Repository `wordpress-backup` trên ECR (xóa toàn bộ image bên trong trước hoặc dùng tùy chọn force-delete).

#### 5.8.3. Xóa hạ tầng High Availability
* Xóa Auto Scaling Group `wordpress-asg` (đặt Desired=0 trước, đợi terminate hết instance, rồi xóa ASG).
* Xóa Application Load Balancer `wordpress-alb` và Target Group `wordpress-tg`.
* Xóa Launch Template `wordpress-launch-template` và AMI `wordpress-app-ami-v1` (kèm Snapshot EBS liên quan để tránh phí lưu trữ dư).

#### 5.8.4. Xóa hạ tầng Serverless
* Xóa API Gateway `GuestbookAPI`.
* Xóa Lambda Function `GuestbookHandler`.
* Xóa bảng DynamoDB `GuestbookMessages`.
* Xóa SNS Topic `guestbook-new-message` (nếu có sử dụng).

#### 5.8.5. Xóa cấu hình Giám sát
* Xóa CloudWatch Alarm `EC2-High-CPU-Utilization` và Dashboard `WordPress-Production-Dashboard`.
* Xóa SNS Topic `ec2-high-cpu-alert`.
* Log group CloudTrail Event History không cần xóa thủ công (không phát sinh phí, tự hết hạn theo policy 90 ngày).

#### 5.8.6. Xóa Database
* Tạo Final Snapshot của RDS `wordpress-db` trước khi xóa (nếu muốn lưu trữ dữ liệu tham khảo sau này).
* Xóa RDS Instance `wordpress-db`.

#### 5.8.7. Xóa Compute & Storage
* Terminate toàn bộ EC2 Instance còn lại (cả bản gốc đã Stop và bản do ASG tạo nếu còn sót).
* Xóa Security Groups `ec2-web-sg`, `RDS-SG`, `ALB-SG` (sau khi không còn tài nguyên nào tham chiếu tới).
* Làm rỗng và xóa Bucket S3 `my-portfolio-blog-media-...` (nếu không cần giữ lại dữ liệu backup/media).

#### 5.8.8. Xóa hạ tầng mạng (VPC)
* Xóa Subnet (2 Public, 2 Private), Route Table, Internet Gateway.
* Xóa VPC `my-project-vpc`.

#### 5.8.9. Xóa IAM Roles & Policies (thực hiện cuối cùng)
* Xóa lần lượt: `EventBridgeSchedulerECSRole`, `ecsTaskExecutionRole`, `EcsBackupTaskRole`, `GuestbookLambdaRole`, IAM Role gắn cho EC2.
* Xóa các Custom Policy tương ứng: `EventBridgeSchedulerEcsPolicy`, `EcsBackupTaskPolicy`, `GuestbookLambdaPolicy`.

> ⚠️ **Lưu ý**: Chỉ xóa IAM Role/Policy sau khi chắc chắn không còn tài nguyên nào (Lambda, ECS Task, EC2...) đang tham chiếu tới, để tránh lỗi phụ thuộc.
