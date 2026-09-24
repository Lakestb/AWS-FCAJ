---
title : "Tạo 4 Subnet"
date : "2024-05-15"
weight : 2
chapter : false
pre : " <b> 5.2.2. </b> "
---

1. Vào **Subnets** → **Create subnet**, chọn VPC vừa tạo.
2. Tạo lần lượt 4 subnet:
   * `my-project-subnet-public1-ap-southeast-1a` — AZ `ap-southeast-1a` — CIDR `10.0.0.0/20`.
   * `my-project-subnet-public2-ap-southeast-1b` — AZ `ap-southeast-1b` — CIDR `10.0.16.0/20`.
   * `my-project-subnet-private1-ap-southeast-1a` — AZ `ap-southeast-1a` — CIDR `10.0.128.0/20`.
   * `my-project-subnet-private2-ap-southeast-1b` — AZ `ap-southeast-1b` — CIDR `10.0.144.0/20`.

   ![Danh sách 4 Subnet trong VPC](/images/5/5.2.2/01-subnets.png?classes=border,shadow)
