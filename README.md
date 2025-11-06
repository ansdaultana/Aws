# Aws

# ☁️ What Is AWS & How Cloud Computing Works (IaaS, PaaS, SaaS)

## 💡 What Is Cloud Computing?
Cloud computing means **using the internet to access servers, storage, databases, and software** — instead of owning physical hardware.

In simple terms:
> You rent computing power, not buy it.

You only pay for what you use 💰 — like electricity or mobile data.


## 🧠 AWS Overview
**AWS (Amazon Web Services)** is Amazon’s **cloud platform** that provides:
- Computing power 💻 (EC2, Lambda)
- Storage 📦 (S3, EBS)
- Databases 🗄️ (RDS, DynamoDB)
- Networking 🌐 (VPC, Route 53)
- DevOps tools ⚙️ (CodePipeline, CloudFormation)

> AWS = A global data center network that lets you build and run anything in the cloud.

---

## ☁️ Cloud Computing Models

### 1️⃣ **IaaS — Infrastructure as a Service**
- You manage the **OS, runtime, and apps**, but AWS provides the infrastructure (servers, networking, storage etc).
- Gives you **most control** and flexibility.

🧩 **Examples:**
- EC2 (virtual machines)
- S3 (storage)
- EBS (block storage)
- VPC (networking)

🧠 **Think:** Renting a virtual machine and managing it yourself.

---

### 2️⃣ **PaaS — Platform as a Service**
- AWS manages the **infrastructure + runtime**.
- You only focus on **your code** and **data**.
- No need to handle servers or scaling manually.

🧩 **Examples:**
- AWS Elastic Beanstalk
- AWS Lambda (serverless)
- AWS RDS (managed database)

🧠 **Think:** You deploy your app — AWS runs it for you.

---

### 3️⃣ **SaaS — Software as a Service**
- You simply use the software — no setup or management.
- Everything (infrastructure, app, updates) is handled by the provider.

🧩 **Examples:**
- AWS WorkMail (email service)
- Amazon Chime (video meetings)
- Third-party SaaS like Gmail, Zoom, Salesforce

🧠 **Think:** Using ready-made software through your browser.

---

## 🧾 Comparison Table

| Layer | You Manage | Cloud Provider Manages | Example AWS Service |
|-------|-------------|------------------------|----------------------|
| **IaaS** | OS, App, Data | Servers, Networking | EC2, S3 |
| **PaaS** | App, Data | OS, Runtime, Infra | Elastic Beanstalk, RDS |
| **SaaS** | Nothing | Everything | WorkMail, Chime |



# 🌍 AWS Global Infrastructure

## 🏙️ 1. Region
- A **Region** is a group of AWS data centers in one geographical area.
- Each region is **independent** — data stays within that region.
- You choose a region when launching AWS services (like EC2, S3).
- Examples:
  - `us-east-1` → N. Virginia (default)
  - `ap-south-1` → Mumbai
  - `ap-southeast-1` → Singapore

🧠 **Tip:** Pick a region closest to your users for lower latency.

---

## 🏢 2. Availability Zones (AZs)
- Each region has **2 or more AZs** (separate data centers).
- AZs are connected but isolated — if one fails, others keep running.
- Example:

## 🛰️ 3. Edge Locations
- Smaller data centers that cache content closer to users.
- Used by **CloudFront (CDN)** for faster content delivery.
- Example: Users in Pakistan may access S3 files from the Singapore edge location.

# 🖥️ AWS Management Console Overview

## 💡 What Is It?
- The **AWS Management Console** is a **web-based dashboard** to access and manage all AWS services.
- You can launch, configure, and monitor resources like EC2, S3, IAM, and more — **visually** (no CLI needed).
- URL: [https://aws.amazon.com/console/](https://aws.amazon.com/console/)

---

## 🧭 Main Sections of the Console

### 🔍 1. Search Bar
- Quickly find any AWS service (e.g., “EC2”, “IAM”, “S3”).
- You can also search for documentation and settings.

### 🌍 2. Region Selector (Top-Right)
- Lets you choose which **Region** to manage resources in.
- Example: `US East (N. Virginia)` → `us-east-1`.
- ⚠️ Services and data are **region-specific**, so check this before creating anything.

### 👤 3. Account Menu
- Manage your AWS account, billing info, and security settings.
- Option to sign in as **Root user**, **IAM user**, or **federated identity**.

### ⚙️ 4. Services Menu
- Lists all AWS services grouped by category:
  - **Compute** → EC2, Lambda
  - **Storage** → S3, EBS
  - **Networking** → VPC, Route53
  - **Security** → IAM, KMS
  - **Monitoring** → CloudWatch

### 📊 5. Resource Dashboard / Home
- Shows shortcuts to your recently used services and regions.
- Displays resource counts and health status.

### �� 6. Billing & Cost Management
- View usage and cost reports.
- Set **billing alarms** and **budgets** to avoid overcharges.
- URL: [https://console.aws.amazon.com/billing](https://console.aws.amazon.com/billing)

---

## ⚙️ Access Levels

| Type | Description | Example |
|------|--------------|----------|
| **Root User** | Full access to account (use rarely) | Used for initial setup only |
| **IAM User** | Access controlled by policies | Everyday usage |
| **IAM Role** | Temporary permissions for services | EC2 accessing S3 |

---

## 🧩 Best Practices
- Always sign in as an **IAM User**, not the root account.
- Enable **MFA (Multi-Factor Authentication)** for security.
- Check the **Region** before creating resources.
- Set **budget alerts** for Free Tier usage.

---

## ✅ Summary
| Feature | Purpose |
|----------|----------|
| **Console** | Web UI for all AWS services |
| **Region Selector** | Choose where your resources are created |
| **Billing Dashboard** | Monitor and control AWS spending |
| **IAM Sign-in** | Secure way to log in with least privilege |

🧠 The Console is great for learning and visualization,  
but DevOps engineers later use **AWS CLI** and **Terraform** for automation.

# 🔐 AWS IAM — Users vs Roles vs Groups

## 💡 What Is IAM?
**IAM (Identity and Access Management)** is the AWS service used to securely manage **who can access what** in your AWS account.

It controls authentication (who you are) and authorization (what you can do).

---

## 👤 IAM User
- A **person or service account** that needs to log in to AWS.
- Each user has their **own username, password, and access keys**.
- Permissions are assigned using **policies** (JSON documents).

🧩 **Example:**
- `ans-dev` → Developer IAM user  
- Permissions: EC2, S3 (no Billing access)

🧠 **Use case:**  
You → create `ans-dev` user to access AWS CLI instead of using root.

---

## 👥 IAM Group
- A **collection of users** that share the same permissions.
- You attach policies to the **group**, and all members inherit them.
- Makes permission management easier.

🧩 **Example:**
- Group: `Developers`
- Policy: Access to EC2, S3
- Users: `ans-dev`, `ali-dev` → both get EC2 + S3 access automatically.

🧠 **Use case:**  
When you have multiple users with similar roles.

---

## 🎭 IAM Role
- A **temporary identity** with specific permissions.
- **No username or password.** Instead, AWS services or users **assume** a role to perform actions.
- Used by EC2 instances, Lambda, or external users for short-term access.

🧩 **Example:**
- Role: `EC2S3AccessRole`
- Policy: Allow EC2 instance to read/write S3 bucket.
- EC2 assumes the role → can access S3 without storing credentials.

🧠 **Use case:**  
Grant access to AWS services or external systems **securely** (no hard-coded keys).

---

## 🧾 Summary Table

| Type | Who Uses It | Access Method | Example Use Case |
|------|--------------|----------------|------------------|
| **User** | Human or app needing login | Username/Password or Access Keys | You logging in via CLI or Console |
| **Group** | Collection of users | Inherits attached policies | Team of developers with same access |
| **Role** | AWS service or external entity | Assumed temporarily | EC2 accessing S3 securely |

---

# 🧾 AWS IAM Policies (JSON Documents)

## 💡 What Is a Policy?
An **IAM Policy** is a **JSON document** that defines what actions are **allowed or denied** in AWS.

Policies control permissions for **Users**, **Groups**, or **Roles**.

---

## 🧠 Basic Idea
A policy answers three questions:
1. **Who** → (User / Role / Group)
2. **Can do what** → (Action)
3. **On which resource** → (Resource)

---

## 🧩 Example Policy
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::my-bucket"
    }
  ]
}
```

# 🔐 AWS IAM Best Practices


## ✅ Summary
| Practice | Why It Matters |
|-----------|----------------|
| Don’t use Root for daily work | Prevent full-account compromise |
| Create IAM Users | Traceable access per person |
| Use Groups | Easier permission management |
| Use Roles | Secure service-to-service access |
| Least Privilege | Reduces attack surface |
| Enable MFA | Prevents unauthorized logins |
| Monitor IAM | Detect and fix security risks |
| Billing Alerts | Avoid surprise costs |

# 💻 What Is EC2 (Elastic Compute Cloud)

## 💡 Definition
**Amazon EC2 (Elastic Compute Cloud)** is AWS’s service that provides **virtual servers (instances)** in the cloud.

Instead of buying physical computers, you **rent computing power** from AWS and pay only for what you use.

🧠 Think of EC2 as:
> “Your personal Linux or Windows server running inside Amazon’s data center.”

---

## ⚙️ Key EC2 Concepts

### 🧩 1️⃣ Instance
- An **EC2 instance** is your **virtual machine**.
- You choose its size (CPU, RAM, storage).
- Runs an operating system from an AMI (Amazon Machine Image).

🧠 Example:
`t2.micro` → 1 vCPU, 1 GB RAM (Free Tier eligible).

---

### 🧩 2️⃣ AMI (Amazon Machine Image)
- An **AMI** is a **template** used to create instances.
- It defines:
  - Operating System (Ubuntu, Amazon Linux, Windows)
  - Preinstalled software
  - Default configuration

🧠 Example:
You select “Ubuntu Server 22.04 LTS AMI” → AWS launches a server with Ubuntu preinstalled.

---

### 🧩 3️⃣ Key Pair
- EC2 uses **SSH key pairs** (not passwords) for secure access.
- When launching an instance:
  - You **download a `.pem` file** (your private key).
  - AWS keeps the public key.
- You use this `.pem` file to connect via SSH.

🧠 Example:
```bash
chmod 400 my-key.pem
ssh -i my-key.pem ubuntu@<ec2-public-ip>

```

# ☁️ AWS Storage Services

## 🧭 Overview
AWS provides multiple types of storage for different needs — from storing static files and backups to attaching persistent disks or sharing data across multiple servers.

| Service | Type | Used For | Think Of It Like |
|----------|------|-----------|------------------|
| **S3** | Object Storage | Files, backups, websites | A giant online USB drive |
| **EBS** | Block Storage | EC2 disks (OS or app data) | Your computer’s hard drive |
| **EFS** | File Storage | Shared storage for many EC2s | A shared office network drive |

---

## 🪣 1️⃣ Amazon S3 — Object Storage

### 💡 Concept
Amazon **S3 (Simple Storage Service)** is used to store and retrieve any amount of data — such as images, logs, or website files.  
It’s **object-based**, meaning you store files as *objects* inside *buckets* instead of as traditional files/folders.

---

### 🧩 Key Components
| Component | Description | Example |
|------------|--------------|----------|
| **Bucket** | Container for data (unique name per region) | `my-devops-bucket` |
| **Object** | The actual file or data | `index.html`, `photo.png` |
| **Key** | File path (unique identifier for object) | `images/logo.png` |
| **Region** | Buckets are created in a specific AWS region | `ap-south-1` |

---

### ⚙️ Features
- **Versioning:** Keeps multiple versions of files.  
- **Lifecycle Rules:** Automatically move or delete old data.  
- **Bucket Policies:** Control public or private access.  
- **Static Website Hosting:** Host websites directly from a bucket.  
- **Cross-Region Replication:** Replicate data to another region.  

---

### 🧠 CLI Example
```bash
# Create a new bucket
aws s3 mb s3://my-devops-bucket --region ap-south-1

# Upload a file
aws s3 cp index.html s3://my-devops-bucket/

# List bucket contents
aws s3 ls s3://my-devops-bucket
```

---

## 💾 **2️⃣ Amazon EBS — Block Storage**

# 💾 Amazon EBS — Block Storage

## 💡 Concept
**EBS (Elastic Block Store)** provides **block-level storage** for EC2 instances — like a virtual hard disk.  
Each EC2 uses an EBS volume to store its OS and application data.  
When stopped, data remains intact (persistent storage).

---

## 🧩 Key Components
| Component | Description | Example |
|------------|--------------|----------|
| **Volume** | Virtual hard disk attached to EC2 | `/dev/xvda` |
| **Snapshot** | Backup image of a volume (stored in S3) | `snap-0ab12345` |
| **Attachment** | Linking a volume to an EC2 instance | `i-0a12b34c5` |

---

## ⚙️ Features
- Persistent and replicated within the same AZ  
- Snapshots for backup & recovery  
- Supports encryption and resizing  
- Detach and reattach between EC2s  

---

## 🧠 CLI Example
```bash
# Create a volume
aws ec2 create-volume --size 8 --availability-zone us-east-1a

# Attach it to an EC2 instance
aws ec2 attach-volume --volume-id vol-123456 --instance-id i-123456 --device /dev/xvdf

# Create a snapshot
aws ec2 create-snapshot --volume-id vol-123456 --description "Daily Backup"
```

---

## 🗂️ **3️⃣ Amazon EFS — File Storage**

# 🗂️ Amazon EFS — File Storage

## 💡 Concept
**EFS (Elastic File System)** is a **shared file storage system** that multiple EC2 instances can access at once.  
It’s like a shared network drive for your servers — ideal for web apps, logs, and container workloads.

---

## 🧩 Key Components
| Component | Description | Example |
|------------|--------------|----------|
| **File System** | The main EFS storage resource | `fs-12345abcd` |
| **Mount Target** | Network endpoint in each AZ | `fs-12345.efs.ap-south-1.amazonaws.com` |
| **Access Point** | Defines access permissions and paths | `ap-0a1b2c3d` |

---

## ⚙️ Features
- Shared across multiple EC2 instances  
- Automatically scales with data size  
- Highly available across multiple AZs  
- Uses **NFS (Network File System)** protocol  

---

## 🧠 Mount Example
```bash
# Install NFS utilities
sudo apt update -y
sudo apt install nfs-common -y

# Create mount directory
sudo mkdir /mnt/efs

# Mount EFS
sudo mount -t nfs4 fs-12345.efs.ap-south-1.amazonaws.com:/ /mnt/efs
```

# ⚖️ Key Differences Between S3, EBS, and EFS

## 🧩 1️⃣ Storage Type & Access Method
| Service | Storage Type | Access Method |
|----------|---------------|---------------|
| **S3** | Object Storage | Accessed via API or HTTPS (upload/download files) |
| **EBS** | Block Storage | Attached to a single EC2 instance as a disk |
| **EFS** | File Storage | Mounted as a shared file system by multiple EC2s |

---

## 🧩 2️⃣ Use Case & Scalability
| Service | Primary Use Case | Scalability |
|----------|------------------|--------------|
| **S3** | Store backups, media, logs, static websites | Automatically scales to unlimited size |
| **EBS** | EC2 OS or database storage | Manual resizing; tied to one AZ |
| **EFS** | Shared storage for multiple EC2s | Automatically scales with file growth |

---

✅ **In short:**  
- **S3** → Best for files and backups.  
- **EBS** → Best for one EC2’s disk or database storage.  
- **EFS** → Best for shared data between multiple EC2 instances.
