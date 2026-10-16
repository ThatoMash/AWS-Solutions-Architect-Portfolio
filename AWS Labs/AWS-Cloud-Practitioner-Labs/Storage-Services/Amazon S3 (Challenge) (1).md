# Challenge Lab: Amazon S3

## Introduction
In this challenge lab, I worked with **Amazon Simple Storage Service (Amazon S3)** to create a storage bucket, upload an object, configure public access at the object level, and verify access through both a web browser and the AWS Command Line Interface (AWS CLI).

This lab focused on understanding how S3 handles object storage, permissions, and public accessibility ,skills that are essential for real-world cloud and web hosting scenarios.

---

## Lab Overview
The goal of this challenge was to complete a set of tasks using **AWS Management Console** and **AWS CLI** to demonstrate hands-on knowledge of Amazon S3.

**Key tasks included:**
- Creating an S3 bucket
- Uploading an object to the bucket
- Making the object publicly accessible
- Accessing the object via a browser
- Listing bucket contents using AWS CLI

---

## Objectives
By completing this lab, I was able to:
- Create an Amazon S3 bucket
- Upload objects to S3
- Configure object-level public access
- Access S3 objects using a web browser
- List S3 bucket contents using AWS CLI

---

## Tools & Services Used
- Amazon S3
- Amazon EC2 (CLI Host)
- AWS Management Console
- AWS Command Line Interface (AWS CLI)

---

## Lab Steps

### 1. Connecting to the CLI Host Instance
I connected to the pre-provisioned **CLI Host EC2 instance** using **EC2 Instance Connect**. This instance was used to configure AWS CLI credentials and interact with S3 programmatically.

 **CLI Host Connection**  

<img width="1365" height="329" alt="image" src="https://github.com/user-attachments/assets/95cf84bb-a346-48d3-8099-b3cd695377af" />

---

### 2. Configuring the AWS CLI
Once connected to the CLI Host, I configured the AWS CLI using the credentials provided in the lab.

Configuration details:
- **Region:** us-west-2
- **Output format:** json

This setup allowed me to run AWS CLI commands to manage S3 resources.

 **AWS CLI Configuration**  

<img width="1364" height="282" alt="image" src="https://github.com/user-attachments/assets/ca3246b7-309e-4b3f-9648-cfd0e9ae7448" />

---

### 3. Creating an S3 Bucket
Using the AWS CLI, I created a new S3 bucket with a unique name in the `us-west-2` region.

This bucket was used to store and manage objects throughout the lab.

 **S3 Bucket Creation**  

<img width="988" height="38" alt="image" src="https://github.com/user-attachments/assets/e9db47df-3d42-4e13-bfaa-f6a61beafcd1" />

---

### 4. Uploading an Object to the Bucket
After creating the bucket, I uploaded an object (sample file) into the S3 bucket using AWS CLI commands.

This object served as the content I later configured for public access.

 **Object Upload**  

<img width="1361" height="91" alt="image" src="https://github.com/user-attachments/assets/f08eb2ea-eca9-4285-b5de-ffb7ca7a108e" />

---

### 5. Accessing the Object via Browser (Initial Attempt)
I attempted to access the uploaded object using its S3 object URL in a web browser.

As expected, access was denied because the object permissions were still private by default.

 **Access Denied**  

<img width="1347" height="174" alt="image" src="https://github.com/user-attachments/assets/b7322845-8160-42ef-bcee-e6e2468d8e45" />

---

### 6. Making the Object Publicly Accessible
To resolve the access issue, I updated the **object-level permissions** to allow public read access.

Important note:
- Only the **object** was made public — the bucket itself remained private.

This step demonstrated the principle of **least privilege**.

 **Public Object Permissions**  


<img width="1359" height="561" alt="image" src="https://github.com/user-attachments/assets/4a193e51-f1f0-4490-83e4-b1ef8431562b" />


---

### 7. Accessing the Object via Browser (Successful)
After updating the permissions, I accessed the object again using a web browser.

This time, the object loaded successfully, confirming that public access was correctly configured.

 **Successful Browser Access**  

<img width="1365" height="131" alt="image" src="https://github.com/user-attachments/assets/98027037-fb71-48c9-8f2d-637af05cb1e8" />

---

### 8. Listing Bucket Contents Using AWS CLI
Finally, I listed the contents of the S3 bucket using the AWS CLI to confirm that the object was present.


 **AWS CLI List**  

<img width="1361" height="47" alt="image" src="https://github.com/user-attachments/assets/30ea7143-bf66-42f1-8bc3-c6ca78f25ec7" />

---

## Key Learnings
- S3 buckets are private by default for security
- Public access can be applied at the **object level** without exposing the entire bucket
- AWS CLI provides an efficient way to manage S3 resources
- Understanding S3 permissions is critical for secure cloud storage

---

## Conclusion
This challenge lab strengthened my understanding of Amazon S3 fundamentals, including bucket creation, object management, and permission configuration. It also reinforced the importance of secure access control while enabling public content delivery when required.

---
