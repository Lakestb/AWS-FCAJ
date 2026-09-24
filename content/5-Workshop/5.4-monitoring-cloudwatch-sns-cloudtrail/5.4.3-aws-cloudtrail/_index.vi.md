---
title : "AWS CloudTrail"
date : "2024-05-15"
weight : 3
chapter : false
pre : " <b> 5.4.3. </b> "
---

1. Vào **CloudTrail** → **Event history** (đã bật sẵn miễn phí, lưu 90 ngày, không cần tạo Trail mới).
2. Lọc theo Event name `ModifySecurityGroupRules`, `PutMetricAlarm`, `CreateTopic`, `Subscribe` để tìm đúng các sự kiện đã thực hiện.

   ![Danh sách sự kiện kiểm toán trên CloudTrail Event history](/images/5/5.4.3/01-cloudtrail-event-history.png?classes=border,shadow)

   ![Chi tiết định dạng JSON của sự kiện CloudTrail](/images/5/5.4.3/02-cloudtrail-event-json.png?classes=border,shadow)
