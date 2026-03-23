# High-Availability Self-Healing Architecture 

## 📌 Objective
To design a fault-tolerant, highly available web architecture that automatically scales and recovers from instance failures without human intervention, ensuring 99.9% uptime.

## ⚙️ Technology Stack
* **Compute:** AWS EC2, Auto Scaling Groups (ASG), Launch Templates
* **Networking:** Application Load Balancer (ALB), Virtual Private Cloud (VPC), Security Groups
* **Automation:** Bash Scripting (User Data), IMDSv2

## 🏗️ Architecture & Implementation
1. **Launch Template Configuration:** Created a secure EC2 Launch Template using Amazon Linux 2023. Automated the provisioning of Nginx web servers using a custom Bash script via User Data. 
2. **Secure Metadata Retrieval:** Implemented IMDSv2 in the initialization script to securely fetch and display the specific Instance ID on the web page to verify traffic routing.
3. **Traffic Distribution:** Deployed an Internet-facing Application Load Balancer (ALB) across three Availability Zones (us-east-1a, 1b, 1c) to ensure high availability.
4. **Auto Scaling & Self-Healing:** Configured an Auto Scaling Group (Desired: 2, Min: 1, Max: 3) linked to the ALB. 

## 📸 Proof of Concept

### 1. Automated Nginx Provisioning via User Data (IMDSv2)
<img width="833" height="575" alt="1 1" src="https://github.com/user-attachments/assets/957fe0a2-d95b-4339-a56c-66f252e68a88" />


### 2. Application Load Balancer Successfully Routing Traffic
<img width="1920" height="1033" alt="1 2 1" src="https://github.com/user-attachments/assets/5ba00356-e899-4d19-8e5f-4a9802a3e42f" />
<img width="1918" height="1036" alt="1 2 2" src="https://github.com/user-attachments/assets/a3369bce-31fb-45bb-9d5f-3a6daf790c94" />


### 3. Self-Healing Verification (Simulated Instance Failure)
*I manually terminated a healthy EC2 instance to simulate a crash. As shown in the Activity History below, the Auto Scaling Group detected the failure and automatically spun up a replacement instance within 120 seconds to maintain the desired capacity.*
<img width="1575" height="800" alt="1 3 1" src="https://github.com/user-attachments/assets/beb4029f-37f7-437a-9f1c-05eb84c1687c" />
