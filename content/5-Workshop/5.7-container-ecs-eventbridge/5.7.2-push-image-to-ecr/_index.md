---
title : "Push Image to Amazon ECR"
date : "2024-05-15"
weight : 2
chapter : false
pre : " <b> 5.7.2. </b> "
---

1. Navigate to **ECR** → **Create repository**, name it `wordpress-backup`.
2. Authenticate and push image to repository:
   ```bash
   aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin <account-id>.dkr.ecr.ap-southeast-1.amazonaws.com
   docker build -t wordpress-backup .
   docker tag wordpress-backup:latest <account-id>.dkr.ecr.ap-southeast-1.amazonaws.com/wordpress-backup:latest
   docker push <account-id>.dkr.ecr.ap-southeast-1.amazonaws.com/wordpress-backup:latest
   ```

   ![Amazon ECR wordpress-backup repository storing tag latest](/images/5/5.7.2/01-ecr-repo.png?classes=border,shadow)
