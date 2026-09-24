---
title : "Amazon API Gateway (REST API)"
date : "2024-05-15"
weight : 3
chapter : false
pre : " <b> 5.5.3. </b> "
---

1. Vào **API Gateway** → **Create API** → **REST API**, đặt tên `GuestbookAPI`.
2. Tạo Resource `/guestbook`, Method POST, Integration type: Lambda Function, chọn `GuestbookHandler`, bật Lambda Proxy integration.
3. Chọn resource `/guestbook` → **Actions** → **Enable CORS**.

   ![Cấu hình Method POST và kích hoạt CORS trên API Gateway](/images/5/5.5.3/01-api-gateway-cors.png?classes=border,shadow)

4. Actions → Deploy API, tạo stage `prod`.
   * **Kết quả**: Invoke URL: `https://f1atpevw96.execute-api.ap-southeast-1.amazonaws.com/prod/guestbook`.

   ![API Gateway Deploy stage prod và Invoke URL](/images/5/5.5.3/02-api-gateway-invoke-url.png?classes=border,shadow)
