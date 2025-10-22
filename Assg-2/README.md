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

  <img width="1280" height="800" alt="Screenshot 2025-10-22 at 12 22 56 PM" src="https://github.com/user-attachments/assets/aef2bcff-4ed6-46f8-8ee3-804ce50bef22" />

### 2️⃣ Create an IAM Role
- Go to AWS IAM → Roles → Create Role → AWS Service → Lambda.
- Attach `AmazonS3FullAccess` policy.
- Name it `lambda-s3-cleanup-role`.
  
  <img width="1280" height="800" alt="Screenshot 2025-10-22 at 1 59 12 PM" src="https://github.com/user-attachments/assets/28c88ee4-50a0-4275-a51b-0ba67f87bc5f" />

  
### 3️⃣ Create Lambda Function
- Runtime: Python 3.x  
- Attach the IAM role above.  
- Copy-paste the code from `lambda_function.py`.
  
  <img width="1280" height="800" alt="Screenshot 2025-10-22 at 2 01 21 PM" src="https://github.com/user-attachments/assets/0461d337-faee-432d-8f1c-a2b9059c2e3a" />

  
### 4️⃣ Deploy and Test
- Click **Deploy** in the Lambda console.
- Click **Test** and run a manual invocation.
- Check CloudWatch logs or S3 bucket to verify deleted files.


   <img width="1280" height="800" alt="Screenshot 2025-10-22 at 1 59 47 PM" src="https://github.com/user-attachments/assets/fcf80b12-f5a1-4bab-afbb-ea1e1b91d2bf" />

## 🧪 Example Output
   START RequestId: cbc49481-0aaf-43b2-9ad5-fdb2bce2bfb6 Version: $LATEST
Deleting old file: Screenshot 2025-10-21 at 7.37.21 PM.png (Last modified: 2025-10-22 06:52:28+00:00)
Deleting old file: Screenshot 2025-10-22 at 12.16.58 PM.png (Last modified: 2025-10-22 06:52:29+00:00)
Deleting old file: old_1.txt (Last modified: 2025-10-22 08:04:05+00:00)
Deleted files: ['Screenshot 2025-10-21 at 7.37.21\u202fPM.png', 'Screenshot 2025-10-22 at 12.16.58\u202fPM.png', 'old_1.txt']
END RequestId: cbc49481-0aaf-43b2-9ad5-fdb2bce2bfb6
REPORT RequestId: cbc49481-0aaf-43b2-9ad5-fdb2bce2bfb6	Duration: 3673.57 ms	Billed Duration: 3969 ms	Memory Size: 128 MB	Max Memory Used: 86 MB	Init Duration: 294.73 ms	
