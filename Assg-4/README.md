Here’s your full **documentation-only README** in plain text (perfect for a GitHub project):

---

# 🚨 Monitor and Alert High AWS Billing Using AWS Lambda, Boto3, and SNS

This project demonstrates how to **automatically monitor AWS billing** and **send alerts via SNS** when your AWS spending exceeds a predefined threshold.

---

## 🧩 Features

* Retrieves **current AWS billing amount** from CloudWatch.
* Compares billing total with a **user-defined threshold** (e.g., $50).
* Sends **email alerts** using **Amazon SNS**.
* Can be **scheduled daily** using **EventBridge (CloudWatch Events)**.

---

## ⚙️ Prerequisites

* AWS Account with:

  * CloudWatch Billing Metrics Enabled
  * SNS Access
  * Lambda Execution Permissions
* IAM Role for Lambda with:

  * `CloudWatchReadOnlyAccess`
  * `AmazonSNSFullAccess`

---

## 🪩 Step 1: SNS Setup

1. Go to **Amazon SNS → Topics → Create topic**

   * Type: Standard
   * Name: `BillingAlertTopic`
2. Create a **subscription**:

   * Protocol: `Email`
   * Endpoint: your email address
   * Confirm the subscription via the email link you receive.

---

## 🔑 Step 2: Create IAM Role for Lambda

1. Go to **IAM → Roles → Create role**
2. Choose **Trusted entity type:** AWS service → **Lambda**
3. Attach the following policies:

   * `CloudWatchReadOnlyAccess`
   * `AmazonSNSFullAccess`
4. Name the role: `LambdaBillingAlertRole`

---

## 🧠 Step 3: Create Lambda Function

1. Go to **AWS Lambda → Create Function**
2. Choose **Author from scratch**

   * Name: `BillingMonitorFunction`
   * Runtime: **Python 3.12** (or 3.x)
   * Role: `LambdaBillingAlertRole`
3. Paste your billing monitoring code and deploy it.

---

## ⏰ Step 4 (Optional Bonus): Schedule Daily Trigger

To automate daily checks:

1. Go to **Amazon EventBridge → Rules → Create rule**
2. Name: `DailyBillingCheck`
3. Schedule pattern: `rate(1 day)`
4. Target: **Lambda function → BillingMonitorFunction**
5. Save and enable the rule.

---

## 🧪 Step 5: Testing

### Option 1: Manual Test

1. Open your Lambda function.
2. Click **Test → Configure test event → Create new test event**.
3. Name it `ManualBillingTest`.
4. Use this sample JSON:

```json
{
  "detail": {
    "action": "manual_test"
  }
}
```

5. Click **Test** — check the **Logs** and your **email** for alert.

### Option 2: Automatic Trigger

Wait for the **daily EventBridge trigger** — if your billing exceeds the threshold, you’ll receive an **email alert**.

---

## 🧾 Example Log Output

**When billing exceeds the threshold:**

```
Current estimated charges: $54.32  
Alert sent to SNS.
```

**When billing is within limits:**

```
Current estimated charges: $12.45  
Billing is within limits ($12.45 < $50.00).
```

---

## 🧰 Summary

| Component       | Purpose                              |
| --------------- | ------------------------------------ |
| **Lambda**      | Runs daily to check billing          |
| **CloudWatch**  | Provides AWS Billing metric          |
| **SNS**         | Sends email alert                    |
| **IAM Role**    | Grants Lambda necessary permissions  |
| **EventBridge** | (Optional) Automates daily execution |

---

## 📄 Example Architecture Diagram (Conceptual)

```
+------------------+
| CloudWatch Billing|
+---------+--------+
          |
          v
+------------------+
| Lambda Function  |
| (Check Billing)  |
+---------+--------+
          |
          v
+------------------+
| SNS Topic        |
| (Email Alert)    |
+------------------+
```

---

## ✅ Final Notes

* Ensure billing metrics are **enabled in CloudWatch**.
* SNS subscription **must be confirmed via email** before it works.
* IAM role permissions are crucial for Lambda to access CloudWatch and SNS.
* You can **update the threshold amount** directly in the Lambda code.

---
