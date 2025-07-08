
```markdown
# **AWS Auto Scaling with ALB using Launch Template**  

## **🚀 Project Overview**  
Automates EC2 instance scaling using **Launch Templates + Application Load Balancer (ALB)**. Demonstrates:  
- **Dynamic resource allocation** based on demand  
- **High availability** through ALB integration  
- **Infrastructure-as-Code** principles via AWS Console  

---

## **🛠️ Core Components**  
| Component | Purpose | AWS Service |  
|-----------|---------|-------------|  
| **Launch Template** | Blueprint for EC2 instances | EC2 |  
| **Auto Scaling Group** | Manages instance fleet size | Auto Scaling |  
| **Scaling Policies** | Rules for scaling in/out | CloudWatch Alarms |  
| **Application Load Balancer** | Distributes traffic | ELB |  

---

## **📜 Step-by-Step Implementation**  

### **1. Create Launch Template**  
```bash
# Sample User Data for Auto Scaling Instances (Optional)
#!/bin/bash
sudo amazon-linux-extras install epel -y
sudo yum install stress -y
```
**Key Settings:**  
- AMI (e.g., Amazon Linux 2)  
- Instance type (`t2.micro`)  
- Security groups (allow HTTP/HTTPS)  
- IAM role (if needed)  

---

### **2. Configure Auto Scaling Group**  
**Critical Parameters:**  
| Parameter | Example Value |  
|-----------|---------------|  
| Desired Capacity | 2 |  
| Minimum Size | 1 |  
| Maximum Size | 4 |  
| Subnets | Multi-AZ selection |  

---

### **3. Set Up Scaling Policies**  
**Example CPU-Based Policy:**  
- **Scale-out**: Add 1 instance when CPU > 70% for 3 mins  
- **Scale-in**: Remove 1 instance when CPU < 30% for 5 mins  

![Scaling Policy Diagram](https://i.imgur.com/JZw9FEN.png) *(Replace with your screenshot)*  

---

### **4. Attach ALB**  
```bash
# ALB Health Check Configuration
Health Check Path: /index.html
Interval: 30 seconds
Timeout: 5 seconds
```
**Best Practices:**  
- Enable **cross-zone load balancing**  
- Configure **stickiness** if needed  

---

### **5. Test Auto Scaling**  
**Simulate Load:**  
```bash
stress -c 4  # Triggers CPU scaling
```
**Monitoring Tools:**  
- AWS Console → Auto Scaling → **Activity History**  
- CloudWatch → **CPU Utilization Metrics**  

---

## **🔧 Troubleshooting**  
| Issue | Solution |  
|-------|----------|  
| Instances not launching | Check IAM permissions & subnet routes |  
| ALB 503 errors | Verify security groups allow HTTP/HTTPS |  
| Scaling delays | Adjust CloudWatch alarm durations |  

---

## **📚 Learning Outcomes**  
✔ **Launch Templates** vs Launch Configurations  
✔ **Target Tracking** vs Step Scaling policies  
✔ **ALB integration** for zero-downtime deployments  
✔ **CloudWatch metrics** for scaling triggers  

---

## Screenshots

<img width="1388" alt="Snipaste_2025-07-08_23-32-08" src="https://github.com/user-attachments/assets/595cb101-4306-40ad-94d6-2c36e012ca82" />


<img width="1379" alt="Snipaste_2025-07-08_23-31-42" src="https://github.com/user-attachments/assets/3bb34b9d-e6a5-495f-afe6-f8d380d37f33" />


<img width="1383" alt="Snipaste_2025-07-08_23-31-10" src="https://github.com/user-attachments/assets/c8ed6982-f95f-411f-bfcc-9a6a1eeb5c36" />


<img width="1119" alt="Snipaste_2025-07-08_23-30-47" src="https://github.com/user-attachments/assets/04827a2c-7b2b-4e6a-9c15-4abcf4bb2464" />


## **📈 Next Steps**  
- [ ] Terraform/CDK automation  
- [ ] Custom metrics scaling (e.g., request queue depth)  
- [ ] Blue/green deployment testing  

[![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?logo=amazon-aws)](https://aws.amazon.com) 
[![Auto Scaling](https://img.shields.io/badge/Auto_Scaling-EC2-orange)](https://docs.aws.amazon.com/autoscaling/)
```

### **Key Features of This Template**:
1. **Visual Hierarchy** – Clear sections with icons/headers
2. **Tables for Technical Details** – Easy parameter reference
3. **Code Snippets** – Ready-to-use commands
4. **Troubleshooting Guide** – Quick debug reference
5. **Badges** – For repository aesthetics

### **How to Customize**:
1. Replace placeholder image URL with your actual architecture diagram
2. Add specific AMI IDs/instance types used
3. Include your ALB DNS name in examples
4. Add **"How to Contribute"** section if open-source
