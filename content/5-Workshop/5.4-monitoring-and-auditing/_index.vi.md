---
title : "Giám sát & Kiểm toán: CloudWatch, SNS, CloudTrail"
date : "2024-05-15"
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

### 5.4. Giám sát & Kiểm toán: CloudWatch, SNS, CloudTrail

#### 5.4.1. CloudWatch Dashboard & Alarm
* **Dashboard**: `WordPress-Production-Dashboard`, theo dõi `CPUUtilization` của EC2 và `DatabaseConnections` của RDS.
* **Alarm**: `EC2-High-CPU-Utilization`, kích hoạt khi `CPUUtilization >= 80%`.

> 📷 **Ảnh minh chứng**: Dashboard CloudWatch và cấu hình chi tiết của Alarm.

#### 5.4.2. Thông báo qua Amazon SNS
* **Topic**: `ec2-high-cpu-alert`, Subscription qua Email, tự động gửi cảnh báo khi Alarm kích hoạt.

> 📷 **Ảnh minh chứng**: Cấu hình SNS Topic/Subscription và email cảnh báo nhận được.

#### 5.4.3. Kiểm toán hoạt động với AWS CloudTrail
Sử dụng CloudTrail Event History (miễn phí, lưu 90 ngày) — không dùng CloudTrail Lake vì không cần thiết và tính phí:
* **Sự kiện `ModifySecurityGroupRules`**: ghi lại đúng thời điểm chỉnh sửa rule SSH ở mục 5.2.4, thể hiện rõ user, IP nguồn, nội dung thay đổi.
* **Sự kiện `PutMetricAlarm`, `CreateTopic`, `Subscribe`**: minh chứng cho việc thiết lập CloudWatch/SNS ở mục 5.4.1–5.4.2.

> 📷 **Ảnh minh chứng**: Chi tiết (JSON) của sự kiện `ModifySecurityGroupRules` và `PutMetricAlarm` trong CloudTrail Event History.
