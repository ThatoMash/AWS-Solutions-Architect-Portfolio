# Data Protection Using AWS KMS Encryption

## Overview
This lab demonstrates how I implemented data encryption and decryption using **AWS Key Management Service (KMS)** and the **AWS Encryption CLI**. I learned how to protect sensitive data by transforming plaintext into ciphertext using symmetric encryption keys, gaining hands-on experience with cloud security fundamentals.

By completing this lab, I successfully created an AWS KMS encryption key, installed and configured the AWS Encryption CLI, and encrypted and decrypted files to verify data integrity.

---

## Objectives
After completing this lab, I was able to:
* Create an AWS KMS encryption key.
* Install and configure the AWS Encryption CLI.
* Encrypt plaintext files into ciphertext.
* Decrypt ciphertext back to plaintext.

---

## Lab Tasks

### 1️⃣ Create an AWS KMS Key
I began by navigating to the **AWS KMS Console** to create a symmetric encryption key. I configured the key settings with the alias `MyKMSKey` and the description "Key used to encrypt and decrypt data files." I assigned the key administrators and usage permissions to the `voclabs` user and copied the **Key ARN** for use in later steps.

**Screenshot Placeholder**
<img width="1346" height="517" alt="image" src="https://github.com/user-attachments/assets/7d9e249b-f161-4628-a997-50412d282318" />
<img width="1364" height="565" alt="image" src="https://github.com/user-attachments/assets/170012f7-d8f3-4f43-b0a9-e434d35763f7" />
<img width="1348" height="573" alt="image" src="https://github.com/user-attachments/assets/7c54998f-17e7-46ce-b420-81fec86d0c25" />
<img width="1365" height="571" alt="image" src="https://github.com/user-attachments/assets/8b0a9238-6fce-49e7-908d-ecbbd05dff32" />
<img width="1363" height="424" alt="image" src="https://github.com/user-attachments/assets/a740a21f-df04-4988-bb73-e9c09451c73a" />
<img width="1352" height="571" alt="image" src="https://github.com/user-attachments/assets/6a843726-3400-4d7e-a646-fcd8651e78e6" />

---

### 2️⃣ Configure the File Server Instance

#### Connect to the EC2 Instance
I navigated to the **EC2 Console** and selected the **File Server** instance. Instead of using SSH keys, I securely connected via **Session Manager**.

**Screenshot Placeholder**
<img width="1365" height="559" alt="image" src="https://github.com/user-attachments/assets/9c8414f6-a9b6-4685-9055-464aa81f3376" />
<img width="1365" height="575" alt="image" src="https://github.com/user-attachments/assets/45bf7990-a920-4db0-ab22-54b67be988d9" />
<img width="1358" height="400" alt="image" src="https://github.com/user-attachments/assets/2fb3bd51-c545-4061-9943-d2ad0d5c826d" />

#### Configure AWS Credentials
Once connected, I initialized the AWS configuration using the `aws configure` command. I edited the `~/.aws/credentials` file to ensure the instance had the correct access keys to interact with the KMS service.

**Screenshot Placeholder**
<img width="1363" height="183" alt="image" src="https://github.com/user-attachments/assets/7b3e3488-b398-4e0b-8801-a894325770ef" />
<img width="1359" height="190" alt="image" src="https://github.com/user-attachments/assets/dedf459e-185f-489f-9f73-998cc7ea7b0e" />

#### Install AWS Encryption CLI
To perform the encryption operations, I installed the **AWS Encryption CLI** using `pip3` and exported the path to ensure the tools were executable from the command line.

**Screenshot Placeholder**
<img width="1363" height="601" alt="image" src="https://github.com/user-attachments/assets/73ec2230-295a-42e6-8832-df1d2ef72264" />
<img width="1362" height="225" alt="image" src="https://github.com/user-attachments/assets/82448cfe-cd99-4d8c-b921-29de15be81f6" />

---

### 3️⃣ Encrypt and Decrypt Data

#### Set Up Encryption Environment
I created three dummy files (`secret1.txt`, etc.) containing "TOP SECRET" text. I set up the environment by creating an output directory and assigning my KMS Key ARN to a variable.

**Screenshot Placeholder**
<img width="558" height="155" alt="image" src="https://github.com/user-attachments/assets/6f19e52a-08ea-4d38-b89f-ef3c0613b40f" />

#### Perform Encryption and Decryption
I used the `aws-encryption-cli` to encrypt the plaintext file using my KMS key and an encryption context (`purpose=test`). After verifying the file was encrypted, I successfully decrypted it back to plaintext to confirm the process worked as expected.

**Screenshot Placeholder**
<img width="1356" height="227" alt="image" src="https://github.com/user-attachments/assets/37c05388-e1d1-49a5-a0a8-745731b8176c" />

---

## What I Learned
Through this lab, I gained hands-on experience with **symmetric encryption** on AWS. I learned how to:

* **Create and Manage Keys:** I successfully created a symmetric key in AWS KMS and defined usage permissions.
* **Secure Data:** I used the AWS Encryption CLI to transform readable plaintext into secure ciphertext.
* **Verify Integrity:** I decrypted the data back to its original form, validating the full encryption lifecycle.
* **Follow Best Practices:** I utilized encryption contexts and commitment policies to ensure a high standard of security.

---

## Security Best Practices
* Always use encryption contexts for additional security.
* Store KMS key ARNs securely.
* Use IAM roles with least privilege access.
* Enable key rotation for long-term keys.
* Monitor key usage with AWS CloudTrail.

---
