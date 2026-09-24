---
title : "Workshop"
date : "2024-05-15"
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

### End-to-End WordPress Portfolio Blog Deployment on AWS

This document records the complete implementation sequence chronologically, from foundational infrastructure to advanced cloud services. Each section contains designated artifact placeholders (📷) for attaching implementation evidence.

---

### Workshop Outline:

1. [**5.1. Environment Setup & Region Selection**](5.1-environment-and-region/)
2. [**5.2. Networking Infrastructure (VPC, Subnets, Internet Gateway)**](5.2-networking-vpc/)
   * [5.2.1. VPC Creation](5.2-networking-vpc/5.2.1-create-vpc/)
   * [5.2.2. Subnet Configuration](5.2-networking-vpc/5.2.2-create-subnets/)
   * [5.2.3. Internet Gateway & Route Tables](5.2-networking-vpc/5.2.3-internet-gateway-route-table/)
   * [5.2.4. Security Groups](5.2-networking-vpc/5.2.4-security-groups/)
3. [**5.3. WordPress Deployment: EC2, RDS, S3, IAM**](5.3-wordpress-ec2-rds-s3-iam/)
   * [5.3.1. Amazon RDS for MySQL Creation](5.3-wordpress-ec2-rds-s3-iam/5.3.1-create-rds-mysql/)
   * [5.3.2. EC2 Provisioning & WordPress Setup](5.3-wordpress-ec2-rds-s3-iam/5.3.2-create-ec2-install-wordpress/)
   * [5.3.3. IAM Role for EC2 (Least Privilege)](5.3-wordpress-ec2-rds-s3-iam/5.3.3-iam-role-for-ec2/)
   * [5.3.4. Amazon S3 & Media Offloading](5.3-wordpress-ec2-rds-s3-iam/5.3.4-s3-offload-media/)
4. [**5.4. Monitoring & Auditing: CloudWatch, SNS, CloudTrail**](5.4-monitoring-cloudwatch-sns-cloudtrail/)
   * [5.4.1. CloudWatch Dashboard & Alarms](5.4-monitoring-cloudwatch-sns-cloudtrail/5.4.1-cloudwatch-dashboard-alarm/)
   * [5.4.2. Amazon SNS Notification](5.4-monitoring-cloudwatch-sns-cloudtrail/5.4.2-amazon-sns/)
   * [5.4.3. AWS CloudTrail Auditing](5.4-monitoring-cloudwatch-sns-cloudtrail/5.4.3-aws-cloudtrail/)
5. [**5.5. Serverless Backend: Lambda, API Gateway, DynamoDB**](5.5-serverless-backend/)
   * [5.5.1. DynamoDB Table Creation](5.5-serverless-backend/5.5.1-create-dynamodb-table/)
   * [5.5.2. IAM Role & Lambda Function](5.5-serverless-backend/5.5.2-iam-role-lambda-function/)
   * [5.5.3. Amazon API Gateway (REST API)](5.5-serverless-backend/5.5.3-api-gateway-rest-api/)
   * [5.5.4. WordPress Frontend Form Embed](5.5-serverless-backend/5.5.4-embed-form-wordpress/)
6. [**5.6. High Availability: Load Balancer & Auto Scaling**](5.6-high-availability-alb-asg/)
   * [5.6.1. AMI Packaging](5.6-high-availability-alb-asg/5.6.1-package-ec2-to-ami/)
   * [5.6.2. Launch Template](5.6-high-availability-alb-asg/5.6.2-launch-template/)
   * [5.6.3. Application Load Balancer & Target Group](5.6-high-availability-alb-asg/5.6.3-alb-target-group/)
   * [5.6.4. Auto Scaling Group](5.6-high-availability-alb-asg/5.6.4-auto-scaling-group/)
7. [**5.7. Containerization & Automation: Docker, ECS Fargate, EventBridge**](5.7-container-ecs-eventbridge/)
   * [5.7.1. Docker Image Packaging](5.7-container-ecs-eventbridge/5.7.1-docker-image-packaging/)
   * [5.7.2. Push Image to Amazon ECR](5.7-container-ecs-eventbridge/5.7.2-push-image-to-ecr/)
   * [5.7.3. IAM Roles & ECS Task Definition](5.7-container-ecs-eventbridge/5.7.3-iam-roles-ecs-task-definition/)
   * [5.7.4. Manual Testing & EventBridge Scheduler](5.7-container-ecs-eventbridge/5.7.4-manual-test-eventbridge-scheduler/)
8. [**5.8. Resource Cleanup**](5.8-resource-cleanup/)
   * [5.8.1. Delete EventBridge Scheduler & ECS](5.8-resource-cleanup/5.8.1-delete-eventbridge-ecs/)
   * [5.8.2. Teardown High Availability Stack](5.8-resource-cleanup/5.8.2-delete-high-availability/)
   * [5.8.3. Remove Serverless Stack](5.8-resource-cleanup/5.8.3-delete-serverless/)
   * [5.8.4. Delete Monitoring Configuration](5.8-resource-cleanup/5.8.4-delete-monitoring/)
   * [5.8.5. Delete Database, Compute & Storage](5.8-resource-cleanup/5.8.5-delete-database-compute-storage/)
   * [5.8.6. Delete Networking & IAM](5.8-resource-cleanup/5.8.6-delete-networking-iam/)
