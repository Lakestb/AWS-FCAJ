---
title : "Launch EC2 & Install WordPress"
date : "2024-05-15"
weight : 2
chapter : false
pre : " <b> 5.3.2. </b> "
---

1. Navigate to **EC2** → **Launch instance**, choose AMI **Ubuntu Server 24.04 LTS**, Instance type `t3.micro`.
2. Network: select `my-project-vpc`, Public Subnet 1, Auto-assign public IP: **Enable**.
3. Key pair: `my-ec2-key`. Security group: `ec2-web-sg`.
4. Once Instance status changes to Running, SSH in using user `ubuntu`, install LAMP stack (Apache 2.4, PHP 8.3, modules `php-mysql`, `php-curl`, `php-gd`, `php-xml`, `php-mbstring`).

   ![Running EC2 instance in Public Subnet](/images/5/5.3.2/01-ec2-running.png?classes=border,shadow)

5. Download WordPress, extract to `/var/www/html`, create `wp-config.php` pointing to RDS endpoint from step 5.3.1.

   ![WordPress website online via EC2 Public IP](/images/5/5.3.2/02-wordpress-installed.png?classes=border,shadow)
