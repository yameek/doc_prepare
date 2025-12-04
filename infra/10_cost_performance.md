[← Back to Index](./README.md)

# 10. Cost & Performance Optimisation

The cloud is infinite, but your budget is not.

## Junior -> Mid: The Basics
**Goal:** Understands where the money goes.

### 1. Cost Awareness
- **Concept:** Cloud billing.
- **Key Skills:**
    - **Resource Types:** Knowing that a `t3.micro` is cheaper than a `c5.2xlarge`.
    - **Idle Resources:** Turning off dev servers at night.

### 2. Basic Performance
- **Concept:** Right-sizing.
- **Key Skills:**
    - **Monitoring:** Seeing that CPU is at 5% and downsizing the instance.
    - **Instance Types:** Choosing Compute Optimized (C family) vs Memory Optimized (R family).

---

## Mid -> Senior: Automated Optimization
**Goal:** Implements tools to save money automatically.

### 1. Compute Optimization
- **Concept:** Paying less for the same work.
- **Key Knowledge:**
    - **Spot Instances:** Handling interruptions for stateless workloads.
    - **Karpenter:** Aggressive bin-packing of Kubernetes nodes (consolidating pods to fewer nodes).
    - **Mixed Instances:** Running Spot and On-Demand in the same Auto Scaling Group.

### 2. Storage Optimization
- **Concept:** Data tiers.
- **Key Knowledge:**
    - **S3 Intelligent-Tiering:** Automatically moving rarely accessed files to cheaper storage.
    - **Lifecycle Rules:** Deleting old backups.

### 3. Tools
- **Concept:** Visibility.
- **Key Knowledge:**
    - **Kubecost:** Breaking down K8s spend by Namespace/Team.
    - **AWS Cost Explorer:** Analyzing trends.

---

## Senior -> Lead: FinOps
**Goal:** Aligns engineering with finance.

### 1. Anomaly Detection
- **Concept:** Catching mistakes early.
- **Key Knowledge:**
    - **AWS Cost Anomaly Detection:** "Why did our bill jump 50% yesterday?" (e.g., a loop creating resources).
    - **Budgets:** Setting hard alerts on spend.

### 2. Strategic Savings
- **Concept:** Long-term commitment.
- **Key Knowledge:**
    - **Savings Plans / RIs:** Committing to 1-3 years of usage for significant discounts.
    - **Enterprise Agreements:** Negotiating custom rates with the cloud provider.

### 3. Performance Tuning
- **Concept:** Getting more out of the hardware.
- **Key Knowledge:**
    - **Kernel Tuning:** Optimizing network stacks for high throughput.
    - **Architecture:** Moving from x86 to ARM (Graviton) for better price/performance.
