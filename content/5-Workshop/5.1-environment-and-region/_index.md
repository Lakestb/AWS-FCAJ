---
title : "Environment Setup & Region Selection"
date : "2024-05-15"
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

1. Sign in to AWS Console using IAM account `cloud-admin` (avoid root account for daily operations).

   ![Sign in with IAM account cloud-admin](/images/5/5.1/01-iam-signin.png?classes=border,shadow)

2. At the top-right corner, select Region Asia Pacific (Singapore) — `ap-southeast-1`.
3. Create a new Key Pair: navigate to **EC2** → **Key Pairs** → **Create key pair**, name it `my-ec2-key`, format `.pem`, download file for SSH access.

   ![Create EC2 Key Pair my-ec2-key](/images/5/5.1/02-create-keypair.png?classes=border,shadow)
