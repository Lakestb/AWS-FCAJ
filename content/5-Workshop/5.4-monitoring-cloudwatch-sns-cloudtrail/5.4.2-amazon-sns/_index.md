---
title : "Amazon SNS"
date : "2024-05-15"
weight : 2
chapter : false
pre : " <b> 5.4.2. </b> "
---

1. Navigate to **SNS** → **Topics** → **Create topic**, Standard type, name it `ec2-high-cpu-alert`.
2. Create Email Subscription, enter administrator email, confirm via verification link.

   ![SNS Topic and confirmed email subscription](/images/5/5.4.2/01-sns-topic-confirmed.png?classes=border,shadow)

3. Return to Alarm in section 5.4.1, attach action to publish to this SNS Topic on ALARM state trigger.

   ![Automated alarm notification email received from Amazon SNS](/images/5/5.4.2/02-sns-email-alert.png?classes=border,shadow)
