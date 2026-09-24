---
title : "Amazon API Gateway (REST API)"
date : "2024-05-15"
weight : 3
chapter : false
pre : " <b> 5.5.3. </b> "
---

1. Navigate to **API Gateway** → **Create API** → **REST API**, name it `GuestbookAPI`.
2. Create Resource `/guestbook`, Method POST, Integration type: Lambda Function, select `GuestbookHandler`, enable Lambda Proxy integration.
3. Select `/guestbook` resource → **Actions** → **Enable CORS**.

   ![Method POST configuration and CORS activation on API Gateway](/images/5/5.5.3/01-api-gateway-cors.png?classes=border,shadow)

4. Actions → Deploy API, create stage `prod`.
   * **Result**: Invoke URL: `https://f1atpevw96.execute-api.ap-southeast-1.amazonaws.com/prod/guestbook`.

   ![Deployed API Gateway stage prod with Invoke URL](/images/5/5.5.3/02-api-gateway-invoke-url.png?classes=border,shadow)
