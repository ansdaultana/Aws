# Aws

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