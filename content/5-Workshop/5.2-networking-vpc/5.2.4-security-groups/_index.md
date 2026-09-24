---
title : "Security Groups"
date : "2024-05-15"
weight : 4
chapter : false
pre : " <b> 5.2.4. </b> "
---

1. Create Security Group `ec2-web-sg`: Inbound allows HTTP (80) from `0.0.0.0/0`, HTTPS (443) from `0.0.0.0/0`, SSH (22) strictly from administrator's IP (`/32`).

   ![Inbound rules for ec2-web-sg](/images/5/5.2.4/01-sg-ec2-web.png?classes=border,shadow)

2. Create Security Group `RDS-SG`: Inbound strictly allows MySQL/Aurora (3306) with Source set to `ec2-web-sg`.

   ![Inbound rules for RDS-SG](/images/5/5.2.4/02-sg-rds.png?classes=border,shadow)
