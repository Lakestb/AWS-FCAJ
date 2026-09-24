---
title : "Embed Form into WordPress"
date : "2024-05-15"
weight : 4
chapter : false
pre : " <b> 5.5.4. </b> "
---

1. Create a new page on WordPress, add a **Custom HTML** block.
2. Paste HTML form markup (Name, Email, Message) and client JavaScript triggering `fetch()` to the Invoke URL.

   ![Guestbook form rendering and submitting on WordPress](/images/5/5.5.4/01-wordpress-form.png?classes=border,shadow)

3. Publish page, test form submission, verify record entry in DynamoDB and email delivery via SNS.

   ![Persisted feedback record in DynamoDB GuestbookMessages table](/images/5/5.5.4/02-dynamodb-items.png?classes=border,shadow)

   ![Instant email notification delivered via Amazon SNS](/images/5/5.5.4/03-sns-email-received.png?classes=border,shadow)
