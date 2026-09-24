---
title : "AWS CloudTrail"
date : "2024-05-15"
weight : 3
chapter : false
pre : " <b> 5.4.3. </b> "
---

1. Navigate to **CloudTrail** → **Event history** (enabled by default for 90 days, no extra trail required).
2. Filter by Event names `ModifySecurityGroupRules`, `PutMetricAlarm`, `CreateTopic`, `Subscribe` to verify administrative actions.

   ![Audit trail records in CloudTrail Event history](/images/5/5.4.3/01-cloudtrail-event-history.png?classes=border,shadow)

   ![Detailed JSON payload of CloudTrail audit event](/images/5/5.4.3/02-cloudtrail-event-json.png?classes=border,shadow)
