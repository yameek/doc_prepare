[← Back to Index](./README.md)

# 3. Containers & Orchestration

The standard unit of software delivery.

## Junior -> Mid: The Basics
**Goal:** Can containerize an app and run it locally or on a simple orchestrator.

### 1. Docker
- **Concept:** "It works on my machine."
- **Key Skills:**
    - **Dockerfile:** Writing a recipe to build your image.
    - **Commands:** `docker build`, `docker run`, `docker ps`, `docker logs`.
    - **Docker Compose:** Running multi-container apps (App + DB) locally.

### 2. Kubernetes Concepts
- **Concept:** Managing containers across servers.
- **Key Skills:**
    - **Pod:** The smallest unit (one or more containers).
    - **Deployment:** Managing replicas and updates.
    - **Service:** Exposing pods to the network.

---

## Mid -> Senior: Production Kubernetes
**Goal:** Manages a production cluster, handles upgrades, and troubleshoots.

### 1. Advanced Docker
- **Concept:** Optimized images.
- **Key Knowledge:**
    - **Multi-stage Builds:** Compiling in a heavy image, running in a tiny one (Distroless/Alpine).
    - **Layer Caching:** Speeding up builds by ordering instructions correctly.
    - **Image Scanning:** Finding vulnerabilities (Trivy).

### 2. Kubernetes Resources
- **Concept:** The full toolkit.
- **Key Knowledge:**
    - **Ingress:** Routing external HTTP traffic to services.
    - **ConfigMap / Secret:** Injecting configuration.
    - **StatefulSet:** Running databases (pods with stable identities).
    - **Helm:** The package manager for K8s (templating YAML).

### 3. Troubleshooting
- **Concept:** Why is my pod crashing?
- **Key Knowledge:**
    - `kubectl describe pod`: Reading events.
    - `kubectl logs`: Reading application output.
    - `kubectl exec`: Shelling into a running container.

---

## Senior -> Lead: Platform Engineering
**Goal:** Builds a platform on top of Kubernetes for other developers.

### 1. Advanced Orchestration
- **Concept:** Extending K8s.
- **Key Knowledge:**
    - **Operators / CRDs:** Custom resources (e.g., "PostgresCluster") managed by code.
    - **Service Mesh (Istio/Linkerd):** mTLS, traffic splitting, and observability without changing app code.
    - **Network Policies:** Firewalls inside the cluster.

### 2. Scaling & Scheduling
- **Concept:** Efficiency.
- **Key Knowledge:**
    - **HPA / VPA:** Horizontal (more pods) vs Vertical (bigger pods) autoscaling.
    - **Cluster Autoscaler / Karpenter:** Adding nodes when the cluster is full.
    - **Affinity / Taints:** Controlling exactly where pods land (e.g., GPU nodes).

### 3. Security
- **Concept:** Hardening the cluster.
- **Key Knowledge:**
    - **RBAC:** Who can do what in the cluster.
    - **OPA Gatekeeper / Kyverno:** Policy enforcement (e.g., "No images from Docker Hub allowed").
    - **Pod Security Standards:** Preventing root containers.
