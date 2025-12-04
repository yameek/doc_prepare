[← Back to Main Index](../README.md)

# Infrastructure & DevOps Concepts

This documentation covers the "minimum-viable-skill matrix" for DevOps, Platform, and SRE roles. It is structured to guide you from Junior to Lead.

## Table of Contents

1.  [Core OS & Networking](./01_core_os_networking.md)
    *   *Linux Internals, CLI, TCP/IP, DNS*
2.  [Cloud-Native Services](./02_cloud_native_services.md)
    *   *Compute, Storage, Networking, IAM (AWS/GCP/Azure)*
3.  [Containers & Orchestration](./03_containers_orchestration.md)
    *   *Docker, Kubernetes, Helm, Service Mesh*
4.  [Infrastructure-as-Code (IaC)](./04_iac.md)
    *   *Terraform, Ansible, Policy-as-Code*
5.  [CI/CD & GitOps](./05_cicd_gitops.md)
    *   *Pipelines, ArgoCD, Progressive Delivery*
6.  [Observability & SLOs](./06_observability_slos.md)
    *   *Metrics, Logs, Traces, Alerting*
7.  [Secrets & Security Automation](./07_secrets_security.md)
    *   *Vault, Supply Chain Security, Runtime Defense*
8.  [Git, Scripting & Automation Glue](./08_git_scripting_automation.md)
    *   *Bash, Python/Go, Advanced Git*
9.  [Backup, DR & Compliance](./09_backup_dr_compliance.md)
    *   *Disaster Recovery, SOC-2, Auditing*
10. [Cost & Performance Optimisation](./10_cost_performance.md)
    *   *FinOps, Spot Instances, Right-sizing*
11. [Soft-skills & Process](./11_soft_skills_process.md)
    *   *Incident Response, ADRs, Documentation*

## The "Prove-it" Checklist
If you can build these 6 artifacts, you are qualified for a mid-level role:

1.  **Terraform Module:** VPC, EKS, IRSA, ArgoCD.
2.  **GitHub Actions:** Build multi-arch image, sign (cosign), scan (trivy), update ArgoCD manifest.
3.  **Helm Chart:** HPA, VPA, PDB, NetworkPolicy, Canary (Flagger).
4.  **Observability:** Prometheus Rule + Grafana Dashboard (p99 latency/error rate) + Alertmanager.
5.  **Ansible Playbook:** Harden Ubuntu to CIS Level 1 + Audit Report.
6.  **Demo:** 5-minute recording of the whole flow (Plan -> Apply -> Sync -> Destroy).
