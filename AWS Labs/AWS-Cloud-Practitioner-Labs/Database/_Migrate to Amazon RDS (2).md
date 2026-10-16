# AWS RDS Migration Lab – Café Web Application

## Overview
This lab demonstrates the migration of a **local database** to a **fully managed Amazon RDS (Relational Database Service) MariaDB instance**. During this exercise, I migrated the café web application database from a self-managed EC2 instance to a managed RDS instance, configured the necessary network and security components, and validated the application’s functionality after migration.

Through this hands-on experience, I learned how to **design and deploy secure, highly available, and scalable database environments** in AWS, while also understanding **data migration, monitoring, and connectivity best practices**.

---

## Lab Architecture

### Starting Architecture
Initially, the café web application ran on a **LAMP EC2 instance** (Linux, Apache, MySQL, PHP) in a **public subnet**, with a CLI Host for administration. Both the application and database were hosted on the same instance.

<img width="429" height="446" alt="image" src="https://github.com/user-attachments/assets/0832919c-c7b4-471c-8a71-bbd8e68f09f2" />


### Final Architecture
After the migration, the **database was moved to Amazon RDS**, deployed in **private subnets** across multiple Availability Zones. The EC2 instance now connects to the RDS instance securely via a dedicated security group.

<img width="742" height="433" alt="image" src="https://github.com/user-attachments/assets/5d9ec6a9-8571-42e9-8df7-3a84d3cc995e" />

---

## Lab Tasks

### 1️⃣ Generating Data on the Café Website
Before migrating the database, I generated sample order data on the café website. By placing several orders, I created realistic data in the local MySQL database to use for migration.

**Screenshot Placeholder**  
<img width="1081" height="55" alt="image" src="https://github.com/user-attachments/assets/699207d7-fd4a-4ffe-89a1-745ca1724d43" />


<img width="1353" height="675" alt="image" src="https://github.com/user-attachments/assets/d4d726d1-7dde-4917-906c-509e027b7132" />

On the cafe website,I choose Menu, and chose  one  each item to order, and then chose Submit Order.
<img width="868" height="596" alt="image" src="https://github.com/user-attachments/assets/2e564037-5136-4650-9255-87480f7da84c" />

I went to the Order History page, and recorde the number of orders that i placed for Later in this lab, I will compare this number with the number of orders in the migrated database.

 

<img width="863" height="384" alt="image" src="https://github.com/user-attachments/assets/47c27d31-7c55-4dc3-9f7b-0eec3e44d329" />


---

### 2️⃣ Creating the Amazon RDS Instance via AWS CLI
Using **EC2 Instance Connect**, I accessed the CLI Host to run AWS CLI commands for provisioning RDS.  

**Steps included:**
- Configuring the AWS CLI with provided credentials
- Creating prerequisite components:
  - `CafeDatabaseSG` security group
  - Two private subnets in separate Availability Zones
  - `CafeDB Subnet Group` including both private subnets
- Launching the RDS MariaDB instance (`CafeDBInstance`) with:
  - Engine: MariaDB 10.5.13
  - Instance class: db.t3.micro
  - Allocated storage: 20 GB
  - Security group: CafeDatabaseSG
  - Private subnets for high availability

**Screenshot Placeholder**  

 I Went to EC2 Management Console
<img width="1356" height="274" alt="image" src="https://github.com/user-attachments/assets/57e4855a-1b4d-4877-81e2-9d58c0ab54fd" />

<img width="1360" height="580" alt="image" src="https://github.com/user-attachments/assets/5bac13b5-f94f-4c65-be6b-95de81a3bacc" />

I connect to the EC2 Instance Connect

<img width="1364" height="518" alt="image" src="https://github.com/user-attachments/assets/a6f1ba3a-841c-4d85-a7e0-14406aac3d3e" />


I have to run the AWS configure commands 

<img width="1365" height="226" alt="image" src="https://github.com/user-attachments/assets/3fd3421e-f633-46c3-9361-db3ce7477f1f" />

<img width="471" height="87" alt="image" src="https://github.com/user-attachments/assets/869c987c-e65e-4ece-bdbd-74b423e310c5" />

 CafeDB Private Subnet 1 in the same AZ as your Cafe EC2 instance (us-west-2a
 
<img width="690" height="394" alt="image" src="https://github.com/user-attachments/assets/3623a95b-58c2-4a84-872d-72d5b90ea5f2" />

CafeDB Private Subnet 2

<img width="632" height="384" alt="image" src="https://github.com/user-attachments/assets/ccb28efe-5c5f-4dcc-836e-f14f1b1f91b8" />

DB Subnet Group for your RDS instance

<img width="615" height="404" alt="image" src="https://github.com/user-attachments/assets/e55b13a8-ecf6-495b-a39c-b00293c58636" />

creation of a MariaDB database

<img width="447" height="339" alt="image" src="https://github.com/user-attachments/assets/223412d8-823f-4cb6-aad7-62ad668a9786" />



<img width="556" height="430" alt="image" src="https://github.com/user-attachments/assets/f99d9547-5d9d-443b-aca2-f529310f79a5" />

Status of the database

BACKING UP STATUS

<img width="852" height="129" alt="image" src="https://github.com/user-attachments/assets/b9c4dc6f-a620-45c0-8840-02169b46c96d" />


AVAILABLE STATUS

<img width="902" height="160" alt="image" src="https://github.com/user-attachments/assets/2d1628ea-fc7e-451d-96af-8fa78c24e7b7" />


---
### 3️⃣ Migrating Application Data to RDS
I performed a **data migration** from the local EC2 database to the new RDS instance:

1. Connected to the Café EC2 instance via SSH.
2. Exported the local database using `mysqldump`:

  <img width="1365" height="338" alt="image" src="https://github.com/user-attachments/assets/6b98ebb4-5bc3-4372-acea-076d0ee13fa5" />

  <img width="560" height="278" alt="image" src="https://github.com/user-attachments/assets/f47ae534-70ed-4a40-a806-7ad9ddce9044" />

  <img width="1365" height="494" alt="image" src="https://github.com/user-attachments/assets/90cca6f9-4562-4d85-90ee-fb2a780d64bf" />

  <img width="530" height="193" alt="image" src="https://github.com/user-attachments/assets/a3940be8-151f-4a3e-a58f-8513c14497b4" />

  ProductS table on MariaDB
  
<img width="1106" height="176" alt="image" src="https://github.com/user-attachments/assets/6b615408-54b8-493d-b431-58e2e7e143f8" />

## Configuring the website to use the Amazon RDS instance

The café application used AWS Systems Manager Parameter Store to store the database URL. I updated the /cafe/dbUrl parameter to point to the RDS instance endpoint. After saving changes, the website successfully connected to the RDS database.

I verified the migration by checking the Order History page and confirming that all previous orders were correctly reflected in the RDS database.

<img width="1361" height="582" alt="image" src="https://github.com/user-attachments/assets/39d3ace7-a39f-41fe-9281-b49d4d2d0106" />
<img width="1361" height="556" alt="image" src="https://github.com/user-attachments/assets/504195c8-345e-48f9-9426-c0979b791968" />
<img width="1348" height="440" alt="image" src="https://github.com/user-attachments/assets/47d98196-72d6-4bee-877f-10929624f47e" />
<img width="1340" height="561" alt="image" src="https://github.com/user-attachments/assets/0fa9f916-2c88-4698-aa6e-9a126a31f804" />
<img width="875" height="589" alt="image" src="https://github.com/user-attachments/assets/65366155-eb13-4b34-bd81-06b711dad808" />

 I Chose the Order History tab. and observe the number of orders in the database. Compare this number with the number of orders that you recorded before the database migration. Both numbers should be the same

 <img width="870" height="330" alt="image" src="https://github.com/user-attachments/assets/48d1d7d8-25a4-4291-a282-1e93de384688" />

 Monitoring the Amazon RDS Database

## Amazon RDS integrates with CloudWatch, providing insights into database performance. I explored key metrics including:

CPUUtilization – percentage of CPU used
DatabaseConnections – active database connections
FreeStorageSpace – available storage
FreeableMemory – available RAM
ReadIOPS & WriteIOPS – disk read/write performance

I tested the Database Connections metric by connecting to the RDS instance and observing a single active connection, then confirmed it returned to zero after disconnecting.

Screenshot Placeholder

Opening RdS

<img width="1363" height="567" alt="image" src="https://github.com/user-attachments/assets/f95604ef-4e4e-41b2-8935-13ffb5ed11da" />

Choose Cafe Db instance

<img width="1358" height="236" alt="image" src="https://github.com/user-attachments/assets/9dfb20bb-f445-401a-9f5a-23ba6eb0a3b5" />

Go to Monitoring Tab

This tab displays a number of key database instance metrics that are available from CloudWatch. Each metric includes a graph that shows the metric as it is monitored over a specific time span.

<img width="1365" height="572" alt="image" src="https://github.com/user-attachments/assets/dd56d86e-081d-476c-a41f-c8bf5d7b4a4c" />


<img width="1362" height="594" alt="image" src="https://github.com/user-attachments/assets/6bb0da84-afdc-4c39-b938-f2d2263879d7" />



What I Learned

Through this lab, I gained practical experience in migrating a live database to AWS RDS. Specifically, I learned how to:
Provision secure RDS instances using the AWS CLI
Build private subnets and subnet groups for high availability
Configure security groups to control database access
Migrate data safely from EC2-hosted databases to RDS
Update applications to use a managed database service
Monitor RDS performance using CloudWatch metrics
This experience provided hands-on insight into database migration, connectivity management, and cloud-native monitoring, which are critical skills for modern cloud architecture.




  


  


