# AWS Infrastructure Setup using Terraform

## Overview  
This project provisions a **scalable and highly available** web infrastructure on AWS using Terraform. It includes:  
✅ VPC  
✅ Public Subnets  
✅ Internet Gateway  
✅ Security Group  
✅ Application Load Balancer (ALB)  
✅ EC2 Instances  
✅ S3 Bucket  

## Architecture Components  

### 1️⃣ Virtual Private Cloud (VPC)  
- Creates a VPC with a **CIDR block** specified via variables.  

### 2️⃣ Public Subnets  
- Two public subnets in **us-east-1a** and **us-east-1b**.  
- Enables **public IP mapping** for instances.  

### 3️⃣ Internet Gateway & Route Table  
- Attaches an **Internet Gateway** to the VPC.  
- Routes all outbound traffic (`0.0.0.0/0`).  

### 4️⃣ Security Group  
✅ **Inbound Rules:**  
   - Allow HTTP (`80`) from anywhere 🌍  
   - Allow SSH (`22`) from anywhere (optional)  

✅ **Outbound Rules:**  
   - All traffic allowed  

### 5️⃣ S3 Bucket  
- Creates an S3 bucket for potential data storage.  

### 6️⃣ EC2 Instances  
- Deploys **two EC2 instances** (`t2.micro`).  
- Uses **User Data Scripts** (`userdata.sh`, `userdata1.sh`).  
- Associated **Security Group** ensures access control.  

### 7️⃣ Application Load Balancer (ALB)  
- Configured across **both subnets** for high availability.  
- Listens on **port 80** for incoming traffic.  

### 8️⃣ Target Group & Attachments  
- Creates an **ALB Target Group** with health checks (`/`).  
- Registers **EC2 instances** as targets.  

### 9️⃣ ALB Listener  
- Listens on **port 80** and forwards traffic to the Target Group.  

### 🔥 Deployment Instructions  

#### Prerequisites  
✔️ **AWS CLI** configured  
✔️ **Terraform** installed  

#### Steps to Deploy  

```sh
# Clone the repo
git clone <repo-url>
cd <repo-name>

# Initialize Terraform
terraform init

# Validate configuration
terraform validate

# Deploy infrastructure
terraform apply -auto-approve

# Get Load Balancer DNS
terraform output loadbalancerdns
















































