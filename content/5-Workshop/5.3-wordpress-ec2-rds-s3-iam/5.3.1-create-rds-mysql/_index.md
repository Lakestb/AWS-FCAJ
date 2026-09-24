---
title : "Create Amazon RDS for MySQL"
date : "2024-05-15"
weight : 1
chapter : false
pre : " <b> 5.3.1. </b> "
---

1. Navigate to **RDS** → **Create database**, choose engine **MySQL**, template **Free tier**.
2. DB instance identifier: `wordpress-db`. Set Master username and Master password.
3. Select VPC `my-project-vpc`, DB Subnet Group consisting of 2 Private Subnets, Public access: **No**.
4. Security group: select `RDS-SG`.
   * **Result**: Endpoint `wordpress-db.cnwgwiseq95o.ap-southeast-1.rds.amazonaws.com`, status Available.

   ![RDS connectivity details with Public access set to No](/images/5/5.3.1/01-rds-connectivity.png?classes=border,shadow)
