Got it! Here’s your original doc, **cleaned up only for formatting and minor fixes**, keeping the structure and wording almost exactly the same:

---

# Auto-Tagging EC2 Instances on Launch

This project demonstrates how to automatically tag EC2 instances when they are launched using **AWS Lambda** and **EventBridge (CloudWatch Events)**.

## Features

* Automatically tags new EC2 instances with:

  * `LaunchDate` = current UTC date
  * `Environment` = "AutoTagged"
* Uses Boto3 to interact with EC2
* Event-driven using EventBridge rule for `EC2 Instance State-change Notification`

---

## Setup Instructions

### 1. IAM Role for Lambda

Create a new IAM role (`lambda-role`) with:

* **Managed Policies**:

  * `AmazonEC2FullAccess`
  * `AWSLambdaBasicExecutionRole`

    <img width="1280" height="800" alt="Screenshot 2025-10-22 at 10 53 17 PM" src="https://github.com/user-attachments/assets/ca522b79-dd54-4b5a-aeec-6b013bd94f42" />

     

This allows the Lambda function to tag EC2 instances and write logs to CloudWatch.

---

### 2. Lambda Function

1. Go to **Lambda → Create function**
2. Choose **Python 3.x** runtime
3. Assign **lambda-role** as execution role
4. Copy `lambda_function.py` code into the Lambda editor
5. Set environment variable `AWS_REGION` if needed (default is current region)
6. Save and deploy

   <img width="1280" height="800" alt="Screenshot 2025-10-22 at 10 54 19 PM" src="https://github.com/user-attachments/assets/7fcbdb7c-e831-4e55-b0b2-f09764d75483" />

   
---

### 3. EventBridge Rule

1. Go to **EventBridge → Rules → Create rule**
2. Name: `saurabh-trigger-lambda`
3. Rule type: **Event pattern**
4. Event pattern:

   <img width="1280" height="800" alt="Screenshot 2025-10-22 at 10 58 31 PM" src="https://github.com/user-attachments/assets/0aba058d-1185-478a-959d-e7e37edd96e9" />

   
```json
{
  "source": ["aws.ec2"],
  "detail-type": ["EC2 Instance State-change Notification"],
  "detail": {
    "state": ["running"]
  }
}

  
```

5. Set **target** as the Lambda function you created

---

### 4. (Optional) Debugging & Manual Testing

If tags don’t appear:

* Check CloudWatch Logs for the Lambda
* Verify Lambda permissions (it needs EC2 tagging rights)
* Ensure EventBridge rule is enabled and correctly linked

You can also manually trigger the Lambda with a sample test event:

```json
{
  "detail": {
    "instances": [
      {"instance-id": "i-0abcd1234efgh5678"}
    ]
  }
}
```
  <img width="1280" height="800" alt="Screenshot 2025-10-22 at 6 16 56 PM" src="https://github.com/user-attachments/assets/145dd3f7-c5fb-403a-ba1e-3c6cdec48d49" />

  <img width="1280" height="800" alt="Screenshot 2025-10-22 at 7 05 25 PM" src="https://github.com/user-attachments/assets/a9d62e45-a078-4dfa-a378-3499c5aae4dd" />


