# AWS Cloud Infrastructure Monitoring & Compliance Project



##  Project Overview
In modern cloud environments, observability and compliance are critical for maintaining system uptime and security posture. This project focuses on implementing a robust monitoring solution for EC2 infrastructure.

Using **Amazon CloudWatch**, **AWS Systems Manager**, and **AWS Config**, I architected a solution to capture system-level metrics, analyze application logs in real-time, and automatically audit infrastructure for compliance deviations.

###  Architecture
<img width="668" alt="Architecture Diagram" src="https://github.com/user-attachments/assets/d22d6bf3-f37d-4f45-9012-ce68237db78f" />

---

##  Tech Stack & Services Used
* **Compute:** Amazon EC2 (Web Servers)
* **Automation:** AWS Systems Manager (Run Command, Parameter Store)
* **Observability:** Amazon CloudWatch (Logs, Metrics, Alarms, Events)
* **Notifications:** Amazon SNS
* **Compliance:** AWS Config

---

##  Project Tasks & Accomplishments

### Task 1: Installing the CloudWatch Agent
**What I did:**
I successfully installed and configured the CloudWatch Unified Agent on EC2 instances to enable deeper visibility into system performance.
* I used **AWS Systems Manager Run Command** to automate the installation across the web server fleet, eliminating manual SSH work.
* I stored the agent configuration in the **SSM Parameter Store** to ensure consistent settings for metrics and logs.

**Implementation Screenshots:**
<img width="1353" alt="SSM Run Command" src="https://github.com/user-attachments/assets/75e5856e-4b09-4793-89c0-897c3f67ab54" />
<img width="1359" alt="SSM Success" src="https://github.com/user-attachments/assets/33e6e27a-92de-4bc5-b0d9-2b5b0f6ba2b4" />
<img width="1359" alt="Agent Running" src="https://github.com/user-attachments/assets/b0bbbcc2-218a-4a33-b0d3-933103867ad4" />

---

### Task 2: Monitoring Application Logs
**What I did:**
I configured CloudWatch Logs to ingest real-time data from the web server's access and error logs.
* I created a **Metric Filter** specifically to track HTTP 404 errors.
* I set up a **CloudWatch Alarm** that triggers an SNS email notification if the error count exceeds 5 in one minute, ensuring rapid response to potential application issues.

**Implementation Screenshots:**
*Log Groups & Metric Filters:*
<img width="1358" alt="Metric Filter Setup" src="https://github.com/user-attachments/assets/50a457db-c2aa-4cfc-8ea9-382654fa7f14" />

*Alarm Configuration:*
<img width="1354" alt="Alarm Condition" src="https://github.com/user-attachments/assets/9c06115a-7cb5-4d15-b077-107b89574a39" />
<img width="1360" alt="Alarm Actions" src="https://github.com/user-attachments/assets/a659f86b-4580-47cf-b8ff-93637fd57ea7" />
<img width="1359" alt="Alarm Review" src="https://github.com/user-attachments/assets/886bfc2d-c0a9-45de-93e2-db2eee836cbc" />

*Testing & Alerts:*
<img width="1355" alt="Alarm Graph" src="https://github.com/user-attachments/assets/84b47ff2-e0f2-417f-9bb3-b8975d0404a6" />
<img width="1365" alt="Email Notification" src="https://github.com/user-attachments/assets/69f4e482-c45d-4f9f-91ed-5cc1c2bb8d39" />
<img width="673" alt="SNS Email" src="https://github.com/user-attachments/assets/d09fdf84-ac93-48b2-8303-04c649a7bded" />
<img width="1348" alt="Testing 404 Page" src="https://github.com/user-attachments/assets/47bb4b80-765d-45f8-8926-9f7a62697287" />

---

### Task 3: Monitoring Instance Metrics
**What I did:**
I extended default monitoring capabilities to capture OS-level metrics that are not available out-of-the-box.
* I configured the agent to track **Memory Usage** and **Disk Utilization**, giving me a complete view of the instance's health.
* I verified these metrics in the CloudWatch dashboard to ensure data accuracy.

**Implementation Screenshots:**
<img width="1357" alt="EC2 Monitoring Tab" src="https://github.com/user-attachments/assets/cef80809-82b1-4bfc-a1cf-a2205398e42d" />
<img width="1363" alt="CloudWatch Metrics" src="https://github.com/user-attachments/assets/81936214-7f9f-4a84-a97e-9b678f8d7d81" />

---

### Task 4: Creating Real-Time Notifications
**What I did:**
I built an event-driven notification system to alert the operations team about critical infrastructure changes.
* I created an **EventBridge Rule** to detect EC2 state changes (specifically `stopped` or `terminated`).
* I routed these events to an **SNS Topic**, ensuring that I receive an immediate email whenever a production server goes offline.

---

### Task 5: Monitoring for Infrastructure Compliance
**What I did:**
I implemented governance rules to ensure the environment remains secure and cost-efficient.
* I deployed **AWS Config rules** to automatically check for unattached EBS volumes (cost optimization).
* I set up compliance checks to verify that all EC2 instances possess the required project tags.

---

##  Key Takeaways
* **Operational Excellence:** Automated the installation of monitoring agents, removing manual overhead.
* **Observability:** Transformed raw log data into real-time alerts, reducing potential Mean Time to Detect (MTTD) for application errors.
* **Cost & Compliance:** Utilized AWS Config to proactively identify wasted resources (unattached volumes) and enforce tagging standards.
