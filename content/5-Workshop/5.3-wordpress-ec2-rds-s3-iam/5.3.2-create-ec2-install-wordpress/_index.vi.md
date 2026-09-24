---
title : "Khởi tạo EC2 và cài đặt WordPress"
date : "2024-05-15"
weight : 2
chapter : false
pre : " <b> 5.3.2. </b> "
---

1. Vào **EC2** → **Launch instance**, chọn AMI **Ubuntu Server 24.04 LTS**, Instance type `t3.micro`.
2. Network: chọn `my-project-vpc`, Public Subnet 1, Auto-assign public IP: **Enable**.
3. Key pair: `my-ec2-key`. Security group: `ec2-web-sg`.
4. Sau khi Instance chuyển sang Running, SSH vào bằng user `ubuntu`, cài đặt LAMP stack (Apache 2.4, PHP 8.3, các module `php-mysql`, `php-curl`, `php-gd`, `php-xml`, `php-mbstring`).

   ![Thông tin EC2 Instance đang chạy trong Public Subnet](/images/5/5.3.2/01-ec2-running.png?classes=border,shadow)

5. Tải WordPress, giải nén vào `/var/www/html`, tạo file `wp-config.php` trỏ tới RDS endpoint ở mục 5.3.1.

   ![Website WordPress hoạt động thành công qua Public IP của EC2](/images/5/5.3.2/02-wordpress-installed.png?classes=border,shadow)
