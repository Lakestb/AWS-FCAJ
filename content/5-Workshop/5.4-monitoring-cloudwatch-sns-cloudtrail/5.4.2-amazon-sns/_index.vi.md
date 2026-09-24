---
title : "Amazon SNS"
date : "2024-05-15"
weight : 2
chapter : false
pre : " <b> 5.4.2. </b> "
---

1. Vào **SNS** → **Topics** → **Create topic**, loại Standard, đặt tên `ec2-high-cpu-alert`.
2. Tạo Subscription loại Email, nhập email quản trị, xác nhận (Confirm) qua email nhận được.

   ![SNS Topic và Subscription đã xác nhận Confirmed](/images/5/5.4.2/01-sns-topic-confirmed.png?classes=border,shadow)

3. Quay lại Alarm ở mục 5.4.1, gắn Action gửi tới SNS Topic này khi Alarm chuyển sang trạng thái ALARM.

   ![Email cảnh báo tự động nhận từ Amazon SNS khi kích hoạt Alarm](/images/5/5.4.2/02-sns-email-alert.png?classes=border,shadow)
