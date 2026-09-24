---
title : "Application Load Balancer & Target Group"
date : "2024-05-15"
weight : 3
chapter : false
pre : " <b> 5.6.3. </b> "
---

1. Trong quá trình tạo Auto Scaling Group ở mục sau, chọn **Attach to a new load balancer**.
2. Loại: **Application Load Balancer**, Scheme: Internet-facing, tên `wordpress-alb`, chọn cả 2 Public Subnet.
3. Tạo Target Group mới `wordpress-tg`, Protocol HTTP:80, Health check path `/`.

   ![DNS Name của ALB và thông số Target Group](/images/5/5.6.3/01-alb-tg.png?classes=border,shadow)
