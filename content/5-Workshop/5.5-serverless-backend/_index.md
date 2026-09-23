---
title : "Serverless Backend (Lambda, API Gateway, DynamoDB)"
date : "2024-05-15"
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

### 5.5. Serverless Backend: Lambda, API Gateway, DynamoDB

Independent serverless Guestbook pipeline deployed alongside WordPress.

#### 5.5.1. DynamoDB Table Provisioning
* **Table**: `GuestbookMessages`, Partition key: `id` (String), Capacity mode: Provisioned 5 RCU / 5 WCU.

> 📷 **Artifact**: DynamoDB table configuration dashboard.

#### 5.5.2. Scoped IAM Roles for Lambda
* **Policy `GuestbookLambdaPolicy`**: `dynamodb:PutItem`, `sns:Publish`, CloudWatch logging.
* **Role**: `GuestbookLambdaRole`.

> 📷 **Artifact**: Lambda execution role JSON policy.

#### 5.5.3. AWS Lambda Function Implementation
* **Function**: `GuestbookHandler`, Runtime Python 3.12.
* **Flow**: Parses input payload, validates fields, writes item to DynamoDB, triggers SNS notification.

> 📷 **Artifact**: Lambda code console and CloudWatch log execution stream.

#### 5.5.4. Amazon API Gateway Integration
* **API**: `GuestbookAPI` (REST), resource `/guestbook`, method POST with CORS enabled.
* **Stage**: `prod`.

> 📷 **Artifact**: Method execution overview and API deployment stage URL.

#### 5.5.5. WordPress Frontend Form Embed
* Integrated via Custom HTML block calling backend endpoint via JavaScript `fetch()`.

> 📷 **Artifact**: Rendered guestbook submission interface on WordPress frontend.

#### 5.5.6. End-to-End Validation
* Form submission verification in DynamoDB table explorer and inbox receipt of SNS alert.

> 📷 **Artifact**: DynamoDB item explorer console and delivery notification.
