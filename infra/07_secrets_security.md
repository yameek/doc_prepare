[← Back to Index](./README.md)

# 7. Secrets & Security Automation

Secrets management is the difference between a secure platform and a data breach.

## Junior -> Mid: The Basics
**Goal:** Never commits secrets to git.

### 1. Secret Management
- **Concept:** Where to put passwords.
- **Key Skills:**
    - **Env Vars:** Injecting secrets at runtime.
    - **Kubernetes Secrets:** Base64 encoded secrets in the cluster.
    - **Sealed Secrets:** Encrypting secrets so they can be stored in Git safely.

### 2. Scanning
- **Concept:** Finding mistakes.
- **Key Skills:**
    - **Trivy:** Scanning container images for CVEs.
    - **GitLeaks:** Scanning the repo for accidental keys.

---

## Mid -> Senior: Dynamic Secrets & Policy
**Goal:** Automates rotation and enforces least privilege.

### 1. Vault
- **Concept:** The gold standard.
- **Key Knowledge:**
    - **Dynamic Secrets:** "Give me a Postgres user valid for 1 hour." (Vault creates it and deletes it later).
    - **Transit Engine:** Encryption as a Service.
    - **External Secrets Operator:** Syncing Vault secrets into Kubernetes.

### 2. Compliance Scanning
- **Concept:** Are we following the rules?
- **Key Knowledge:**
    - **CIS Benchmarks:** Standard hardening rules for Linux/K8s.
    - **Kube-bench:** Running CIS checks on your cluster.
    - **Prowler / ScoutSuite:** Auditing your AWS account for security gaps.

### 3. Network Security
- **Concept:** Zero Trust.
- **Key Knowledge:**
    - **Network Policies:** "Frontend can talk to Backend, but not Database."
    - **mTLS:** Encrypting traffic between pods (Istio/Linkerd).

---

## Senior -> Lead: Supply Chain & Runtime Defense
**Goal:** Secures the entire software lifecycle.

### 1. Supply Chain Security
- **Concept:** Trusting your code.
- **Key Knowledge:**
    - **Cosign / Sigstore:** Signing container images to prove they came from your CI.
    - **SBOM:** Generating a list of every library in your software.
    - **Admission Controllers:** "Reject any image that isn't signed by us."

### 2. Runtime Threat Detection
- **Concept:** Catching the hacker.
- **Key Knowledge:**
    - **Falco:** "Alert if a container spawns a shell or modifies /etc."
    - **eBPF:** Monitoring syscalls at the kernel level with low overhead.

### 3. Identity
- **Concept:** No more long-lived keys.
- **Key Knowledge:**
    - **SPIFFE/SPIRE:** Identity for workloads (giving a pod an ID card).
    - **OIDC Federation:** Letting GitHub Actions talk to AWS without an Access Key.
