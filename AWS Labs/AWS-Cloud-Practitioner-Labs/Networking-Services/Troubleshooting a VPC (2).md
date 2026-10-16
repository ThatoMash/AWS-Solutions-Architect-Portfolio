# Troubleshooting a VPC (VPC Flow Logs)

## Introduction
In this lab, I worked through a hands-on troubleshooting scenario focused on Amazon Virtual Private Cloud (VPC). The goal was to identify and resolve networking issues that prevented access to an EC2 web server, while also learning how to create and analyze VPC Flow Logs for deeper visibility into network traffic.

This lab closely mirrors real-world cloud support and networking troubleshooting tasks, where multiple layers (security groups, route tables, and network ACLs) must work together correctly.

---

## Overview
The environment consisted of two VPCs:
- **VPC1** hosting a café web server EC2 instance in a public subnet
- **A separate VPC** hosting a CLI Host EC2 instance used for AWS CLI-based troubleshooting

I used AWS CLI commands exclusively (where possible) to investigate connectivity issues, create VPC Flow Logs, and analyze rejected traffic.

**Key focus areas:**
- VPC Flow Logs creation and analysis
- Network troubleshooting using AWS CLI
- Understanding how security groups, route tables, and network ACLs interact

---

## Architecture
The architecture included the following components:
- Two VPCs
- Public subnet hosting a web server EC2 instance
- Internet Gateway
- Route tables
- Security groups and network ACLs
- S3 bucket for storing VPC Flow Logs
- CLI Host EC2 instance for AWS CLI access

 **Architecture Diagram**  
<img width="834" height="413" alt="image" src="https://github.com/user-attachments/assets/ea21360e-c508-4267-b756-009fa92b94cc" />


---

## Objectives
By completing this lab, I was able to:
- Create and configure VPC Flow Logs
- Troubleshoot EC2 connectivity issues
- Diagnose routing, security group, and network ACL misconfigurations
- Analyze VPC Flow Log data using Linux command-line tools

---

## Tools & Services Used
- Amazon VPC
- Amazon EC2
- VPC Flow Logs
- Amazon S3
- AWS CLI
- EC2 Instance Connect
- Linux utilities (`nmap`, `grep`, `gunzip`, `date`)

---

## Lab Steps

### 1. Connecting to the CLI Host
I connected to the CLI Host EC2 instance using **EC2 Instance Connect** and configured the AWS CLI with the provided credentials and default region (`us-west-2`). This instance was used for all troubleshooting tasks.

📸 **CLI Host Connection Placeholder**  

<img width="1357" height="398" alt="image" src="https://github.com/user-attachments/assets/bdfdad81-358d-48ed-a6dc-7739cffd283b" />
<img width="1363" height="381" alt="image" src="https://github.com/user-attachments/assets/eb94f65c-edd3-477c-89fe-fe3f089b7d21" />

---

### 2. Creating VPC Flow Logs
I created an S3 bucket to store flow log data and then enabled VPC Flow Logs on **VPC1** to capture **ALL** IP traffic.

Steps included:
- Creating an S3 bucket
- Identifying the VPC ID
- Creating a flow log targeting the S3 bucket
- Verifying the flow log status was **ACTIVE**

 **VPC Flow Logs Creation Placeholder**  

<img width="1365" height="107" alt="image" src="https://github.com/user-attachments/assets/04ef055e-4c51-4010-80cf-d3712269eabf" />

VPC ID
<img width="1348" height="184" alt="image" src="https://github.com/user-attachments/assets/70a8fe8d-73d3-4b2d-8f6b-2a245c495f1e" />

FLOWLOG
<img width="1354" height="141" alt="image" src="https://github.com/user-attachments/assets/9eb56bfd-5c53-45b2-bdc6-a17cc0d2a5cd" />

FLOW LOG STATUS (ACTIVE)
<img width="1363" height="320" alt="image" src="https://github.com/user-attachments/assets/23af60a6-dad7-4807-89fa-6738b8f2a1c3" />


---

### 3. Troubleshooting Connectivity Issues

#### Issue 1: Website Not Loading
When I attempted to access the web server using its public IP address, the page failed to load.

**What I investigated:**
- Verified the EC2 instance was running
- Scanned open ports using `nmap`
- Reviewed security group inbound rules
- Inspected the route table associated with the public subnet

**Root Cause:**
The route table for the public subnet was missing a route to the Internet Gateway.


**Resolution:**
I added a route (`0.0.0.0/0`) pointing to the Internet Gateway. After this fix, the webpage loaded successfully and displayed:

<img width="1359" height="86" alt="image" src="https://github.com/user-attachments/assets/7b9ef96e-da5c-4ae9-8a4a-77602d465288" />

> **"Hello From Your Web Server!"**

<img width="1365" height="158" alt="image" src="https://github.com/user-attachments/assets/0c7c1cde-a2ef-4ea2-bc37-f118b791439f" />


 **Web Server Success**  

INSTANCE RUNNING
<img width="1363" height="374" alt="image" src="https://github.com/user-attachments/assets/7b268a9e-100a-4f84-833a-e4fd4795e932" />
<img width="1365" height="290" alt="image" src="https://github.com/user-attachments/assets/cd38d1a3-8587-4381-86a1-e74120787542" />


---

#### Issue 2: SSH Access Still Failing
Even after fixing web access, SSH connections using EC2 Instance Connect continued to fail.

**What I investigated:**
- Verified port 22 was allowed in the security group

  <img width="1365" height="461" alt="image" src="https://github.com/user-attachments/assets/f9485680-eaed-451d-9a79-f4dc9afdf1c1" />

- Checked Network ACL rules associated with the subnet
  
**Root Cause:**
A Network ACL rule was explicitly **blocking inbound SSH (port 22)** traffic.
<img width="1355" height="399" alt="image" src="https://github.com/user-attachments/assets/fc57e079-93f8-414b-8977-f5e2ce6214f8" />


**Resolution:**
I deleted the restrictive NACL entry. After this change, I successfully connected to the instance via EC2 Instance Connect and confirmed the hostname as `web-server`.

<img width="1232" height="82" alt="image" src="https://github.com/user-attachments/assets/bb1ab370-f7b5-408e-a1ba-e755fc589687" />

 **SSH Access**  

<img width="1365" height="561" alt="image" src="https://github.com/user-attachments/assets/8d2138f5-c2eb-42cd-851b-c465a6b4812a" />

---

## Analyzing VPC Flow Logs

### Downloading Logs
I downloaded the VPC Flow Logs from the S3 bucket to the CLI Host and extracted the compressed `.gz` files for analysis.

### Log Analysis
Using `grep`, I analyzed the logs to:
- Identify **REJECT** traffic
- Filter failed SSH attempts on port 22
- Match rejected traffic to my public IP address
- Confirm the elastic network interface ID matched the web server instance

I also converted Unix timestamps into human-readable format to verify the timing of rejected connections.

 **Flow Log Analysis Placeholder**  

<img width="1345" height="268" alt="image" src="https://github.com/user-attachments/assets/8fbb7746-a504-4b13-9d5f-65ade2fec747" />


grep Reject

<img width="1365" height="280" alt="image" src="https://github.com/user-attachments/assets/e4bf1ee6-5e39-4b30-9d17-298d0ad606bd" />






---

## Key Learnings
- VPC Flow Logs are extremely valuable for diagnosing network issues
- Security groups, route tables, and NACLs must all be configured correctly
- Network ACLs can silently block traffic even when security groups allow it
- AWS CLI is a powerful troubleshooting tool in real-world cloud environments

---

## Conclusion
This lab strengthened my understanding of AWS networking fundamentals and reinforced a structured approach to troubleshooting cloud connectivity issues. By combining VPC Flow Logs with hands-on investigation, I was able to confidently identify and resolve layered network problems.

This experience reflects real-world cloud support and operations tasks and has significantly improved my confidence in troubleshooting AWS VPC environments.

---

✅ **Lab Status: Completed Successfully**

