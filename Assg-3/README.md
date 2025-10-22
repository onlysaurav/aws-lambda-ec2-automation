# Auto-Tagging EC2 Instances on Launch

This project demonstrates how to automatically tag EC2 instances when they are launched using **AWS Lambda** and **EventBridge (CloudWatch Events)**.

## Features

- Automatically tags new EC2 instances with:
  - `LaunchDate` = current UTC date
  - `Environment` = "AutoTagged"
- Uses Boto3 to interact with EC2
- Event-driven using EventBridge rule for `EC2 Instance State-change Notification`

## Setup Instructions

### 1. IAM Role for Lambda

Create a new IAM role (`lambda-role`) with:

- **Managed Policies**:
  - `AmazonEC2FullAccess`
  - `AWSLambdaBasicExecutionRole`

This allows the Lambda function to tag EC2 instances and write logs to CloudWatch.

### 2. Lambda Function

1. Go to **Lambda → Create function**
2. Choose **Python 3.x** runtime
3. Assign **lambda-role** as execution role
4. Copy `lambda_function.py` code into the Lambda editor
5. Set environment variable `AWS_REGION` if needed (default is current region)
6. Save and deploy

### 3. EventBridge Rule

1. Go to **EventBridge → Rules → Create rule**
2. Name: `saurabh-trigger-lambda`
3. Rule type: **Event pattern**
4. Event pattern:

```json
{
  "source": ["aws.ec2"],
  "detail-type": ["EC2 Instance State-change Notification"],
  "detail": {
    "state": ["running"]
  }
}

## 4. (Optional) Debugging Tips

If tags don’t appear:

Check CloudWatch Logs for the Lambda.

Verify Lambda permissions (it needs EC2 tagging rights).

Ensure EventBridge rule is enabled and correctly linked.

We can also manually trigger the Lambda with a sample test event like:

{
  "detail": {
    "instances": [
      {"instance-id": ""}
    ]
  }
}
