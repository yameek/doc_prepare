[← Back to Index](./README.md)

# 2. Cloud-Native Services

Pick one major provider (AWS, GCP, Azure) and know it deep. The concepts transfer.

## Junior -> Mid: The Basics
**Goal:** Can deploy a standard web app with a database.

### 1. Compute
- **Concept:** Where code runs.
- **Key Skills:**
    - **EC2 (VMs):** Launching an instance, SSH-ing in.
    - **Lambda (Serverless):** Running functions without managing servers.

### 2. Storage & DB
- **Concept:** Where data lives.
- **Key Skills:**
    - **S3 (Object Storage):** Storing files, static websites.
    - **RDS (Relational DB):** Managed Postgres/MySQL.
    - **EBS (Block Storage):** The hard drive attached to your VM.

### 3. Networking
- **Concept:** Connecting the pieces.
- **Key Skills:**
    - **VPC:** Your private network in the cloud.
    - **Security Groups:** Firewalls (allow port 80 from anywhere, port 22 from my IP).
    - **Load Balancers (ELB):** Distributing traffic across multiple servers.

---

## Mid -> Senior: Architecture & Resilience
**Goal:** Designs highly available, fault-tolerant systems.

### 1. Advanced Networking
- **Concept:** Routing and isolation.
- **Key Knowledge:**
    - **Subnets:** Public vs Private subnets (NAT Gateways).
    - **Route 53:** Managed DNS and health checks.
    - **CDN (CloudFront):** Caching content at the edge.

### 2. IAM (Identity & Access Management)
- **Concept:** Who can do what.
- **Key Knowledge:**
    - **Roles vs Users:** Why services should use Roles, not Access Keys.
    - **Least Privilege:** Granting only the permissions needed (and nothing more).
    - **Policies:** JSON documents defining permissions.

### 3. Observability
- **Concept:** Knowing what's happening.
- **Key Knowledge:**
    - **CloudWatch:** Metrics and Logs.
    - **CloudTrail:** Auditing API calls (who deleted the database?).

---

## Senior -> Lead: Cost & Scale
**Goal:** Optimizes for millions of users and keeps the bill in check.

### 1. Advanced Compute
- **Concept:** Orchestration at scale.
- **Key Knowledge:**
    - **EKS / ECS:** Managed Kubernetes or Container services.
    - **Spot Instances:** Using spare capacity for 90% discounts.
    - **Auto Scaling Groups:** Automatically adding/removing servers based on load.

### 2. Data Strategy
- **Concept:** Big data and speed.
- **Key Knowledge:**
    - **DynamoDB:** NoSQL for single-digit millisecond latency at any scale.
    - **ElastiCache (Redis):** In-memory caching to offload the DB.
    - **Aurora:** Cloud-native relational DB with auto-scaling storage.

### 3. Security & Governance
- **Concept:** Enterprise-grade control.
- **Key Knowledge:**
    - **KMS:** Managing encryption keys.
    - **WAF:** Web Application Firewall to block attacks.
    - **Organizations:** Managing multiple AWS accounts (Billing, Security boundaries).
