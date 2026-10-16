#  Working with AWS Lambda – Sales Analysis Report

##  Introduction
In this lab, I deployed and configured an **AWS Lambda–based serverless solution** that automatically generates a **daily sales analysis report**.  
The solution retrieves data from a MySQL database hosted on an Amazon EC2 LAMP instance, processes it using AWS Lambda, and delivers the report via **Amazon SNS email notifications**.

This project focuses on **SysOps and serverless configuration tasks**, allowing me to gain hands-on experience with IAM roles, Lambda layers, VPC networking, scheduled automation, and monitoring.

---

##  Lab Overview
The solution is built using the following AWS services:

- **AWS Lambda** – Serverless compute
- **Amazon EC2 (LAMP stack)** – Hosts the café MySQL database
- **AWS Systems Manager Parameter Store** – Secure storage of database credentials
- **Amazon SNS** – Email notifications
- **Amazon EventBridge (CloudWatch Events)** – Scheduled execution
- **AWS IAM** – Permissions and access control
- **Amazon CloudWatch Logs** – Monitoring and troubleshooting

---

##  Architecture Diagram

<img width="786" height="413" alt="image" src="https://github.com/user-attachments/assets/72258e63-a4cd-49ac-b247-c2a4fc8bec7a" />


---

##  Solution Flow
1. An EventBridge rule triggers the report Lambda function on a schedule.
2. The Lambda function retrieves database credentials from Parameter Store.
3. It invokes a second Lambda function to extract sales data.
4. Sales data is formatted into a report.
5. The report is published to an SNS topic.
6. SNS sends the report to the administrator via email.

---

##  Objectives
By completing this lab, I was able to:

- Apply correct **IAM policies** for Lambda-to-service communication
- Create and use a **Lambda Layer** for external Python dependencies
- Configure Lambda functions to access resources inside a **VPC**
- Automate reporting using **EventBridge schedules**
- Send notifications using **Amazon SNS**
- Troubleshoot Lambda issues using **CloudWatch Logs**

---


##  Implementation Steps

### 1️ IAM Role Configuration
I reviewed and verified IAM roles required by each Lambda function to ensure least-privilege access.

 <img width="1365" height="565" alt="image" src="https://github.com/user-attachments/assets/1c8e6169-2e45-4fdf-b7cb-ed7b24cd22e9" />

Verification roles are as follows

<img width="1365" height="197" alt="image" src="https://github.com/user-attachments/assets/fe513ae4-43a5-4b8a-83b8-f6785376568c" />

---

### 2️⃣ Lambda Layer Creation
I created a Lambda layer to package the **PyMySQL** library so it could be reused across functions.

<img width="1362" height="572" alt="image" src="https://github.com/user-attachments/assets/02ff997b-c35c-4936-9bf1-37232b2994eb" />

---

### 3️ Data Extractor Lambda Function
I deployed a Lambda function responsible for:
- Connecting to the MySQL database
- Running analytical queries
- Returning aggregated sales data

Function Creation
<img width="1365" height="566" alt="image" src="https://github.com/user-attachments/assets/cc5985b7-560c-42bc-9260-c4023972c7a1" />

Adding Lambda Function Layer

<img width="1362" height="566" alt="image" src="https://github.com/user-attachments/assets/040c253f-7858-4169-9a1a-b603db83d54c" />

<img width="1365" height="569" alt="image" src="https://github.com/user-attachments/assets/5e569814-6d18-426d-8516-216bb5b2ee1f" />

---

### 4️ Troubleshooting & Testing
The function initially timed out due to a missing **MySQL (3306) inbound rule** on the database security group.  
After correcting the security group configuration, the function executed successfully.
 

 TESTING

<img width="1357" height="563" alt="image" src="https://github.com/user-attachments/assets/beacf03d-7d72-4775-8587-bb0222e79e70" />

 **TroubleShooting**

 adding the inbound rule

<img width="1364" height="421" alt="image" src="https://github.com/user-attachments/assets/d5693619-8c85-4381-a896-55b3400fe621" />

 <img width="1354" height="569" alt="image" src="https://github.com/user-attachments/assets/56f40456-03f1-4330-a217-37a49d576d23" />

---

### 5️ SNS Topic & Email Subscription
I created an SNS topic and subscribed an email address to receive the daily sales reports.

 <img width="1365" height="484" alt="image" src="https://github.com/user-attachments/assets/5339d9fd-13b7-40b1-a7e3-dc10e3197d9c" />

 <img width="1365" height="572" alt="image" src="https://github.com/user-attachments/assets/227d98f6-bd29-44a8-8f86-a6f759475e56" />

 
 Enail Confirmation

 <img width="1365" height="454" alt="image" src="https://github.com/user-attachments/assets/7ddfa965-9d0f-4da7-889c-5c043edfb711" />


---

### 6️ Sales Report Lambda Function
I created the main Lambda function using the **AWS CLI**.  
This function orchestrates the reporting process and publishes results to SNS.

 Sales-report-lambda.

<img width="1365" height="321" alt="image" src="https://github.com/user-attachments/assets/a2899ca3-10d3-417a-9faf-efed66072e52" />

 Lambda create-function command to create the Lambda function and configure it to use the salesAnalysisReportRole IAM role

 <img width="1364" height="369" alt="image" src="https://github.com/user-attachments/assets/54729e3b-bf8d-402a-b5d7-6512c700c17d" />
<img width="1360" height="215" alt="image" src="https://github.com/user-attachments/assets/37df8d15-cb1f-48b3-9061-43ebe2b71290" />

<img width="1365" height="607" alt="image" src="https://github.com/user-attachments/assets/fa71f023-4935-412f-b12b-da0edd6ef896" />

---

### 7️ Scheduled Automation
I configured an **EventBridge cron rule** to trigger the report **Monday through Saturday at 8 PM (UTC)**.

 <img width="1365" height="570" alt="image" src="https://github.com/user-attachments/assets/68675b05-922f-421f-ba39-851f05c849d1" />

<img width="1363" height="435" alt="image" src="https://github.com/user-attachments/assets/5df2735d-aed9-465d-af1a-3c069fefbcda" />

---

##  Final Outcome
This lab demonstrates a fully automated **serverless reporting solution** built on AWS.  
It strengthened my understanding of **Lambda orchestration, IAM permissions, VPC networking, monitoring, and event-driven automation**.

---

##  Conclusion
This project shows how AWS serverless services can be combined to automate real-world business workflows efficiently and securely without managing servers.

---


