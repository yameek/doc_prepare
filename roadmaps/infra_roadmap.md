[← Back to Main Index](../README.md)

# Infrastructure & DevOps Mastery Roadmap

This roadmap guides you through the "minimum-viable-skill matrix" for DevOps/SRE roles.

## Phase 1: The Operator (Junior -> Mid)
**Focus:** Linux, Scripting & Basic Cloud.
**Goal:** Can manage a server and deploy an app manually.

1.  **Linux:** Master the CLI (`grep`, `ps`, `curl`). Understand permissions.
2.  **Networking:** Understand IP, Ports, DNS.
3.  **Cloud Basics:** Launch an EC2 instance, set up a VPC, create an RDS database.
4.  **Docker:** Write a Dockerfile and run containers locally.
5.  **Scripting:** Write Bash scripts to automate daily tasks.
6.  **Git:** Master the basic workflow (branch, commit, push).

## Phase 2: The Automator (Mid -> Senior)
**Focus:** IaC, Kubernetes & CI/CD.
**Goal:** Can build a platform where "everything is code".

1.  **IaC:** Learn Terraform. Stop clicking in the console.
2.  **Kubernetes:** Deploy apps with Deployments, Services, and Ingress.
3.  **CI/CD:** Build pipelines (GitHub Actions) to test and build images.
4.  **Observability:** Set up Prometheus and Grafana. Create basic dashboards.
5.  **Secrets:** Use Vault or Sealed Secrets. Stop committing keys.
6.  **Cost:** Right-size your instances and use Spot where possible.

## Phase 3: The Platform Engineer (Senior -> Lead)
**Focus:** Resilience, Scale & Governance.
**Goal:** Build a self-service platform for developers.

1.  **GitOps:** Implement ArgoCD. The cluster syncs from Git.
2.  **Advanced K8s:** Write Custom Controllers/Operators. Use Service Mesh.
3.  **Security:** Implement Policy-as-Code (OPA/Kyverno) and Runtime Defense (Falco).
4.  **Reliability:** Define SLOs and Error Budgets. Run Game Days (Chaos Engineering).
5.  **Compliance:** Automate evidence collection for SOC-2/ISO audits.
6.  **Culture:** Write ADRs, run blameless post-mortems, and mentor the team.
