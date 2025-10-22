# 🧹 Automated S3 Bucket Cleanup Using AWS Lambda and Boto3

### 🎯 Objective
Create an AWS Lambda function that automatically deletes files older than 30 days in a specific S3 bucket.

---

## 🏗️ Project Overview

This project demonstrates how to automate S3 bucket maintenance using **AWS Lambda** and **Boto3**.  
The Lambda function checks all files in a bucket and deletes those older than a defined threshold (default: 30 days).

---

## ⚙️ Setup Instructions

### 1️⃣ Create an S3 Bucket
- Go to AWS S3 → Create Bucket (e.g., `my-lambda-cleanup-bucket`).
- Upload several files for testing.

### 2️⃣ Create an IAM Role
- Go to AWS IAM → Roles → Create Role → AWS Service → Lambda.
- Attach `AmazonS3FullAccess` policy.
- Name it `lambda-s3-cleanup-role`.

### 3️⃣ Create Lambda Function
- Runtime: Python 3.x  
- Attach the IAM role above.  
- Copy-paste the code from `lambda_function.py`.

### 4️⃣ Deploy and Test
- Click **Deploy** in the Lambda console.
- Click **Test** and run a manual invocation.
- Check CloudWatch logs or S3 bucket to verify deleted files.

---

## 🧪 Example Output
