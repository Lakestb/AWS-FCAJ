---
title : "Auto Scaling Group"
date : "2024-05-15"
weight : 4
chapter : false
pre : " <b> 5.6.4. </b> "
---

1. Vào **Auto Scaling Groups** → **Create Auto Scaling group**, tên `wordpress-asg`, chọn Launch Template ở mục 5.6.2.
2. Network: chọn VPC và cả 2 Public Subnet.
3. Group size: Desired = 1, Min = 1, Max = 2.
4. Scaling policy: Target tracking, metric Average CPU Utilization, target value 70.

   ![Cấu hình kích thước và chính sách co giãn Auto Scaling Group](/images/5/5.6.4/01-asg-config.png?classes=border,shadow)

5. Sau khi tạo, vào tab Integrations kiểm tra mục Load balancing đã gắn đúng Target Group `wordpress-tg` chưa — nếu để trống, bấm Edit và gắn lại thủ công.
   * **Kết quả**: Target Group chuyển sang 1 Healthy, website truy cập được qua DNS của ALB.

   ![Target Group chuyển sang trạng thái 1 Healthy](/images/5/5.6.4/02-tg-healthy.png?classes=border,shadow)

   ![Website WordPress truy cập thành công qua DNS của Application Load Balancer](/images/5/5.6.4/03-wordpress-alb-dns.png?classes=border,shadow)
