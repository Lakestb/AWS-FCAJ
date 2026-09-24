---
title : "Internet Gateway & Route Table"
date : "2024-05-15"
weight : 3
chapter : false
pre : " <b> 5.2.3. </b> "
---

1. Navigate to **Internet Gateways** → **Create internet gateway**, name it `my-project-igw` → **Attach to VPC** → select `my-project-vpc`.
2. Navigate to **Route Tables**, create a route table for Public Subnets, add route `0.0.0.0/0` → Target: created Internet Gateway.
3. Associate this route table with both Public Subnets.

   ![Public Route Table with IGW association](/images/5/5.2.3/01-route-table-public.png?classes=border,shadow)

4. Keep Private Subnet Route Table at default (local route only), do not add Internet routing.

   ![Private Route Table with local route only](/images/5/5.2.3/02-route-table-private.png?classes=border,shadow)
