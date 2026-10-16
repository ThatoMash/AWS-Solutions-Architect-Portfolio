# Lab: Introduction to AWS Identity and Access Management (IAM)

##  Project Overview
In this lab, I acted as a Cloud Administrator to manage access control for a business environment. I moved away from a "single login" approach to implement a secure, identity-driven system. My work focused on creating a custom password policy, organizing users into functional groups, and validating permissions to ensure the **Principle of Least Privilege**.

##  Lab Objectives
* I created and applied a custom IAM password policy.
* I audited and explored pre-created IAM users and groups.
* I inspected JSON-based IAM policies (Managed and Inline).
* I implemented Role-Based Access Control (RBAC) by adding users to groups.
* I validated security boundaries by testing service access as different IAM users.

---

##  IAM Architecture & Business Scenario
I configured the environment to support specific job functions across three different users.

<img width="774" height="377" alt="image" src="https://github.com/user-attachments/assets/5a5b7a66-c0df-4750-8f40-29dc83bab7b9" />


| User | Group Assignment | Permission Logic |
| :--- | :--- | :--- |
| **user-1** | `S3-Support` | Read-only access to Amazon S3 |
| **user-2** | `EC2-Support` | Read-only access to Amazon EC2 |
| **user-3** | `EC2-Admin` | View, Start, and Stop EC2 instances |

---

##  Step-by-Step Implementation

### Task 1: Creating an Account Password Policy
I strengthened the account security by implementing a custom password policy. I updated the minimum password length to **10 characters** and enforced complexity requirements.


<img width="1364" height="570" alt="image" src="https://github.com/user-attachments/assets/430ccd2c-6f6a-4deb-b88e-6d6f909b31c0" />


### Task 2: Exploring Users and User Groups
I audited the existing identities to understand the baseline permissions. I specifically inspected the JSON policy for the Admin group to understand the allowed API actions.

IAM Groups List

<img width="1365" height="300" alt="image" src="https://github.com/user-attachments/assets/92a1bec3-ac58-41d9-ae21-87b341e5a54e" />

JSON Policy Structure

<img width="1365" height="572" alt="image" src="https://github.com/user-attachments/assets/ee408f92-7611-4046-96f9-1d5ae339fea6" />


### Task 3: Adding Users to User Groups
I assigned users to their respective groups so they would inherit the necessary permissions via RBAC (Role-Based Access Control).

User Group Membership

 Addiing User 1 to S3 Support
 
<img width="1361" height="314" alt="image" src="https://github.com/user-attachments/assets/5ca87ca5-58be-41ea-bd89-26dc926f602f" />

Adding User 2 to Ec2 Support

<img width="1346" height="318" alt="image" src="https://github.com/user-attachments/assets/a8107415-ae10-4971-868d-04486785af2b" />

Adding user 3 to Ec2 Admin Gtroup

<img width="1365" height="310" alt="image" src="https://github.com/user-attachments/assets/13be9596-5b01-4b6b-9b1e-3a7d54a13d55" />


### Task 4: Signing In and Testing User Permissions
I used the IAM Sign-in URL to log in as each user and verify the "Blast Radius" of their permissions.

* **Testing user-1:** I confirmed I could view S3 buckets but was blocked from EC2.

S3 Success
<img width="1365" height="454" alt="image" src="https://github.com/user-attachments/assets/01eb9ca3-c3c7-4e54-907f-a7a33f02122d" />

EC2 Denied

<img width="1365" height="554" alt="image" src="https://github.com/user-attachments/assets/7ad5ec8f-32af-40f3-a6dc-43be7930e213" />


* **Testing user-2:** I verified I could view EC2 instances, but I was unauthorized to stop them.
* 
  EC2 Read Only

  <img width="1365" height="241" alt="image" src="https://github.com/user-attachments/assets/07eaf07e-dff5-471f-b3c4-cec8bbdfa09e" />

Stop Action Denied

<img width="1365" height="563" alt="image" src="https://github.com/user-attachments/assets/00ce8579-e864-4176-97ab-a45a605746bd" />

 S3 Denied

<img width="1363" height="486" alt="image" src="https://github.com/user-attachments/assets/b10435f6-cc29-445f-bf9d-370a915e1c06" />


 
* **Testing user-3:** As the administrator, I successfully performed the "Stop Instance" action.
* 
  Stop Action Success

<img width="1363" height="316" alt="image" src="https://github.com/user-attachments/assets/69c7e74f-68b7-4f59-ad5c-91bf5a01cee2" />

<img width="1365" height="569" alt="image" src="https://github.com/user-attachments/assets/5633a8ca-26a1-4fd4-9b89-0b0bd291292f" />


---
