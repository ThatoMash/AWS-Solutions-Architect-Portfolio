
# AWS VPC: Build a Custom VPC and Launch a Web Server

##  Project Overview

In this lab, I designed and deployed a **custom AWS Virtual Private Cloud (VPC)** with public and private subnets, routing, security groups, and a fully functional **EC2 web server**.  
The project demonstrates practical AWS networking and compute skills.

---

##  Lab Objectives

After completing this lab, I was able to:

- Create a fully functional **Virtual Private Cloud (VPC)**
- Configure **public and private subnets** across multiple Availability Zones
- Set up an **Internet Gateway** and **NAT Gateway**
- Configure **route tables** for traffic control
- Create and apply **security groups**
- Launch and configure an **EC2 web server**
- Deploy and verify a working web application

### Architecture Overview

![Architecture Diagram](https://github.com/user-attachments/assets/950f2fa8-1e51-4870-984f-f1dafde20d66)

**What I did:**  
I designed the overall VPC architecture showing public and private subnets, routing, security components, and the EC2 web server.

---

## 1️⃣ VPC Creation

- **VPC CIDR:** `10.0.0.0/16`
- **Subnets:** 2 Public and 2 Private
- **Internet Gateway:** Enabled
- **NAT Gateway:** Enabled

![VPC Creation](https://github.com/user-attachments/assets/2cfe1f8d-925c-4e1f-8b6f-88d7668914f5)

**What I did:**  
I created a custom VPC and enabled both an Internet Gateway and a NAT Gateway.

---

## 2️⃣ Subnet Configuration

| Subnet Name | Type | CIDR Block | Availability Zone |
|------------|------|------------|-------------------|
| Public Subnet 1 | Public | 10.0.0.0/24 | us-west-2a |
| Private Subnet 1 | Private | 10.0.1.0/24 | us-west-2a |
| Public Subnet 2 | Public | 10.0.2.0/24 | us-west-2b |
| Private Subnet 2 | Private | 10.0.3.0/24 | us-west-2b |

![Subnet Configuration](https://github.com/user-attachments/assets/d07227e3-dc76-4176-8c28-135ff1bc69f9)

**What I did:**  
I created and organized public and private subnets across two Availability Zones.

---

## 3️⃣ Route Table Configuration

### Public Route Table
- `0.0.0.0/0 → Internet Gateway`

![Public Route Table](https://github.com/user-attachments/assets/b5b3680b-7d70-4b54-8e8c-60478df4f4b1)

**What I did:**  
I configured the public route table to allow internet access.

### Private Route Table
- `0.0.0.0/0 → NAT Gateway`

![Private Route Table](https://github.com/user-attachments/assets/0e5d82e7-9c98-4867-b346-48d7bc3206e4)

**What I did:**  
I configured the private route table for secure outbound internet access.

---

## 4️⃣ Security Group Configuration

- **Security Group Name:** Web Security Group  
- **Inbound Rule:** HTTP (Port 80) from `0.0.0.0/0`

![Security Group](https://github.com/user-attachments/assets/a9af3706-7066-48da-94a4-b120241cc5fe)

**What I did:**  
I created a security group to allow HTTP traffic to the web server.

---

## 5️⃣ EC2 Instance & Web Server Deployment

- **Instance Type:** `t3.micro`
- **AMI:** Amazon Linux 2
- **Subnet:** Public Subnet
- **Security Group:** Web Security Group

### User Data Script

```bash
#!/bin/bash
yum install -y httpd mysql php
wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-RESTRT-1/267-lab-NF-build-vpc-web-server/s3/lab-app.zip
unzip lab-app.zip -d /var/www/html/
chkconfig httpd on
service httpd start
```

**What I did:**  
I automated web server installation and application deployment using a user data script.

![EC2 Instance Created](https://github.com/user-attachments/assets/b0067bc2-7251-4b07-a9bd-bb52a2c6a9b3)

**What I did:**  
I launched an EC2 instance inside the VPC.

![Instance Network Settings](https://github.com/user-attachments/assets/02c52a18-2acc-4d98-8daf-9a02252c498d)

**What I did:**  
I attached the instance to the public subnet and security group.

![User Data Configuration](https://github.com/user-attachments/assets/4d40b20b-c101-4123-b5ab-53c9caaea923)

**What I did:**  
I configured startup scripts to run the web server automatically.

![Instance Details](https://github.com/user-attachments/assets/12f917dc-03ae-49dd-9409-c961066723b9)

**What I did:**  
I verified instance configuration and public IP.

![Instance Running](https://github.com/user-attachments/assets/a9cf9bd7-5ad5-4e3a-9018-bb2ab96f63f7)

**What I did:**  
I confirmed the EC2 instance was running.

---

## 6️⃣ Validation and Testing

![Status Checks](https://github.com/user-attachments/assets/2ec245eb-3018-4b6e-a507-b57dab4db7f7)

**What I did:**  
I waited for EC2 status checks to pass (2/2).

![Public DNS](https://github.com/user-attachments/assets/8843cd28-f940-444d-9157-6a1029740af3)

**What I did:**  
I copied the Public IPv4 DNS.

![Web Server Success Page](https://github.com/user-attachments/assets/3c6cd647-feb2-44e9-b983-1f343de4c250)

**What I did:**  
I accessed the web server and confirmed the success page loaded.

---

##

In this project, I:

- Built a complete **AWS VPC architecture**
- Implemented **public and private networking**
- Configured **secure routing and access controls**
- Deployed and validated a **web server on Amazon EC2**


