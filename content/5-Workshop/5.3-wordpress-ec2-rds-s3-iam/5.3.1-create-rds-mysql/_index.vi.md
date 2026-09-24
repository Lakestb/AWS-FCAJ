---
title : "Khởi tạo Amazon RDS for MySQL"
date : "2024-05-15"
weight : 1
chapter : false
pre : " <b> 5.3.1. </b> "
---

1. Vào **RDS** → **Create database**, chọn engine **MySQL**, template **Free tier**.
2. DB instance identifier: `wordpress-db`. Đặt Master username và Master password.
3. Chọn VPC `my-project-vpc`, DB Subnet Group gồm 2 Private Subnet, Public access: **No**.
4. Security group: chọn `RDS-SG`.
   * **Kết quả**: Endpoint `wordpress-db.cnwgwiseq95o.ap-southeast-1.rds.amazonaws.com`, trạng thái Available.

   ![Thông tin kết nối RDS wordpress-db với Public access No](/images/5/5.3.1/01-rds-connectivity.png?classes=border,shadow)
