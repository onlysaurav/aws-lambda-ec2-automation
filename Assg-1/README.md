# AWS Lambda EC2 Automation Using Boto3

This project automates EC2 instance start/stop actions based on tags using AWS Lambda and Boto3.

---

## 🚀 Objective
Automatically start or stop EC2 instances depending on their `Action` tag:
- **Auto-Stop** → will be stopped.
- **Auto-Start** → will be started.

---

## 🧰 Steps Followed

### 1. EC2 Setup
- Created two t2.micro EC2 instances.
- Tagged them:
  - `Action: Auto-Stop`
  - `Action: Auto-Start`
<img width="1280" height="800" alt="Screenshot 2025-10-21 at 9 37 03 PM" src="https://github.com/user-attachments/assets/55ce1e38-9fc9-4d92-8c1f-28b9b3273271" />
<img width="1280" height="800" alt="Screenshot 2025-10-21 at 9 37 48 PM" src="https://github.com/user-attachments/assets/9b3f4c79-2c76-4ffe-9631-9359c7879101" />


### 2. IAM Role
- Created IAM Role: `lambda-ec2-manager-role`
- Attached `AmazonEC2FullAccess` policy.
  <img width="1280" height="800" alt="Screenshot 2025-10-21 at 7 00 31 PM" src="https://github.com/user-attachments/assets/1fac271c-6ea6-44e3-ac60-f83280f2e78d" />

### 3. Lambda Function
- Runtime: Python 3.x
- Permissions: Assigned the above IAM role.
- Added Boto3 script to:
  - Describe instances.
  - Start/Stop instances based on tags.
    <img width="1280" height="800" alt="Screenshot 2025-10-21 at 7 27 18 PM" src="https://github.com/user-attachments/assets/fdd24bae-0dd1-4020-b1aa-c4cf1ce67092" />

### 4. Testing
- Manually triggered Lambda.
- Verified EC2 instance states updated correctly.

---

## 📸 Screenshots
Include screenshots:
1. EC2 instances with tags
2. IAM role creation
3. Lambda setup
4. Successful execution logs

---

## 🧩 Technologies Used
- AWS Lambda
- Boto3
- IAM Roles
- EC2

---

## 👨‍💻 Author
**Saurabh Tiwari**
