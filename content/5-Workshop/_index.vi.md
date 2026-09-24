---
title : "Workshop"
date : "2024-05-15"
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

### Triển khai WordPress Portfolio Blog toàn diện trên AWS

Tài liệu này ghi lại toàn bộ quá trình triển khai dự án theo đúng trình tự thời gian thực hiện, từ bước chuẩn bị hạ tầng ban đầu đến khi hoàn thiện đầy đủ các dịch vụ AWS đã học. Mỗi mục có ghi chú vị trí cần chèn ảnh minh chứng (📷) — người thực hiện tự chụp và chèn ảnh tương ứng vào đúng vị trí khi hoàn thiện báo cáo cuối cùng.

---

### Danh sách các nội dung thực hành:

1. [**5.1. Chuẩn bị môi trường & Chọn Region**](5.1-environment-and-region/)
2. [**5.2. Hạ tầng mạng (VPC, Subnet, Internet Gateway)**](5.2-networking-vpc/)
   * [5.2.1. Khởi tạo VPC](5.2-networking-vpc/5.2.1-create-vpc/)
   * [5.2.2. Tạo 4 Subnet](5.2-networking-vpc/5.2.2-create-subnets/)
   * [5.2.3. Internet Gateway & Route Table](5.2-networking-vpc/5.2.3-internet-gateway-route-table/)
   * [5.2.4. Security Groups](5.2-networking-vpc/5.2.4-security-groups/)
3. [**5.3. Triển khai WordPress: EC2, RDS, S3, IAM**](5.3-wordpress-ec2-rds-s3-iam/)
   * [5.3.1. Khởi tạo Amazon RDS for MySQL](5.3-wordpress-ec2-rds-s3-iam/5.3.1-create-rds-mysql/)
   * [5.3.2. Khởi tạo EC2 và cài đặt WordPress](5.3-wordpress-ec2-rds-s3-iam/5.3.2-create-ec2-install-wordpress/)
   * [5.3.3. IAM Role cho EC2 (Least Privilege)](5.3-wordpress-ec2-rds-s3-iam/5.3.3-iam-role-for-ec2/)
   * [5.3.4. Amazon S3 & Offload Media](5.3-wordpress-ec2-rds-s3-iam/5.3.4-s3-offload-media/)
4. [**5.4. Giám sát & Kiểm toán: CloudWatch, SNS, CloudTrail**](5.4-monitoring-cloudwatch-sns-cloudtrail/)
   * [5.4.1. CloudWatch Dashboard & Alarm](5.4-monitoring-cloudwatch-sns-cloudtrail/5.4.1-cloudwatch-dashboard-alarm/)
   * [5.4.2. Amazon SNS](5.4-monitoring-cloudwatch-sns-cloudtrail/5.4.2-amazon-sns/)
   * [5.4.3. AWS CloudTrail](5.4-monitoring-cloudwatch-sns-cloudtrail/5.4.3-aws-cloudtrail/)
5. [**5.5. Serverless Backend: Lambda, API Gateway, DynamoDB**](5.5-serverless-backend/)
   * [5.5.1. Khởi tạo bảng DynamoDB](5.5-serverless-backend/5.5.1-create-dynamodb-table/)
   * [5.5.2. IAM Role & Hàm AWS Lambda](5.5-serverless-backend/5.5.2-iam-role-lambda-function/)
   * [5.5.3. Amazon API Gateway (REST API)](5.5-serverless-backend/5.5.3-api-gateway-rest-api/)
   * [5.5.4. Nhúng Form vào WordPress](5.5-serverless-backend/5.5.4-embed-form-wordpress/)
6. [**5.6. Khả dụng cao: Load Balancer & Auto Scaling**](5.6-high-availability-alb-asg/)
   * [5.6.1. Đóng gói EC2 thành AMI](5.6-high-availability-alb-asg/5.6.1-package-ec2-to-ami/)
   * [5.6.2. Launch Template](5.6-high-availability-alb-asg/5.6.2-launch-template/)
   * [5.6.3. Application Load Balancer & Target Group](5.6-high-availability-alb-asg/5.6.3-alb-target-group/)
   * [5.6.4. Auto Scaling Group](5.6-high-availability-alb-asg/5.6.4-auto-scaling-group/)
7. [**5.7. Container hóa & Tự động hóa: Docker, ECS Fargate, EventBridge**](5.7-container-ecs-eventbridge/)
   * [5.7.1. Đóng gói Docker Image](5.7-container-ecs-eventbridge/5.7.1-docker-image-packaging/)
   * [5.7.2. Đẩy Image lên Amazon ECR](5.7-container-ecs-eventbridge/5.7.2-push-image-to-ecr/)
   * [5.7.3. IAM Roles & ECS Task Definition](5.7-container-ecs-eventbridge/5.7.3-iam-roles-ecs-task-definition/)
   * [5.7.4. Chạy thử và Amazon EventBridge Scheduler](5.7-container-ecs-eventbridge/5.7.4-manual-test-eventbridge-scheduler/)
8. [**5.8. Dọn dẹp tài nguyên**](5.8-resource-cleanup/)
   * [5.8.1. Xóa EventBridge Scheduler & ECS](5.8-resource-cleanup/5.8.1-delete-eventbridge-ecs/)
   * [5.8.2. Xóa hạ tầng Khả dụng cao](5.8-resource-cleanup/5.8.2-delete-high-availability/)
   * [5.8.3. Xóa hạ tầng Serverless](5.8-resource-cleanup/5.8.3-delete-serverless/)
   * [5.8.4. Xóa cấu hình Giám sát](5.8-resource-cleanup/5.8.4-delete-monitoring/)
   * [5.8.5. Xóa Database, Compute & Storage](5.8-resource-cleanup/5.8.5-delete-database-compute-storage/)
   * [5.8.6. Xóa hạ tầng mạng & IAM](5.8-resource-cleanup/5.8.6-delete-networking-iam/)
