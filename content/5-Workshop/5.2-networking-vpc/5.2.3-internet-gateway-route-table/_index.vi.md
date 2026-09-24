---
title : "Internet Gateway & Route Table"
date : "2024-05-15"
weight : 3
chapter : false
pre : " <b> 5.2.3. </b> "
---

1. Vào **Internet Gateways** → **Create internet gateway**, đặt tên `my-project-igw` → **Attach to VPC** → chọn `my-project-vpc`.
2. Vào **Route Tables**, tạo route table cho Public Subnet, thêm route `0.0.0.0/0` → Target: Internet Gateway vừa tạo.
3. Associate route table này với cả 2 Public Subnet.

   ![Route Table cho Public Subnet liên kết Internet Gateway](/images/5/5.2.3/01-route-table-public.png?classes=border,shadow)

4. Route Table của Private Subnet giữ nguyên mặc định (chỉ có route local), không thêm route ra Internet.

   ![Route Table cho Private Subnet chỉ có local route](/images/5/5.2.3/02-route-table-private.png?classes=border,shadow)
