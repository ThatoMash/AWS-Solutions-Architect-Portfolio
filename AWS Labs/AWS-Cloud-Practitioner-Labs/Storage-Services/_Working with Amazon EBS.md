# AWS Elastic Block Store (EBS) Lifecycle & Disaster Recovery



Data persistence is the backbone of cloud infrastructure. While EC2 instances can be ephemeral, the data they process must remain secure and recoverable. 

**This project demonstrates a complete storage lifecycle management workflow on AWS.** I provisioned block storage for a Linux server, implemented file system formatting for data usage, and executed a disaster recovery strategy using EBS Snapshots. This simulation proves the ability to restore critical business data from a specific point-in-time backup to a new storage volume.

###  Architecture
<img width="919" alt="Lab Architecture" src="https://github.com/user-attachments/assets/4dea1162-89a6-48b1-964e-939dc314702e" />

---

##  Technical Implementation

### Task 1: Storage Provisioning & Attachment
**Objective:** Allocate persistent block storage to a compute instance.

**Architectural Insight:**
EBS volumes are "Availability Zone (AZ) locked." To attach a volume to an instance, both resources must reside in the same physical location (e.g., `us-east-1a`) to ensure low-latency connectivity.

**What I Did:**
* Created a General Purpose SSD (gp2) EBS volume within the same Availability Zone as my EC2 instance.
* Attached the volume to the running Linux instance as a secondary block device (`/dev/sdb`).
* Verified the attachment via the AWS Console and the Linux terminal.

**Evidence:**
*Volume Creation & Attachment:*

<img width="1362" alt="Volume Config" src="https://github.com/user-attachments/assets/ddbf7313-d40b-465c-94be-d1856d6d7d69" />
<img width="1365" alt="Volume Available" src="https://github.com/user-attachments/assets/8573965e-dc1c-49a3-940f-9144be967915" />
<img width="1362" alt="Volume In-Use" src="https://github.com/user-attachments/assets/21adc515-f47a-4e60-89d6-c876bff36106" />

*Terminal Verification:*
<img width="1364" alt="Terminal Connect" src="https://github.com/user-attachments/assets/463c08fe-25ed-4578-8f25-82fdecb64c7d" />

---

### Task 2: File System Configuration & Mounting
**Objective:** Prepare the raw block storage for data operations.

**Architectural Insight:**
A raw EBS volume is like a brand-new hard drive—it needs a file system to store data. Additionally, mounting a drive manually is temporary; modifying the `/etc/fstab` file is critical to ensure the drive automatically remounts if the server is rebooted.

**What I Did:**
* Formatted the volume with the **ext3** file system using `mkfs`.
* Created a mount point directory `/mnt/data-store` and mounted the volume.
* Configured `/etc/fstab` to ensure persistence across reboots.
* Generated test data (`file.txt`) to simulate a production workload.

**Evidence:**
<img width="1365" alt="Format and Mount" src="https://github.com/user-attachments/assets/1f7d5d33-86ea-4876-a445-4732201c82b0" />
<img width="1362" alt="Fstab Config" src="https://github.com/user-attachments/assets/7b8abb91-97ab-4863-a598-10351ad9f3a5" />
<img width="1365" alt="Verify Mount" src="https://github.com/user-attachments/assets/120f09e8-48d7-44ee-86cd-50cc5d41582f" />
<img width="1365" alt="Create Test File" src="https://github.com/user-attachments/assets/a24e205b-878b-48e8-a42d-1a8f6f589885" />

---

### Task 3: Backup Strategy (Snapshots)
**Objective:** Create a point-in-time backup for data durability.

**Architectural Insight:**
EBS Snapshots are incremental backups stored in Amazon S3. They allow you to capture the state of a volume at a specific moment. In a real-world scenario, this protects against accidental deletion or ransomware.

**What I Did:**
* Initiated a snapshot of the primary volume containing the test data.
* **Simulated Disaster:** Once the snapshot was secure, I intentionally deleted the `file.txt` from the primary volume to simulate data loss.

**Evidence:**
<img width="1365" alt="Create Snapshot" src="https://github.com/user-attachments/assets/b49682ae-e2f3-4e64-84ec-df9a1450cae7" />
<img width="1365" alt="Snapshot Completed" src="https://github.com/user-attachments/assets/850981a4-04de-4994-bb12-a69489fd1fb4" />
<img width="1356" alt="Delete File" src="https://github.com/user-attachments/assets/1e11a05f-d21e-47ee-943a-6942792ecf7a" />

---

### Task 4: Disaster Recovery & Restoration
**Objective:** Restore operations by recovering data from the snapshot.

**Architectural Insight:**
You cannot "mount" a snapshot directly. To restore data, you must hydrate a *new* EBS volume from that snapshot. This new volume is an exact replica of the original drive at the exact second the snapshot was taken.

**What I Did:**
* Created a new EBS volume (`Restored Volume`) from the snapshot.
* Attached this new volume to the instance as `/dev/sdc`.
* Mounted the restored volume to a new directory `/mnt/data-store2`.
* **Verification:** Successfully accessed `file.txt` on the restored drive, confirming the recovery was successful.

**Evidence:**
*Restoring Volume from Snapshot:*
<img width="1363" alt="Create Vol from Snap" src="https://github.com/user-attachments/assets/3f2e8f25-ce7e-4feb-8d19-be1e04b8dfea" />
<img width="1365" alt="Vol Restored Available" src="https://github.com/user-attachments/assets/257c6c48-f7fe-4f1b-ba5e-c9ef8a660b3e" />

*Attaching & Verifying Data:*
<img width="1361" alt="Attach Restored Vol" src="https://github.com/user-attachments/assets/f90cccd2-5ed2-451e-b29b-def4c355805f" />
<img width="1365" alt="Terminal Verification" src="https://github.com/user-attachments/assets/bb3c13a1-01dc-4192-8571-8e9d7c17f761" />
<img width="1350" alt="File Recovered" src="https://github.com/user-attachments/assets/2a56cd95-1430-4def-a253-5a9a7fc02cb8" />

---

##  Skills Demonstrated
* **Storage Management:** Provisioning, attaching, and managing EBS Volumes (gp2).
* **Linux Administration:** File system formatting (`mkfs`), mounting, and fstab configuration.
* **Disaster Recovery:** Executing Snapshot strategies and restoring data volumes.
* **Data Integrity Verification:** Validating successful data recovery post-incident.
