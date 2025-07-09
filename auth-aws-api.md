
```markdown
# **🔐 Secure AWS API Authentication Setup**  
*Automating AWS resource management with IAM & CLI security best practices*

---

## **📌 Project Purpose**  
Establish secure programmatic access to AWS APIs for:  
✅ EC2/S3 automation scripts  
✅ AWS CLI operations  
✅ Infrastructure-as-Code workflows  

---

## **🛠️ Core Components**  
| Component | Purpose | AWS Service |  
|-----------|---------|-------------|  
| **IAM User** | Least-privilege access identity | IAM |  
| **IAM Policy** | EC2/S3 permissions boundary | IAM |  
| **Programmatic Keys** | CLI/API authentication credentials | IAM |  
| **AWS CLI** | Terminal-based AWS control plane | CLI |  

---

## **🔒 Step-by-Step Implementation**  

### **1. IAM Setup (Console)**  
```bash
# Minimal EC2+S3 Policy (JSON)
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["ec2:*", "s3:*"],
      "Resource": "*"
    }
  ]
}
```
**Security Best Practices:**  
- Create dedicated `automation_user`  
- Attach policy to **IAM Role** (not directly to user)  
- Enable **MFA** for console access  

---

### **2. AWS CLI Installation**  
**Linux/macOS:**  
```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
aws --version  # Verify
```

**Windows:**  
```powershell
msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi
aws --version
```

---

### **3. CLI Configuration**  
```bash
aws configure
```
**Prompt Values:**  
```
AWS Access Key ID: AKIAXXXXXXXXXXXXXXXX
AWS Secret Access Key: ****************************************
Default region name: us-east-1
Default output format: json
```

**Test Authentication:**  
```bash
aws sts get-caller-identity  # Verify credentials
aws ec2 describe-regions --output table  # Test API access
```

---

## **🌐 API Fundamentals**  
| Concept | Relevance |  
|---------|-----------|  
| **REST API** | HTTP-based AWS service interactions |  
| **Access Key** | Equivalent to username+password |  
| **Secret Key** | Must never be exposed/shared |  
| **Region** | Geographic API endpoint target |  

---

## **⚠️ Security Considerations**  
- **Rotate keys** every 90 days (IAM → Security Credentials)  
- **Never commit keys** to version control  
- Use **named profiles** for multiple accounts:  
  ```bash
  aws configure --profile prod
  ```

---

## **🔧 Troubleshooting**  
| Error | Solution |  
|-------|----------|  
| `InvalidClientTokenId` | Verify key correctness + region match |  
| `UnauthorizedOperation` | Check IAM policy attachments |  
| `NoRegionError` | Set default region or use `--region` flag |  

---

## **📚 Learning Outcomes**  
✔ Principle of **Least Privilege** in IAM  
✔ Programmatic vs Console access differences  
✔ AWS CLI as an **API client**  
✔ Secure credential management patterns  

---

## Screenshots

<img width="567" alt="Snipaste_2025-07-09_07-59-51" src="https://github.com/user-attachments/assets/d293525b-7089-476a-8d53-303a94343c43" />


<img width="667" alt="Snipaste_2025-07-09_08-00-14" src="https://github.com/user-attachments/assets/40c3ac42-59b6-4b61-be07-380861120720" />


<img width="683" alt="Snipaste_2025-07-09_08-01-31" src="https://github.com/user-attachments/assets/aa542e09-9f6d-4e88-8bda-52ba01254e83" />


## **🚀 Next Steps**  
- [ ] Implement **AWS CLI named profiles**  
- [ ] Explore **AWS SDKs** (Python/Bash)  
- [ ] Set up **CloudTrail** for API auditing  

[![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?logo=amazon-aws)](https://aws.amazon.com) 
[![IAM](https://img.shields.io/badge/IAM-Security-blue)](https://docs.aws.amazon.com/IAM/)
```

### **Key Features**:
1. **Visual Security Alerts** – Highlights credential protection needs
2. **Multi-OS Installation** – Covers Linux/macOS/Windows
3. **API Concept Mapping** – Relates abstract concepts to AWS usage
4. **Ready-to-Run Code** – Copy-paste friendly commands
5. **Badge Integration** – Professional repository branding

### **How to Customize**:
1. Add your actual IAM policy if more restrictive than example
2. Include screenshots of:
   - IAM user creation
   - CLI successful auth test
3. Link to your specific project's next steps

Would you like me to add a **"Common Use Cases"** section showing how this authentication enables specific automation scripts?
