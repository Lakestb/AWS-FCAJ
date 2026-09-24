---
title : "IAM Role & AWS Lambda Function"
date : "2024-05-15"
weight : 2
chapter : false
pre : " <b> 5.5.2. </b> "
---

1. Navigate to **IAM** → **Policies** → **Create policy**, grant `dynamodb:PutItem` on `GuestbookMessages`, `sns:Publish` on notification topic, and CloudWatch Logs write access. Name it `GuestbookLambdaPolicy`.
2. Create Role `GuestbookLambdaRole`, Trusted entity: Lambda, attach policy.
3. Navigate to **Lambda** → **Create function**, name `GuestbookHandler`, Runtime Python 3.12, select created execution role.
4. Paste handler code: parse POST body, validate fields, persist to DynamoDB, optionally publish SNS alert.

   ![AWS Lambda function code for GuestbookHandler](/images/5/5.5.2/01-lambda-code.png?classes=border,shadow)

   ![Successful execution test and CloudWatch Logs output](/images/5/5.5.2/02-lambda-log-test.png?classes=border,shadow)
