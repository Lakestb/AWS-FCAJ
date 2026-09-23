---
title : "Backend Serverless: Lambda, API Gateway, DynamoDB"
date : "2024-05-15"
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

### 5.5. Backend Serverless: Lambda, API Gateway, DynamoDB

Xây dựng thêm tính năng Guestbook (lời nhắn khách) — một backend serverless độc lập, chạy song song với WordPress, không ảnh hưởng tới kiến trúc chính.

#### 5.5.1. Khởi tạo bảng DynamoDB
* **Bảng**: `GuestbookMessages`, Partition key: `id` (String), Capacity mode: Provisioned 5 RCU / 5 WCU (nằm trong Free Tier).

> 📷 **Ảnh minh chứng**: Cấu hình bảng DynamoDB GuestbookMessages.

#### 5.5.2. IAM Role cho Lambda (Least Privilege)
* **Policy `GuestbookLambdaPolicy`**: chỉ cấp quyền `dynamodb:PutItem` trên đúng bảng `GuestbookMessages`, `sns:Publish` trên đúng topic, và quyền ghi CloudWatch Logs.
* **Role**: `GuestbookLambdaRole`, gắn policy trên.

> 📷 **Ảnh minh chứng**: Nội dung Policy JSON và Role đã tạo.

#### 5.5.3. Hàm AWS Lambda xử lý Guestbook
* **Function**: `GuestbookHandler`, Runtime Python 3.12.
* **Logic**: nhận request POST, validate dữ liệu (tên, email, nội dung), ghi vào DynamoDB, gửi thông báo qua SNS (tùy chọn).

> 📷 **Ảnh minh chứng**: Code Lambda trong Console và kết quả log CloudWatch của lần chạy thành công (dòng REPORT RequestId).

#### 5.5.4. Amazon API Gateway (REST API)
* **API**: `GuestbookAPI`, resource `/guestbook`, method POST, tích hợp Lambda Proxy.
* Bật CORS để WordPress (khác domain) có thể gọi API.
* **Stage triển khai**: `prod`, Invoke URL: `https://f1atpevw96.execute-api.ap-southeast-1.amazonaws.com/prod/guestbook`.

> 📷 **Ảnh minh chứng**: Cấu hình method POST, CORS đã bật, và màn hình Deploy API với Invoke URL.

#### 5.5.5. Nhúng giao diện vào WordPress
* Sử dụng khối Custom HTML (không dùng khối Code, tránh bị hiển thị dạng văn bản thô) trong trình soạn thảo WordPress.
* Form gồm: Tên, Email (không bắt buộc), Lời nhắn — gọi API qua JavaScript `fetch()`.

> 📷 **Ảnh minh chứng**: Form Guestbook hiển thị đúng trên trang WordPress công khai.

#### 5.5.6. Kiểm thử end-to-end
* Gửi thử form → xác nhận dữ liệu xuất hiện trong DynamoDB → xác nhận nhận được email SNS.

> 📷 **Ảnh minh chứng**: Dữ liệu trong DynamoDB (Explore table items) và email cảnh báo nhận được.
