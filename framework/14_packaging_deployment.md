# 14. Packaging & Deployment Helpers

It works on my machine... but it needs to work on the server.

## Junior -> Mid: The Basics
**Goal:** Can build the project and run it on a server.

### 1. Build Scripts
- **Concept:** Turning code into an artifact.
- **Key Skills:**
    - `npm build` / `mvn package` / `go build`.
    - Understanding the difference between Source Code and Compiled Artifacts (dist/target folders).

### 2. Environment Setup
- **Concept:** Getting the server ready.
- **Key Skills:**
    - Installing dependencies (`npm install --production`).
    - Setting environment variables.
    - Running the start command (`npm start`).

---

## Mid -> Senior: Containers & Orchestration
**Goal:** Packages applications for consistent deployment anywhere.

### 1. Dockerization
- **Concept:** "It works on my machine" -> "It works in the container".
- **Key Knowledge:**
    - **Dockerfile:** Writing optimized multi-stage builds (build in one image, run in a smaller one).
    - **Entrypoints:** Configuring how the container starts.
    - **Networking:** Exposing ports.

### 2. Health Checks
- **Concept:** "Are you alive?"
- **Key Knowledge:**
    - **Liveness Probe:** "Is the process running?" (If no, restart).
    - **Readiness Probe:** "Can you accept traffic?" (e.g., DB connection is established).
    - Implementing `/health` and `/ready` endpoints.

### 3. Graceful Shutdown
- **Concept:** Dying with dignity.
- **Key Knowledge:**
    - **Signal Handling:** Catching `SIGTERM`.
    - **Draining:** Finishing current requests before exiting.
    - **Cleanup:** Closing DB connections and file handles.

---

## Senior -> Lead: CI/CD & Operations
**Goal:** Automates the entire pipeline from commit to production.

### 1. CI/CD Pipelines
- **Concept:** Automating the factory.
- **Key Knowledge:**
    - **GitHub Actions / GitLab CI:** Defining steps to Lint -> Test -> Build -> Push Docker Image -> Deploy.
    - **Blue/Green Deployment:** Deploying the new version alongside the old one, then switching traffic.

### 2. Infrastructure as Code (IaC)
- **Concept:** Reproducible environments.
- **Key Knowledge:**
    - **Terraform / CloudFormation:** Provisioning servers, load balancers, and databases via code.
    - **GitOps:** Using Git as the source of truth for the state of the cluster (ArgoCD).

### 3. Observability & SRE
- **Concept:** Keeping it running.
- **Key Knowledge:**
    - **SLOs / SLIs:** Defining Service Level Objectives (e.g., "99.9% of requests must be under 200ms").
    - **Chaos Engineering:** Intentionally breaking things to test resilience.
