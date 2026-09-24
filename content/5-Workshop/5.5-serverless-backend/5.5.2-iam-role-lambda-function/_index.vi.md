---
title : "IAM Role & Hàm AWS Lambda"
date : "2024-05-15"
weight : 2
chapter : false
pre : " <b> 5.5.2. </b> "
---

1. Vào **IAM** → **Policies** → **Create policy**, JSON cấp quyền `dynamodb:PutItem` trên bảng `GuestbookMessages`, `sns:Publish` trên topic liên quan, và quyền ghi CloudWatch Logs. Đặt tên `GuestbookLambdaPolicy`.
2. Tạo Role `GuestbookLambdaRole`, Trusted entity: Lambda, gắn policy vừa tạo.
3. Vào **Lambda** → **Create function**, tên `GuestbookHandler`, Runtime Python 3.12, chọn Execution role đã tạo.
4. Dán code xử lý: nhận request POST, validate dữ liệu, ghi vào DynamoDB, gửi SNS (tùy chọn).

   ![Mã nguồn hàm AWS Lambda GuestbookHandler](/images/5/5.5.2/01-lambda-code.png?classes=border,shadow)

   ![CloudWatch Logs và kết quả kiểm thử hàm Lambda thành công](/images/5/5.5.2/02-lambda-log-test.png?classes=border,shadow)
