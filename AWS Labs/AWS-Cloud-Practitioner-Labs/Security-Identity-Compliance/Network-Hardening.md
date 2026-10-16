# AWS Inspector: Vulnerability Assessment and Remediation

## Overview

This lab demonstrates how I used **Amazon Inspector** to automatically scan for vulnerabilities in my **AWS Lambda functions**, analyze security findings, remediate identified issues, and verify the results through continuous scanning. By completing this lab, I gained hands-on experience with real-world security assessment workflows used in enterprise cloud environments.

---

## Lab Tasks

---

### 1️⃣ Activate Amazon Inspector

I started by activating Amazon Inspector to enable automated scanning across my AWS account.

**Steps Performed:**

* Opened **Amazon Inspector** in the AWS Console
* Clicked **Activate Inspector**
* Confirmed activation
* Inspector automatically scanned all Lambda functions (coverage 100%)

```

<img width="1091" height="554" alt="image" src="https://github.com/user-attachments/assets/b1d05898-bc08-4271-9da1-8c1ba6ac3f84" />

---

### 2️⃣ Review Inspector Findings

After Inspector completed its initial scan, I reviewed the vulnerability findings.

**Key Activities:**

* Navigated to **All findings**
* Reviewed severity levels, CVEs, affected resources, and impacted package versions
* A common finding was `CVE-2023-32681` impacting the `requests` Python package


```

**Example Finding:**

| Finding | CVE ID         | Severity | Resource    | Package  | Version |
| ------- | -------------- | -------- | ----------- | -------- | ------- |
| 1       | CVE-2023-32681 | Medium   | get-request | requests | 2.20.0  |

<img width="1346" height="562" alt="image" src="https://github.com/user-attachments/assets/fce50ffe-853f-4553-9c99-4b65ccfa81cf" />

---

### 3️⃣ Remediation Process

The goal was to resolve the `CVE-2023-32681` vulnerability.

#### **Step 1: Open the Lambda Function**

I opened the Lambda function **get-request** and accessed its `requirements.txt` file.




<img width="1359" height="559" alt="image" src="https://github.com/user-attachments/assets/c14f16b4-a5dd-465d-b387-88dfc4594265" />

#### **Step 2: Update Dependencies**

I updated the vulnerable dependency.

```text
# BEFORE (vulnerable)
requests==2.20.0

# AFTER (remediated)
requests
```

#### **Step 3: Deploy the Updated Lambda Function**

After updating dependencies, I deployed the function, triggering an automatic re-scan.

**📸 Screenshot Placeholder**




<img width="1331" height="560" alt="image" src="https://github.com/user-attachments/assets/ae0b63e0-4cb3-47ba-95b4-85195deaac3a" />
<img width="1338" height="559" alt="image" src="https://github.com/user-attachments/assets/1699f2cc-8e95-4d25-9755-f20a5d7735d3" />

#### **Step 4: Verify Remediation**

I waited for Amazon Inspector to re-scan the Lambda function.

**Verification Steps:**

* Filtered results to **Closed** findings
* Confirmed `CVE-2023-32681` was marked as **resolved**

**📸 Screenshot Placeholder**




<img width="1053" height="547" alt="image" src="https://github.com/user-attachments/assets/5dc6b0b4-8bf9-4a6d-863d-71dde3a71c26" />

---

## What I Learned

From this lab, I gained important hands-on security knowledge:

* How to activate and configure Amazon Inspector
* How automated vulnerability scanning works for Lambda functions
* How to analyze CVE-related findings and understand risk impact
* How to remediate vulnerabilities by updating dependencies
* How re-scanning validates successful remediation
* Best practices for continuous monitoring and secure Lambda development

This lab strengthened my practical experience with **serverless security** and vulnerability management in AWS.

---

## Additional Resources

* AWS Inspector Documentation
* Lambda Security Best Practices
* National Vulnerability Database (NVD)
* AWS Well-Architected Security Pillar

---
