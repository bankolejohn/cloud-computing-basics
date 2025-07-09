
---

# 🚀 Capstone Project: WordPress Site on AWS (DigitalBoost)

A DevOps project to deploy a **scalable**, **secure**, and **high-availability** WordPress site on AWS for a digital marketing agency, **DigitalBoost**. This project leverages core AWS services like EC2, RDS, VPC, EFS, Auto Scaling, and ALB.

---

## 📚 Table of Contents

1. [📌 Project Overview](#-project-overview)
2. [🧰 Prerequisites](#-prerequisites)
3. [📐 Architecture Diagram](#-architecture-diagram)
4. [🧩 Components & Setup Guide](#-components--setup-guide)

   * [1️⃣ VPC Setup](#1️⃣-vpc-setup)
   * [2️⃣ Public & Private Subnets + NAT Gateway](#2️⃣-public--private-subnets--nat-gateway)
   * [3️⃣ RDS MySQL Setup](#3️⃣-rds-mysql-setup)
   * [4️⃣ EFS Setup](#4️⃣-efs-setup)
   * [5️⃣ Application Load Balancer](#5️⃣-application-load-balancer)
   * [6️⃣ Auto Scaling Group](#6️⃣-auto-scaling-group)
5. [🔐 Security Measures](#-security-measures)
6. [📸 Demonstration Checklist](#-demonstration-checklist)
7. [📁 Repository Structure](#-repository-structure)
8. [🧪 Testing & Validation](#-testing--validation)
9. [📦 Optional Enhancements](#-optional-enhancements)
10. [🤝 Contributors](#-contributors)
11. [📜 License](#-license)

---

## 📌 Project Overview

This project aims to:

* Deploy a **WordPress** website on AWS
* Ensure **high availability**, **auto-scaling**, and **shared storage**
* Implement a **secure** and **cost-effective** infrastructure
* Use Infrastructure as Code (optional)

---

## 🧰 Prerequisites

* AWS CLI configured with appropriate IAM credentials
* Core understanding of:

  * VPCs & Subnets
  * EC2 instances
  * RDS & EFS
  * Load Balancers & Auto Scaling
* Key Pair for SSH
* Completion of 3MTT Core 2 Projects

---

## 📐 Architecture Diagram

*(Insert your detailed architecture diagram image here)*

The architecture includes:

* Isolated VPC
* Public/Private Subnets across 2 AZs
* NAT Gateway for private subnet internet access
* RDS MySQL DB in private subnet
* EC2 WordPress in private subnet
* ALB in public subnet
* Auto Scaling + CloudWatch

---

## 🧩 Components & Setup Guide

---

### 1️⃣ VPC Setup

**Objective:** Isolate network resources in a custom VPC.

**Steps:**

* VPC CIDR: `10.0.0.0/16`
* 2 Public Subnets: `10.0.1.0/24`, `10.0.2.0/24`
* 2 Private Subnets: `10.0.3.0/24`, `10.0.4.0/24`
* Attach Internet Gateway & NAT Gateway

**Commands:**

```bash
aws ec2 create-vpc --cidr-block 10.0.0.0/16
aws ec2 create-internet-gateway
aws ec2 create-subnet --vpc-id <vpc-id> --cidr-block 10.0.1.0/24
```

---

### 2️⃣ Public & Private Subnets + NAT Gateway

**Objective:** Split resources between public and private access layers.

**Steps:**

* Attach ALB & Bastion Host to public subnets
* Attach EC2 & RDS to private subnets
* Create Elastic IP & NAT Gateway in public subnet
* Update route tables for NAT access from private subnet

---

### 3️⃣ RDS MySQL Setup

**Objective:** Deploy a reliable MySQL database backend for WordPress.

**Steps:**

* Launch Amazon RDS with MySQL
* Configure Multi-AZ deployment (recommended)
* Enable automatic backups and encryption
* Open port 3306 to EC2 security group

**Configuration:**

* DB Instance Class: `db.t3.micro`
* Engine: `MySQL 8.x`
* Public Access: No
* Storage: GP2 or GP3

---

### 4️⃣ EFS Setup

**Objective:** Allow multiple EC2 instances to access shared WordPress files.

**Steps:**

* Create EFS file system
* Create mount targets in each AZ
* Mount EFS at `/var/www/html` on EC2

**Commands:**

```bash
sudo yum install -y amazon-efs-utils
sudo mkdir -p /var/www/html
sudo mount -t efs fs-xxxx:/ /var/www/html
```

---

### 5️⃣ Application Load Balancer

**Objective:** Distribute HTTP/S traffic to healthy EC2 instances.

**Steps:**

* Create ALB in public subnets
* Configure HTTPS Listener using ACM certificate
* Target Group: EC2s in private subnets
* Health Check Path: `/`

---

### 6️⃣ Auto Scaling Group

**Objective:** Dynamically adjust EC2 count based on traffic.

**Steps:**

* Create Launch Template (AMI with WordPress + EFS mount)
* Set Min/Max/Desired instance count
* Scaling Policy: CPU > 70% = scale out, CPU < 30% = scale in
* Attach ASG to target group

---

## 🔐 Security Measures

| Layer | Security Configuration                                |
| ----- | ----------------------------------------------------- |
| VPC   | Subnet segmentation, no public DB access              |
| ALB   | HTTPS with SSL (ACM)                                  |
| EC2   | Security Group allows HTTP/HTTPS only from ALB        |
| RDS   | Access only from EC2 SG, encryption enabled           |
| SSH   | Access only through Bastion Host in public subnet     |
| IAM   | Instance roles for S3, EFS access (no hardcoded keys) |

---

## 📸 Demonstration Checklist

✅ WordPress page loads via Load Balancer
✅ RDS database connection is successful
✅ Uploading media reflects across instances (EFS)
✅ Auto Scaling launches more EC2s under load
✅ SSH access only through Bastion

---

## 📁 Repository Structure

```
wordpress-aws-capstone/
├── scripts/
│   ├── vpc.sh
│   ├── rds.sh
│   ├── efs.sh
│   ├── ec2-wordpress.sh
│   ├── alb-autoscaling.sh
├── assets/
│   └── architecture-diagram.png
├── load-testing/
│   └── locustfile.py
├── terraform/ (optional)
│   └── main.tf
└── README.md
```

---

## 🧪 Testing & Validation

* Use Apache Benchmark:

  ```bash
  ab -n 1000 -c 100 http://<alb-dns>/
  ```
* Use Locust for concurrent user testing
* Confirm logs in CloudWatch
* Validate instance count increases under load

---

## 📦 Optional Enhancements

* [ ] Infrastructure as Code with **Terraform**
* [ ] CI/CD for WordPress deployments
* [ ] Route 53 + custom domain
* [ ] S3 offload for static content
* [ ] Use AWS WAF to protect ALB

---

## Screenshots

<img width="1388" alt="Snipaste_2025-07-08_23-32-08" src="https://github.com/user-attachments/assets/ad339fa4-9201-4fb5-91e5-95388f369a8a" />


<img width="1379" alt="Snipaste_2025-07-08_23-31-42" src="https://github.com/user-attachments/assets/4f8a3de8-1a1c-401a-81d8-01672f92788b" />


<img width="1383" alt="Snipaste_2025-07-08_23-31-10" src="https://github.com/user-attachments/assets/f617b12b-fb71-4930-bf82-af63900365a3" />


<img width="1119" alt="Snipaste_2025-07-08_23-30-47" src="https://github.com/user-attachments/assets/57df4658-13c0-42a9-afe2-039abb9eda1e" />


<img width="1393" alt="Snipaste_2025-07-08_22-44-18" src="https://github.com/user-attachments/assets/9a55d4bb-3cee-4be5-8108-dc892873825b" />

## 🤝 Contributors

* **DigitalBoost DevOps Intern Team**
* **AWS Solutions Architect (You)**

---

## 📜 License

This project is licensed under the MIT License.

---

Would you like this exported as a downloadable `.md` file or a `.docx` for submission? I can also generate a GitHub Pages site if needed.
