# AWS EC2 Performance Monitoring & Incident Response Pipeline


##  Executive Summary
In enterprise cloud environments, "silent failures" are a major risk to business continuity. If a server becomes overloaded without notifying the operations team, it can lead to application downtime and revenue loss.

**This project addresses that risk by building a proactive observability pipeline.**

Instead of manually checking server health, I engineered an automated system using **Amazon CloudWatch** and **Amazon SNS**. The system continuously monitors compute resources, detects anomalies (High CPU), and autonomously triggers alerts to administrators. This reduces the **Mean Time to Detect (MTTD)** from hours to seconds.

---

##  System Workflow
The pipeline follows a standard event-driven monitoring architecture:
1.  **Data Collection:** EC2 instance generates raw performance data (CPU Usage).
2.  **Aggregation:** CloudWatch aggregates this data into 1-minute metrics.
3.  **Evaluation:** A CloudWatch Alarm evaluates the metric against a static threshold (60%).
4.  **Action:** If the threshold is breached, the Alarm publishes a message to an SNS Topic.
5.  **Notification:** SNS fans out the message to subscribed endpoints (Email), alerting the engineer.

---

##  Technical Implementation

### Task 1: Configuring the Notification Backbone (Amazon SNS)
**Objective:** Establish a decoupled messaging channel to handle alerts.

**Technical Explanation:**
Directly hardcoding email addresses into monitoring tools isn't scalable. By using **Simple Notification Service (SNS)**, I created a "Pub/Sub" topic. This allows the monitoring system to publish alerts without needing to know *who* is listening, making the architecture flexible for future integrations (e.g., sending alerts to Slack or PagerDuty later).

**What I Did:**
* Created a Standard SNS Topic named `MyCwAlarm`.
* Configured an Email Subscription to route critical alerts to my inbox.
* Verified the endpoint to ensure the handshake between AWS and the email provider was successful.

**Evidence:**

<img width="1358" alt="Subscription Setup" src="https://github.com/user-attachments/assets/2f9ce1d8-55d4-4f31-9b2a-dffa5b7e4894" />
<img width="1348" alt="Subscription Confirmed" src="https://github.com/user-attachments/assets/07197682-a4c3-4af8-91fd-8f98af7b0997" />

---

### Task 2: Defining Metric Thresholds & Alarms
**Objective:** Automate the detection of performance anomalies.

**Technical Explanation:**
Metrics alone are just data; **Alarms** turn data into actionable intelligence. I chose the `CPUUtilization` metric because it is a leading indicator of server overload. I set the period to **1 minute** to ensure high-resolution monitoring, allowing the team to react to spikes immediately rather than waiting for 5-minute averages.

**What I Did:**
* Selected the `CPUUtilization` metric from the EC2 namespace.
* Defined a static threshold of **> 60%**.
* Configured the "ALARM" state trigger to publish a message to the `MyCwAlarm` SNS topic.

**Evidence:**
*Metric Configuration:*

<img width="1365" alt="Threshold Logic" src="https://github.com/user-attachments/assets/7d193432-836c-4a3b-b143-c92c1fa9ba43" />

*Alarm Logic:*
<img width="1364" alt="SNS Action Link" src="https://github.com/user-attachments/assets/2cd348bb-1e0a-41e3-9538-b44d977c126f" />
<img width="1365" alt="Naming the Alarm" src="https://github.com/user-attachments/assets/2a4b1f52-fbbd-4ca1-8ea4-adcb9453260a" />
<img width="1358" alt="Review Configuration" src="https://github.com/user-attachments/assets/8df1ab1a-fb5f-41fd-bdf3-351bf5cbb278" />
<img width="1359" alt="Success Message" src="https://github.com/user-attachments/assets/46ec47ba-9243-451d-9af0-d92c30f58957" />
<img width="1365" alt="Initial OK State" src="https://github.com/user-attachments/assets/cb186390-06ed-426e-bab2-1f420f0901e9" />

---

### Task 3: Stress Testing & Validation
**Objective:** Validate the reliability of the alert pipeline under simulated production load.

**Technical Explanation:**
A monitoring system is unproven until it is tested. To simulate a "noisy neighbor" or a sudden traffic spike, I utilized the Linux `stress` utility. This tool spawns worker threads that consume CPU cycles, forcing the hypervisor to report high utilization to CloudWatch.

**What I Did:**
* Connected to the instance via SSH.
* Executed `sudo stress --cpu 10 --timeout 400s` to saturate the vCPUs.
* **Result:** The CloudWatch Alarm correctly transitioned from `OK` to `ALARM` state, verifying the pipeline works.

**Evidence:**
<img width="1346" alt="Alarm Triggered Graph" src="https://github.com/user-attachments/assets/b146da66-9763-42f2-9dfd-dd8f35243dae" />

---

### Task 4: Data Visualization (Dashboards)
**Objective:** Provide a "Single Pane of Glass" for infrastructure health.

**Technical Explanation:**
While alarms are good for immediate notification, dashboards are essential for **trend analysis**. By visualizing the CPU spike over time, an engineer can determine if the issue was a momentary blip or a sustained attack.

**What I Did:**
* Created a custom CloudWatch Dashboard (`LabEC2Dashboard`).
* Added line widgets to track CPU history, allowing for easy correlation between the stress test timestamp and the metric spike.

**Evidence:**
<img width="1346" alt="Dashboard Creation" src="https://github.com/user-attachments/assets/ab2c36a0-8134-4109-b760-7f9e778c0ebd" />
<img width="1365" alt="Final Dashboard View" src="https://github.com/user-attachments/assets/883037b3-8984-421a-8a28-59708a477188" />

---

## 💡 Skills Demonstrated
* **Infrastructure Monitoring:** Deep understanding of AWS CloudWatch Metrics and Alarms.
* **Incident Response:** Setting up automated notification pathways using SNS.
* **Chaos Engineering:** Using `stress` tools to validate system behavior under load.
* **Operational Visibility:** Creating dashboards to visualize real-time infrastructure performance.
