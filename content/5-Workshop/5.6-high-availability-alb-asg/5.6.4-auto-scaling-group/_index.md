---
title : "Auto Scaling Group"
date : "2024-05-15"
weight : 4
chapter : false
pre : " <b> 5.6.4. </b> "
---

1. Navigate to **Auto Scaling Groups** → **Create Auto Scaling group**, name `wordpress-asg`, choose Launch Template from 5.6.2.
2. Network: select VPC and both Public Subnets.
3. Group size: Desired = 1, Min = 1, Max = 2.
4. Scaling policy: Target tracking, metric Average CPU Utilization, target value 70.

   ![Auto Scaling Group capacity and scaling policy parameters](/images/5/5.6.4/01-asg-config.png?classes=border,shadow)

5. After creation, check Integrations tab to verify Target Group `wordpress-tg` attachment — if empty, click Edit and re-attach manually.
   * **Result**: Target Group reflects 1 Healthy instance, WordPress is reachable via ALB DNS.

   ![Target Group indicates 1 Healthy registered instance](/images/5/5.6.4/02-tg-healthy.png?classes=border,shadow)

   ![WordPress website loaded smoothly over Application Load Balancer DNS](/images/5/5.6.4/03-wordpress-alb-dns.png?classes=border,shadow)
