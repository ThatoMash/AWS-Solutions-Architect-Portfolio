# AWS CloudTrail Lab – Café Website Investigation

## Overview
In this lab, I created an **AWS CloudTrail** trail to audit actions taken in my AWS account. I then acted as a security detective to investigate a simulated hack on the Café website. By analyzing logs using **grep, the AWS CLI, and Amazon Athena**, I identified the intruder, determined how they compromised the security group, and remediated the vulnerabilities.

This activity demonstrated the critical importance of logging and monitoring in cloud environments to maintain security and operational integrity.

---

## Lab Architecture
The lab environment consisted of an **EC2 Web Server** hosting the Café application. I configured **CloudTrail** to log API events to an **S3 bucket**, and used **Athena** to query those logs to identify the "chaos" user responsible for the breach.

<img width="884" height="430" alt="image" src="https://github.com/user-attachments/assets/bc609547-a029-4db8-9098-5b93d3e01846" />

---

## Lab Tasks

### 1️⃣ Modify Security Group and Observe Website
I began by accessing the **EC2 Console** to configure the **Café Web Server**. I verified the existing security group rules and added a new inbound rule to allow **SSH (Port 22)** access only from my specific IP address (`My IP`). 

After saving the rules, I navigated to the website's public IP address to confirm that the Café website was running normally and displaying the correct images.

**Screenshot Placeholder**
<img width="1356" height="564" alt="image" src="https://github.com/user-attachments/assets/f730078f-c37f-4c5d-a63e-fbc5caaaab75" />
<img width="1359" height="562" alt="image" src="https://github.com/user-attachments/assets/7d220ab1-fdba-4afb-95e6-b5c4c471276d" />
<img width="1361" height="558" alt="image" src="https://github.com/user-attachments/assets/0cc31d83-1558-402b-9f0d-1f1e5902f4d4" />
<img width="830" height="497" alt="image" src="https://github.com/user-attachments/assets/7e17f895-050f-48fe-848d-5ce1995cad06" />

---

### 2️⃣ Create a CloudTrail Trail and Observe the Hack
To enable auditing, I navigated to the **CloudTrail Console** and created a new trail named `monitor`. I configured it to store logs in a new **S3 bucket** named `monitoring####`.

Shortly after enabling the trail, I refreshed the Café website and noticed it had been hacked—the main image was altered. I immediately checked the EC2 security group and discovered a new, unauthorized rule allowing **SSH access from anywhere (0.0.0.0/0)**. This confirmed that an intruder had modified the security settings.

**Screenshot Placeholder**
<img width="1348" height="557" alt="image" src="https://github.com/user-attachments/assets/a92dd78f-6bb2-4e41-875f-336204bf132d" />

---

### 3️⃣ Analyze CloudTrail Logs using Grep and AWS CLI
To investigate the breach, I connected to the web server via SSH and downloaded the CloudTrail logs from S3 to a local directory named `ctraillogs`.

```bash
mkdir ctraillogs
cd ctraillogs
aws s3 cp s3://monitoring####/ . --recursive
gunzip *.gz
