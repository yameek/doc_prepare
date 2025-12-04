[← Back to Index](./README.md)

# 9. Backup, DR & Compliance

The things that keep the CTO awake at night.

## Junior -> Mid: The Basics
**Goal:** Can restore a database and follow security rules.

### 1. Backups
- **Concept:** Saving data.
- **Key Skills:**
    - **Snapshots:** RDS/EBS snapshots.
    - **Point-in-Time Recovery (PITR):** Restoring a DB to "5 minutes ago".
    - **Testing:** Actually trying to restore the backup (Schrödinger's Backup).

### 2. Compliance Basics
- **Concept:** Following the law.
- **Key Skills:**
    - **Encryption:** Ensuring S3 buckets and DBs are encrypted at rest.
    - **Access:** Not sharing passwords.

---

## Mid -> Senior: Disaster Recovery (DR)
**Goal:** Can recover the entire platform if a region fails.

### 1. DR Strategies
- **Concept:** How fast do we need to be back?
- **Key Knowledge:**
    - **RTO (Recovery Time Objective):** How long can we be down?
    - **RPO (Recovery Point Objective):** How much data can we lose?
    - **Cross-Region Replication:** Replicating S3/DBs to another region (e.g., us-east-1 -> us-west-2).

### 2. Lifecycle Policies
- **Concept:** Data governance.
- **Key Knowledge:**
    - **Retention:** "Keep logs for 90 days, then delete."
    - **Archival:** Moving old data to S3 Glacier (cheaper).

### 3. Game Days
- **Concept:** Practice.
- **Key Knowledge:**
    - **Simulation:** Intentionally failing a region or service to test the runbooks.
    - **Post-Mortem:** Learning from the test.

---

## Senior -> Lead: Audit & Governance
**Goal:** Passes SOC-2 / ISO-27001 audits.

### 1. Compliance Frameworks
- **Concept:** The checklist.
- **Key Knowledge:**
    - **SOC-2 / ISO-27001:** Security controls.
    - **HIPAA / PCI-DSS:** Health and Payment data rules.
    - **GDPR:** Privacy and "Right to be Forgotten".

### 2. Automated Evidence
- **Concept:** Proving it to the auditor.
- **Key Knowledge:**
    - **AWS Config:** "Show me a log of every security group change in the last year."
    - **Artifacts:** Generating automated reports from your CI/CD and Infrastructure.

### 3. Data Sovereignty
- **Concept:** Where data lives legally.
- **Key Knowledge:**
    - **Residency:** "German user data must stay in Germany."
    - **Sharding:** Architecting the system to keep data in specific regions.
