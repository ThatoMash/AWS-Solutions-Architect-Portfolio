# AWS Systems Manager Lab - Demonstration

## Introduction

This repository showcases my hands-on work with AWS Systems Manager, a service that enables centralized management, automation, and secure access to AWS resources. In this lab, I focused on:

Collecting inventory from EC2 instances without needing SSH.
Installing and configuring applications remotely.
Managing application settings dynamically using Parameter Store.
Accessing instances securely through Session Manager.
These tasks highlight practical skills in **Compute Services**, **Management & Governance**, and **Security & Compliance** on AWS.  

---

## Task 1: Inventory of Managed Instances

**Overview:**  
Used **Fleet Manager** to collect operating system, application, and metadata from a managed EC2 instance.  

**Outcome:**  
- Inventory successfully created and associated with the instance.  
- Able to review all installed applications and configuration settings remotely.  

**Screenshot Placeholder:**  


<img width="1358" height="592" alt="image" src="https://github.com/user-attachments/assets/c0a83a29-fb7c-4c56-b041-7083cde4c04e" />

<img width="1363" height="568" alt="image" src="https://github.com/user-attachments/assets/e5d73ee9-c15d-48c2-8f5e-50f405a9d1a6" />

<img width="1078" height="515" alt="image" src="https://github.com/user-attachments/assets/4c9290ed-6097-4484-8202-579261803165" />

<img width="1363" height="453" alt="image" src="https://github.com/user-attachments/assets/d8bc4d10-fdeb-4074-adc9-240681689240" />

<img width="1359" height="564" alt="image" src="https://github.com/user-attachments/assets/8369231c-c106-4dbd-9ed8-14896f0c4d06" />

<img width="1364" height="568" alt="image" src="https://github.com/user-attachments/assets/73baa6bf-ba30-4491-8036-cadf18b28cf5" />


## Task 2: Install Custom Web Application

<img width="799" height="411" alt="image" src="https://github.com/user-attachments/assets/96a524d6-756b-4c24-ab1e-a44fd757da67" />


**Overview:**  
Used **Run Command** to remotely install the **Widget Manufacturing Dashboard** application on an EC2 instance.  

**Outcome:**  
- Apache, PHP, AWS SDK, and the dashboard installed automatically.  
- Verified application running via public IP.  

**Screenshot Placeholder:**  


<img width="1356" height="567" alt="image" src="https://github.com/user-attachments/assets/8e67e3d0-81c2-46fd-861a-0961c30b7785" />

<img width="1365" height="578" alt="image" src="https://github.com/user-attachments/assets/71a387d5-2fd7-4442-921c-3f93a552f7ad" />

<img width="1361" height="564" alt="image" src="https://github.com/user-attachments/assets/40fd053c-226d-4649-ab38-4a6161e53071" />

<img width="1363" height="571" alt="image" src="https://github.com/user-attachments/assets/381568d3-bb44-49cd-b431-7a65cddd5be5" />

<img width="1025" height="323" alt="image" src="https://github.com/user-attachments/assets/670c5d6e-8139-4b8f-8b6b-2553d2d38bff" />


## Task 3: Manage Application Settings via Parameter Store

**Overview:**  
Created a parameter `/dashboard/show-beta-features` to enable beta features in the dashboard.  

**Outcome:**  
- Beta charts appeared when the parameter was set to `True`.  
- Verified live configuration updates in the running application.  

**Screenshot Placeholder:**  

<img width="1364" height="577" alt="image" src="https://github.com/user-attachments/assets/45ad2e09-00ab-4a4a-8300-708aab66f678" />

<img width="1365" height="319" alt="image" src="https://github.com/user-attachments/assets/7ea63c55-2c1c-48c1-9a89-d1e000a5adc2" />

<img width="1012" height="267" alt="image" src="https://github.com/user-attachments/assets/a45c4fac-2768-48ee-8ee1-f3a902ad8e04" />


## Task 4: Access Instances with Session Manager


<img width="797" height="319" alt="image" src="https://github.com/user-attachments/assets/a16314f7-6926-449f-8618-09607bdb90d5" />


**Overview:**  
Used **Session Manager** to securely access the EC2 instance without SSH.  

**Outcome:**  
- Listed application files and EC2 metadata.  
- Verified secure, auditable access to instances with IAM control.  

**Screenshot Placeholder:**  
<img width="1365" height="564" alt="image" src="https://github.com/user-attachments/assets/05e04a40-42c0-4a30-9273-82ce1eabd0b8" />
<img width="1364" height="573" alt="image" src="https://github.com/user-attachments/assets/02011939-59bf-441d-8616-fd36732ef598" />
<img width="1359" height="597" alt="image" src="https://github.com/user-attachments/assets/5fd803ee-9e63-47c0-951f-fb8cbe3cbb33" />
<img width="1353" height="603" alt="image" src="https://github.com/user-attachments/assets/5cf9d1db-6840-4ce6-98d9-a7ad0990cf7f" />


## Conclusion

This lab demonstrates how AWS Systems Manager enables **efficient, secure, and automated management of AWS resources**. Key takeaways include:  

- Performing inventory and configuration checks without manual SSH connections  
- Automating application installation across instances  
- Managing dynamic application settings via Parameter Store  
- Securely accessing instances using Session Manager with proper auditing  

These exercises reinforce skills in **Compute Services**, **Management & Governance**, and **Security & Compliance**, providing practical experience with real-world AWS management tasks.
