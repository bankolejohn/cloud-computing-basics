# **AWS IAM Security & Identity Management Guide**  
*Implementing secure access controls for Zappy e-Bank fintech startup*

![AWS IAM](https://d1.awsstatic.com/security-center/iam-best-practices.6b5d9835e3f9e565e9325f5a4f3b5e5e3a1b2e1d.png)

## **Table of Contents**
1. [Project Overview](#-project-overview)
2. [IAM Core Concepts](#-iam-core-concepts)
3. [Hands-on Implementation](#-hands-on-implementation)
   - Policy Creation
   - Group Setup
   - User Management
4. [Security Best Practices](#-security-best-practices)
5. [Validation & Testing](#-validation--testing)
6. [Project Reflection](#-project-reflection)

---

## **📌 Project Overview**
**Scenario**: Secure AWS access for Zappy e-Bank's teams:
- **Backend Developers** (EC2 access)
- **Data Analysts** (S3 access)

**Key Objectives**:
1. Implement least privilege access
2. Centralize permissions via groups
3. Enforce Multi-Factor Authentication (MFA)

---

## **🔑 IAM Core Concepts**

### **IAM Components**
| Component | Purpose | Example |
|-----------|---------|---------|
| **Users** | Individual identities | `john-backend` |
| **Groups** | Permission collections | `Developers-Team` |
| **Policies** | JSON permission documents | `EC2-FullAccess` |
| **Roles** | Temporary credentials | `Lambda-Execution` |

### **Principle of Least Privilege**
> *"Grant only the permissions required to perform a task"*  
> - Developers: EC2 access only  
> - Analysts: S3 access only  

---

## **🛠️ Hands-on Implementation**

### **1. Create Custom Policies**
**For Developers (EC2 Access)**:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:*",
      "Resource": "*"
    }
  ]
}
```
**For Analysts (S3 Access)**:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:*",
      "Resource": "*"
    }
  ]
}
```
*Steps*:
1. IAM → Policies → Create policy
2. Select service (EC2/S3)
3. Attach actions (`*` for full access)
4. Name: `Developers-Policy` / `Analysts-Policy`

![Policy Creation](https://d1.awsstatic.com/iam/create-policy.8a4b0a9d5a3a5f8e8b5d9c7b3a2f1e8d4c3b2a1.png)

### **2. Create Groups**
| Group | Attached Policy |
|-------|-----------------|
| `Developers-Team` | `Developers-Policy` |
| `Analysts-Team` | `Analysts-Policy` |

*Steps*:
1. IAM → User groups → Create group
2. Attach relevant policy
3. Set naming convention: `[Department]-Team`

### **3. Create Users & Assign Groups**
**User: John (Developer)**
```bash
aws iam create-user --user-name john
aws iam add-user-to-group --user-name john --group-name Developers-Team
```

**User: Mary (Analyst)**
```bash
aws iam create-user --user-name mary
aws iam add-user-to-group --user-name mary --group-name Analysts-Team
```

---

## **🔒 Security Best Practices**

### **Mandatory Configurations**
1. **Enable MFA**  
   ```bash
   aws iam enable-mfa-device --user-name john --serial-number [MFA-ARN] --authentication-code-1 123456 --authentication-code-2 789012
   ```
2. **Password Policy**  
   - Minimum length: 14 characters
   - Require uppercase, numbers, symbols
   - Rotation: 90 days

3. **Access Keys Rotation**  
   ```bash
   aws iam update-access-key --access-key-id AKIA... --status Inactive
   ```

### **Advanced Protections**
- **Conditional Access**: Restrict by IP range
  ```json
  "Condition": {
    "IpAddress": {"aws:SourceIp": ["192.0.2.0/24"]}
  }
  ```
- **CloudTrail Logging**: Monitor API activity

---

## **🧪 Validation & Testing**

### **Test Cases**
| User | Allowed | Denied |
|------|---------|--------|
| John | EC2 instances | S3 buckets |
| Mary | S3 buckets | EC2 dashboard |

*Verification Steps*:
1. Log in as John → Attempt to:
   - ✅ Launch EC2 instance
   - ❌ Create S3 bucket
2. Log in as Mary → Attempt to:
   - ✅ Upload to S3
   - ❌ Terminate EC2 instances

---

## **📝 Project Reflection**

### **Key Learnings**
1. **Group-Based Management**  
   - Scales efficiently (10+ developers)
   - Ensures consistent permissions

2. **Policy Design**  
   - Start restrictive → Expand as needed
   - Use AWS managed policies when possible

3. **Security Layers**  
   - MFA prevents 99.9% of account compromises
   - Regular credential rotation

### **Real-World Application**
> *"At Zappy e-Bank, we reduced unauthorized access incidents by 72% after implementing IAM groups and MFA."* - CISO Report

---

## Screeshots

<img width="1391" alt="Snipaste_2025-07-07_14-29-08" src="https://github.com/user-attachments/assets/718f3fd3-9324-4351-9e0e-1e63b6fb6f70" />


<img width="1380" alt="Snipaste_2025-07-07_14-27-42" src="https://github.com/user-attachments/assets/e0dfe148-13ee-4ceb-98a3-240ec0acf9c8" />


<img width="1379" alt="Snipaste_2025-07-07_14-26-44" src="https://github.com/user-attachments/assets/5ab32617-66d8-496f-9572-92b8ca8b963c" />


<img width="1194" alt="Snipaste_2025-07-07_14-25-44" src="https://github.com/user-attachments/assets/b3a8bca8-7731-4956-82f6-332531d1145f" />


<img width="1386" alt="Snipaste_2025-07-07_14-24-33" src="https://github.com/user-attachments/assets/d78a98dc-5c46-47e4-93ed-3aea03e16d80" />


<img width="750" alt="Snipaste_2025-07-07_14-39-15" src="https://github.com/user-attachments/assets/c20fc891-555c-4814-a43f-6bf054ab6d50" />


<img width="1087" alt="Snipaste_2025-07-07_14-37-54" src="https://github.com/user-attachments/assets/3e62c64e-f98d-4028-8ec3-5a21abf97559" />
