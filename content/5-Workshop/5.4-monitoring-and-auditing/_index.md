---
title : "Observability & Auditing (CloudWatch, SNS, CloudTrail)"
date : "2024-05-15"
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

### 5.4. Observability & Auditing: CloudWatch, SNS, CloudTrail

#### 5.4.1. CloudWatch Dashboard & Metric Alarms
* **Dashboard**: `WordPress-Production-Dashboard`, tracking `CPUUtilization` and `DatabaseConnections`.
* **Alarm**: `EC2-High-CPU-Utilization`, configured at `CPUUtilization >= 80%`.

> 📷 **Artifact**: CloudWatch dashboard metrics graphs and alarm configuration.

#### 5.4.2. SNS Alerting Notification
* **Topic**: `ec2-high-cpu-alert` with active Email subscription delivery.

> 📷 **Artifact**: SNS topic subscriptions and sample email notification.

#### 5.4.3. Governance & Auditing with AWS CloudTrail
Utilized CloudTrail Event History for zero-cost compliance:
* **`ModifySecurityGroupRules`**: captures security group SSH hardening events (section 5.2.4) with origin IP metadata.
* **`PutMetricAlarm`, `CreateTopic`, `Subscribe`**: tracks monitoring infrastructure setup (sections 5.4.1–5.4.2).

> 📷 **Artifact**: JSON event records for key management events in CloudTrail.
