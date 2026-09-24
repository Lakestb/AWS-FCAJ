---
title : "Teardown High Availability Stack"
date : "2024-05-15"
weight : 2
chapter : false
pre : " <b> 5.8.2. </b> "
---

1. Set Desired = 0 on `wordpress-asg`, wait for instance termination, then delete ASG.
2. Delete Application Load Balancer `wordpress-alb` and Target Group `wordpress-tg`.
3. Delete Launch Template `wordpress-launch-template` and deregister AMI `wordpress-app-ami-v1` (including snapshots).
