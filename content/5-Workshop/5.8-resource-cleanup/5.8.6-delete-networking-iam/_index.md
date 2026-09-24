---
title : "Delete Networking & IAM"
date : "2024-05-15"
weight : 6
chapter : false
pre : " <b> 5.8.6. </b> "
---

1. Delete Security Groups (`ec2-web-sg`, `RDS-SG`).
2. Delete 4 Subnets, Route Tables, Internet Gateway, and delete VPC `my-project-vpc`.
3. Finally, delete all created IAM Roles and Policies after ensuring no dependencies remain.
