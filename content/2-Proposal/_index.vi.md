---
title : "Bản đề xuất"
date : "2024-05-15"
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

### Đề xuất Dự án: Hạ tầng WordPress toàn diện trên AWS: Từ 2-Tier đến Serverless, High Availability và Container hóa

---

### 1. Tóm tắt điều hành

Đề xuất này trình bày giải pháp hiện đại hóa hệ thống web WordPress trên nền tảng AWS. Thay vì triển khai đơn khối (all-in-one) trên một máy chủ duy nhất gây rủi ro mất an toàn thông tin và gián đoạn dịch vụ, dự án xây dựng hạ tầng phân tầng theo chuẩn AWS Well-Architected:

* **Tách biệt dữ liệu & lưu trữ (Decoupled 2-Tier)**: Tách web server (EC2) khỏi cơ sở dữ liệu (RDS MySQL) và đẩy toàn bộ media tĩnh lên Amazon S3.
* **Mở rộng linh hoạt (High Availability)**: Thiết lập Application Load Balancer (ALB) và Auto Scaling Group (ASG) để tự động cân bằng tải và co giãn theo nhu cầu.
* **Backend Serverless**: Xây dựng tính năng Guestbook độc lập chạy bằng API Gateway, Lambda và DynamoDB.
* **Tự động hóa bằng Container**: Đóng gói tác vụ sao lưu định kỳ bằng Docker, chạy serverless trên ECS Fargate qua EventBridge Scheduler thay thế cron truyền thống trên EC2.

---

### 2. Tuyên bố vấn đề

#### Vấn đề hiện tại
* **Đơn điểm lỗi (SPOF)**: Chạy cả web server và database trên cùng một máy chủ khiến hệ thống sập toàn bộ nếu ứng dụng gặp sự cố tràn RAM hoặc nghẽn CPU.
* **Rủi ro bảo mật**: Cổng cơ sở dữ liệu và SSH thường mở rộng ra ngoài Internet; lưu trữ access key tĩnh trong mã nguồn tiềm ẩn nguy cơ lộ credential.
* **Thiếu khả năng tự động co giãn**: Máy chủ đơn lẻ không thể tự mở rộng khi lượng truy cập tăng vọt, gây nghẽn mạng hoặc chết dịch vụ.
* **Sao lưu phụ thuộc cục bộ**: Tác vụ backup chạy bằng cron job trên chính EC2; nếu instance bị lỗi hoặc bị xóa, quy trình sao lưu và dữ liệu backup cục bộ cũng biến mất.

#### Giải pháp đề xuất
Hệ thống kết hợp giữa mô hình phân tầng truyền thống và các công nghệ Serverless / Container hiện đại:
* **Flow Core (2-Tier & Storage)**: Tách web server sang EC2 (Public Subnet) và database sang RDS (Private Subnet); dùng IAM Role để phân quyền đọc/ghi S3 không cần access key.
* **Flow HA (Load Balancing & Auto Scaling)**: ALB phân phối lưu lượng vào Auto Scaling Group; tự động tăng giảm instance theo ngưỡng CPU.
* **Flow Serverless (Guestbook Service)**: Tách module gửi phản hồi khách hàng ra một backend phi máy chủ độc lập (API Gateway → Lambda → DynamoDB).
* **Flow Container (Automated Scheduled Backup)**: Container hóa script backup database bằng Docker, lưu trên Amazon ECR, chạy tự động theo lịch trên ECS Fargate kích hoạt bởi EventBridge.

---

### 3. Kiến trúc giải pháp

#### Sơ đồ kiến trúc tổng thể
![Sơ đồ kiến trúc tổng thể](/images/2/architecture.png?classes=border,shadow)

#### Chi tiết 4 luồng xử lý chính trong kiến trúc:

1. **Flow Web & Decoupled Data (EC2 + RDS + S3)**
   * Người dùng truy cập WordPress qua IP/DNS của Web Server trên EC2.
   * EC2 đọc/ghi dữ liệu có cấu trúc sang Amazon RDS MySQL đặt cô lập trong Private Subnet qua cổng 3306.
   * Toàn bộ media và ảnh tải lên được plugin đồng bộ trực tiếp lên Amazon S3 qua IAM Instance Profile.

2. **Flow High Availability (ALB + ASG)**
   * Application Load Balancer tiếp nhận lưu lượng HTTP/HTTPS tại tầng biên công khai, phân phối đều tới các instance EC2 trong Target Group.
   * Auto Scaling Group tự động thay thế instance lỗi thông qua Health Check và tự động kích hoạt tạo thêm máy chủ khi CPU trung bình vượt ngưỡng 70%.

3. **Flow Serverless Guestbook (API Gateway + Lambda + DynamoDB)**
   * Giao diện form nhúng trên WordPress gửi request POST tới Amazon API Gateway.
   * API Gateway kích hoạt AWS Lambda (Python 3.12) để xác thực dữ liệu và ghi bản ghi vào bảng DynamoDB.
   * Lambda phát thông báo email tức thời qua Amazon SNS khi có lời nhắn mới.

4. **Flow Containerized Scheduled Backup (Docker + ECS Fargate + EventBridge)**
   * Amazon EventBridge Scheduler kích hoạt tác vụ sao lưu vào 02:00 AM hàng ngày.
   * ECS Fargate kéo Docker Image từ Amazon ECR, khởi chạy container thực thi tác vụ dump dữ liệu từ RDS, nén tệp và tải lên thư mục `backups/` trên S3.

#### Dịch vụ AWS sử dụng
* **Amazon VPC**: Phân chia mạng cô lập với 2 Public Subnets và 2 Private Subnets trên 2 AZs.
* **Amazon EC2 & Auto Scaling**: Cung cấp năng lực tính toán linh hoạt.
* **Amazon RDS (MySQL)**: Quản trị cơ sở dữ liệu quan hệ độc lập.
* **Amazon S3**: Lưu trữ đối tượng phân tán cho media và các bản backup.
* **Application Load Balancer**: Cân bằng tải ứng dụng đa vùng.
* **API Gateway, Lambda, DynamoDB**: Xây dựng backend serverless cho form phản hồi.
* **Amazon ECR & ECS Fargate**: Lưu trữ image và vận hành container không máy chủ.
* **CloudWatch, SNS & CloudTrail**: Giám sát chỉ số, cảnh báo tức thì và kiểm toán thao tác quản trị.

---

### 4. Triển khai kỹ thuật

#### Các giai đoạn triển khai
* **Giai đoạn 1: Mạng VPC & Cấu hình bảo mật**
  * Khởi tạo VPC `10.0.0.0/16`, tạo 2 Public Subnets và 2 Private Subnets phân bổ trên 2 Availability Zones (`ap-southeast-1a`, `ap-southeast-1b`).
  * Gắn Internet Gateway cho Public Subnet; Private Subnet chỉ định tuyến local. Siết chặt Security Group SSH theo IP quản trị.
* **Giai đoạn 2: Nền tảng 2-Tier & Dỡ tải Media**
  * Cài đặt LAMP stack và WordPress trên EC2.
  * Khởi tạo Amazon RDS MySQL trong DB Subnet Group private.
  * Cấu hình S3 Bucket, gắn IAM Role cho EC2 để dỡ tải media lên S3.
* **Giai đoạn 3: Giám sát, Cảnh báo & Kiểm toán**
  * Tạo CloudWatch Dashboard theo dõi `CPUUtilization` và `DatabaseConnections`.
  * Thiết lập Alarm kích hoạt gửi email qua SNS khi tải CPU $\ge$ 80%.
  * Rà soát nhật ký kiểm toán trên CloudTrail Event History.
* **Giai đoạn 4: Mở rộng tính năng Serverless (Guestbook)**
  * Tạo bảng DynamoDB `GuestbookMessages` ở chế độ Provisioned.
  * Viết hàm AWS Lambda (Python 3.12) và tạo REST API trên API Gateway có bật CORS.
  * Nhúng mã form vào giao diện WordPress để gọi API.
* **Giai đoạn 5: Cấu hình Khả dụng cao (ALB + ASG)**
  * Đóng gói EC2 thành AMI và tạo Launch Template.
  * Thiết lập ALB kèm Target Group (Health Check path `/`) và liên kết vào Auto Scaling Group.
* **Giai đoạn 6: Tự động hóa Backup bằng Container & Lập lịch**
  * Viết Dockerfile đóng gói script backup, đẩy image lên Amazon ECR.
  * Tạo ECS Fargate Task Definition và cấu hình EventBridge Scheduler chạy định kỳ lúc 02:00 AM.

#### Yêu cầu kỹ thuật & Bảo mật
* **Phân tầng mạng nghiêm ngặt**: Database nằm hoàn toàn trong Private Subnet, không gán Public IP.
* **Bảo mật không dùng khóa tĩnh**: Sử dụng IAM Instance Profile và ECS Task Role, tuyệt đối không lưu access key trên mã nguồn.
* **Nguyên tắc đặc quyền tối thiểu (Least Privilege)**: Mỗi dịch vụ (Lambda, ECS, EventBridge) chỉ được cấp đúng quyền tài nguyên cần thao tác.

---

### 5. Lộ trình & Mốc triển khai

```text
+-----------------------------------------------------------------------------------+
| Tuần 1 - 3: Thiết kế mạng VPC & Triển khai nền tảng 2-Tier                        |
|   - Thiết kế VPC, Subnet, Route Table, siết Security Group SSH                   |
|   - Triển khai EC2 (LAMP), kết nối RDS MySQL và cấu hình S3 Media Offload         |
+-----------------------------------------------------------------------------------+
                                  │
                                  ▼
+-----------------------------------------------------------------------------------+
| Tuần 4 - 5: Serverless Backend & Giám sát vận hành                                |
|   - Phát triển API Gateway + Lambda + DynamoDB cho tính năng Guestbook            |
|   - Thiết lập CloudWatch Dashboard, SNS Email Alarm và kiểm toán CloudTrail       |
+-----------------------------------------------------------------------------------+
                                  │
                                  ▼
+-----------------------------------------------------------------------------------+
| Tuần 6 - 8: High Availability, Container hóa tác vụ & Tổng kết                    |
|   - Đóng gói AMI, cấu hình Application Load Balancer và Auto Scaling Group        |
|   - Đóng gói Docker backup, đẩy lên ECR, lập lịch chạy trên ECS Fargate           |
|   - Kiểm thử tích hợp toàn diện, nghiệm thu và thực hiện dọn dẹp tài nguyên       |
+-----------------------------------------------------------------------------------+
```

---

### 6. Ước tính ngân sách

Dự án được cấu hình bám sát giới hạn của AWS Free Tier và định mức Always Free:

| Dịch vụ AWS | Cấu hình / Quy mô sử dụng | Chi phí ước tính / Tháng (USD) |
| :--- | :--- | :--- |
| **Amazon EC2** | 1 instance t3.micro (750 giờ/tháng) | \$0.00 (Free Tier) |
| **Amazon RDS** | 1 instance db.t4g.micro, 20GB SSD | \$0.00 (Free Tier) |
| **Amazon S3** | Lưu trữ media và backup (< 5GB) | \$0.00 (Free Tier) |
| **AWS Lambda** | < 10,000 requests/tháng | \$0.00 (Always Free) |
| **Amazon DynamoDB** | Chế độ Provisioned: 5 RCU / 5 WCU | \$0.00 (Always Free) |
| **Amazon ECS Fargate** | 0.25 vCPU / 0.5 GB RAM, chạy ~2 phút/ngày | < \$0.05 |
| **CloudWatch & CloudTrail** | 1 Dashboard, 1 Alarm, Event History 90 ngày | \$0.00 (Free Tier) |
| **Application Load Balancer** | Chạy kiểm thử ngắn hạn và chụp minh chứng | ~\$0.50 - \$1.00 |
| **Tổng chi phí ước tính** | **Toàn bộ môi trường thực hành và kiểm thử** | **< \$1.50 USD / Tháng** |

> **Điểm tối ưu chi phí**: Không duy trì Load Balancer hay NAT Gateway chạy ngầm liên tục cả tháng. Tận dụng triệt để định mức miễn phí của RDS, DynamoDB và Lambda để đưa chi phí thực tế về gần mức \$0.

---

### 7. Đánh giá rủi ro

| Rủi ro tiềm ẩn | Mức độ ảnh hưởng | Xác suất | Chiến lược giảm thiểu |
| :--- | :--- | :--- | :--- |
| **Phát sinh phí duy trì tài nguyên** | Cao | Trung bình | Thiết lập AWS Budget cảnh báo ngưỡng \$5.00/tháng. Xóa ALB và dọn dẹp tài nguyên theo quy trình ngay sau khi hoàn thành nghiệm thu. |
| **Lỗi Target Group trên ALB (0 targets)** | Trung bình | Trung bình | Kiểm tra mục Load Balancing trong Integrations của ASG để đảm bảo đã gắn đúng Target Group. |
| **Xung đột client công cụ backup** | Thấp | Thấp | Tinh chỉnh lệnh `mysqldump` trong Docker container cho phù hợp với đặc tính của Debian/MariaDB client khi giao tiếp với RDS MySQL. |
| **Lỗi phân quyền IAM (AccessDenied)** | Trung bình | Thấp | Cấu hình đúng Trust Policy cho `scheduler.amazonaws.com` và gắn policy tối thiểu theo nguyên tắc Least Privilege. |

---

### 8. Kết quả kỳ vọng

* **Hạ tầng hoàn chỉnh, hoạt động thực tế**: Triển khai thành công ứng dụng WordPress phân tầng ổn định, có khả năng tự phục hồi, co giãn tự động và tách biệt hoàn toàn dữ liệu.
* **Làm chủ công nghệ Cloud đa dạng**: Chứng minh năng lực ứng dụng thực tế các mảng kiến thức cốt lõi: Mạng VPC, Máy chủ EC2, Cơ sở dữ liệu RDS, Lưu trữ S3, Phi máy chủ (Lambda/DynamoDB) và Container (Docker/ECS Fargate).
* **Sẵn sàng cho báo cáo và kiểm toán**: Hồ sơ thực tập đầy đủ gồm báo cáo kỹ thuật minh chứng thực tế, mã nguồn Git rõ ràng và quy trình quản trị hạ tầng an toàn, tối ưu chi phí.
