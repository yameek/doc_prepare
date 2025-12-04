[← Back to Index](./README.md)

# 5. CI/CD & GitOps

The factory that builds and ships your code.

## Junior -> Mid: The Basics
**Goal:** Can set up a simple pipeline to test and deploy.

### 1. Git Workflow
- **Concept:** Source control.
- **Key Skills:**
    - **Branching:** Feature branches, Pull Requests.
    - **Commits:** Writing clear messages.

### 2. CI (Continuous Integration)
- **Concept:** Testing every change.
- **Key Skills:**
    - **Pipeline Steps:** Checkout -> Install Deps -> Lint -> Test.
    - **GitHub Actions / GitLab CI:** Writing YAML configuration.

### 3. CD (Continuous Deployment)
- **Concept:** Shipping it.
- **Key Skills:**
    - **Artifacts:** Building a Docker image or binary.
    - **Deploy:** SSH-ing to a server and updating the app (basic).

---

## Mid -> Senior: GitOps & Optimization
**Goal:** Implements GitOps and optimizes build times.

### 1. GitOps (ArgoCD / Flux)
- **Concept:** Git is the source of truth for the cluster.
- **Key Knowledge:**
    - **Pull Model:** The cluster pulls changes from Git (no `kubectl apply` from CI).
    - **Sync:** Automatically correcting drift.
    - **App of Apps:** Managing hundreds of microservices.

### 2. Build Optimization
- **Concept:** Fast feedback loops.
- **Key Knowledge:**
    - **Caching:** Caching `node_modules` or Docker layers.
    - **Parallelism:** Running tests in parallel.
    - **Docker Buildx:** Building multi-arch images (ARM/AMD).

### 3. Advanced Git
- **Concept:** Clean history.
- **Key Knowledge:**
    - **Rebase:** Keeping history linear.
    - **Conventional Commits:** Standardizing messages for automated changelogs.
    - **Signed Commits:** Verifying identity with GPG.

---

## Senior -> Lead: Progressive Delivery
**Goal:** Deploys safely with zero downtime and automated rollbacks.

### 1. Deployment Strategies
- **Concept:** Reducing blast radius.
- **Key Knowledge:**
    - **Blue/Green:** Two full environments, switching traffic.
    - **Canary:** Rolling out to 1% of users, then 10%, then 100%.
    - **Flagger / Argo Rollouts:** Automating canary analysis based on metrics.

### 2. Pipeline Security
- **Concept:** Securing the supply chain.
- **Key Knowledge:**
    - **OIDC:** Authenticating CI to Cloud without long-lived keys.
    - **SLSA:** Provenance (proving *where* the binary came from).
    - **SBOM:** Software Bill of Materials.

### 3. Self-Hosted Runners
- **Concept:** Scale and security.
- **Key Knowledge:**
    - **Autoscaling Runners:** Spinning up CI agents on Kubernetes.
    - **Private Networking:** Accessing internal resources during tests.
