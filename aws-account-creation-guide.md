# **AWS Account Creation Guide**  
*A step-by-step walkthrough for setting up your first AWS account*

![AWS Logo](https://d1.awsstatic.com/logos/aws-logo-lockups/poweredbyaws/PB_AWS_logo_RGB_stacked_REV_SQ.91cd4af40773cbfbd15577a3c2b8a346fe3e8fa2.png)

## **Table of Contents**
1. [Cloud Computing Overview](#-cloud-computing-overview)
2. [AWS Account Setup](#-aws-account-setup)
   - Email Verification
   - Payment Method
   - Identity Confirmation
3. [First Login](#-first-login)
4. [Security Best Practices](#-security-best-practices)
5. [Project Reflection](#-project-reflection)

---

## **☁️ Cloud Computing Overview**

### **What is Cloud Computing?**
- **Digital storage space** accessible via internet
- **Pay-as-you-go model**: Only pay for resources used
- **Scalable**: Easily adjust resources based on demand

### **Why AWS?**
- **Market leader** with 200+ services
- **Free Tier**: 12 months free for new accounts
- **Global infrastructure**: 31 geographic regions

---

## **🛠️ AWS Account Setup**

### **1. Initial Registration**
1. Go to [AWS Signup Page](https://portal.aws.amazon.com/billing/signup)
2. Enter:
   - Email address
   - AWS account name (e.g., "my-first-aws-account")
   - Password

![Signup Form](https://d1.awsstatic.com/account-creation/sign-up-page.8a4b0a9d5a3a5f8e8b5d9c7b3a2f1e8d4c3b2a1.png)

### **2. Email Verification**
1. Check inbox for verification code
2. Enter code on AWS verification page

### **3. Payment Method**
- Credit/debit card required (may see $1 temporary hold)
- No charges unless exceeding Free Tier limits

### **4. Identity Confirmation**
1. Enter personal information (phone/address)
2. Choose verification method:
   - **Text message (SMS)**
   - **Voice call**

### **5. Support Plan Selection**
- **Basic (Free)**: Recommended for beginners
- Developer/Business: Paid options with enhanced support

---

## **🔑 First Login**

### **Accessing AWS Console**
1. Go to [AWS Management Console](https://console.aws.amazon.com/)
2. Select **"Root user"**  
3. Enter:
   - Registered email
   - Password
   - CAPTCHA if prompted

![Login Screen](https://d1.awsstatic.com/console/login-console.8a4b0a9d5a3a5f8e8b5d9c7b3a2f1e8d4c3b2a1.png)

---

## **🔒 Security Best Practices**

### **Immediate Actions After Setup**
1. **Enable MFA** (Multi-Factor Authentication)
   ```bash
   IAM → Users → Security Credentials → Assign MFA device
   ```
2. **Create IAM Users** (Avoid using root account daily)
3. **Set Billing Alerts**
   ```bash
   Billing → Preferences → Receive Billing Alerts
   ```

### **Free Tier Monitoring**
- Track usage at: [AWS Free Tier Dashboard](https://console.aws.amazon.com/billing/home#/freetier)

---

## **📝 Project Reflection**

### **Key Learnings**
1. **AWS Democratizes Technology**: Small businesses can access enterprise-grade infrastructure
2. **Flexible Pricing**: Pay only for what you use
3. **Global Reach**: Deploy resources worldwide in minutes

### **Next Steps**
1. Explore **EC2** (Virtual Servers)
2. Try **S3** (File Storage)
3. Set up **CloudWatch** for monitoring

---

## **🚀 Getting Started with AWS Services**
```bash
# First CLI command (install AWS CLI first)
aws ec2 describe-instances

# Launch your first EC2 instance
aws ec2 run-instances --image-id ami-0abcdef1234567890 --instance-type t2.micro
```

[![AWS Free Tier](https://img.shields.io/badge/AWS-Free_Tier-orange)](https://aws.amazon.com/free/)  
[![Documentation](https://img.shields.io/badge/AWS-Documentation-blue)](https://docs.aws.amazon.com/)

---

## Screehshots

<img width="881" alt="Snipaste_2025-07-07_10-43-53" src="https://github.com/user-attachments/assets/51853103-b43c-4308-b569-31f9c11fdb2f" />


<img width="746" alt="Snipaste_2025-07-07_10-42-39" src="https://github.com/user-attachments/assets/b0ab5802-5506-4a5e-9322-6361c7bb22f0" />


<img width="1085" alt="Snipaste_2025-07-07_10-40-21" src="https://github.com/user-attachments/assets/4b0ec82e-1333-4033-ae0b-9bd104d18554" />


<img width="1384" alt="Snipaste_2025-07-07_10-39-20" src="https://github.com/user-attachments/assets/6122ebfc-db6e-4b1e-99a7-e58876057bf1" />



**Pro Tip**: Always log out from the AWS Console after use, especially on shared computers!  

```bash
# Cleanup reminder
echo "Remember to stop unused resources to avoid charges!" >> aws_tips.txt
``` 

This README provides a permanent reference for AWS beginners while maintaining all key visual elements for GitHub rendering.
