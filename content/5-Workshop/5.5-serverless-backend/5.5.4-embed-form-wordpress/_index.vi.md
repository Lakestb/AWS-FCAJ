---
title : "Nhúng Form vào WordPress"
date : "2024-05-15"
weight : 4
chapter : false
pre : " <b> 5.5.4. </b> "
---

1. Tạo trang mới trên WordPress, thêm khối **Custom HTML** (không dùng khối Code).
2. Dán HTML form (Tên, Email, Lời nhắn) và đoạn JavaScript gọi `fetch()` tới Invoke URL ở mục 5.5.3.

   ![Form Guestbook hiển thị và gửi thành công trên WordPress](/images/5/5.5.4/01-wordpress-form.png?classes=border,shadow)

3. Publish trang, kiểm thử gửi form, xác nhận dữ liệu xuất hiện trong DynamoDB và email SNS nhận được.

   ![Bản ghi phản hồi xuất hiện trong bảng DynamoDB GuestbookMessages](/images/5/5.5.4/02-dynamodb-items.png?classes=border,shadow)

   ![Email thông báo tức thì nhận được qua Amazon SNS](/images/5/5.5.4/03-sns-email-received.png?classes=border,shadow)
