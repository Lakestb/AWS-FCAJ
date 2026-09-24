---
title : "Application Load Balancer & Target Group"
date : "2024-05-15"
weight : 3
chapter : false
pre : " <b> 5.6.3. </b> "
---

1. During Auto Scaling Group creation in next step, select **Attach to a new load balancer**.
2. Type: **Application Load Balancer**, Scheme: Internet-facing, name `wordpress-alb`, select both Public Subnets.
3. Create new Target Group `wordpress-tg`, Protocol HTTP:80, Health check path `/`.

   ![ALB DNS endpoint and Target Group health check parameters](/images/5/5.6.3/01-alb-tg.png?classes=border,shadow)
