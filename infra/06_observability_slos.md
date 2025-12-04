[← Back to Index](./README.md)

# 6. Observability & SLOs

"Monitoring tells you the system is down. Observability tells you *why*."

## Junior -> Mid: The Basics
**Goal:** Can set up basic dashboards and alerts.

### 1. The Three Pillars
- **Concept:** The data types.
- **Key Skills:**
    - **Metrics:** Numbers (CPU usage, Request Count).
    - **Logs:** Text (Error messages, Access logs).
    - **Traces:** Timing (How long did the DB query take?).

### 2. Tools
- **Concept:** The stack.
- **Key Skills:**
    - **Prometheus:** Scraping metrics.
    - **Grafana:** Visualizing data.
    - **Loki / ELK:** Querying logs.

---

## Mid -> Senior: SLOs & Alerting
**Goal:** Defines what "healthy" means and alerts only when it matters.

### 1. Service Level Objectives (SLOs)
- **Concept:** Measuring user happiness.
- **Key Knowledge:**
    - **SLI (Indicator):** "Latency is < 200ms".
    - **SLO (Objective):** "99.9% of requests meet the SLI".
    - **Error Budget:** How much you can fail before you stop shipping features.

### 2. Alerting Strategy
- **Concept:** Avoiding pager fatigue.
- **Key Knowledge:**
    - **Symptom-based Alerting:** Alert on "High Error Rate", not "High CPU".
    - **Alertmanager:** Routing alerts to Slack/PagerDuty.
    - **Runbooks:** Linking every alert to a doc explaining how to fix it.

### 3. Distributed Tracing
- **Concept:** Following the needle.
- **Key Knowledge:**
    - **Jaeger / Tempo:** Visualizing traces.
    - **Instrumentation:** Adding trace IDs to your code (OpenTelemetry).

---

## Senior -> Lead: Profiling & Cost
**Goal:** Optimizes performance and storage costs of observability.

### 1. Continuous Profiling
- **Concept:** Code-level visibility.
- **Key Knowledge:**
    - **Parca / Pyroscope:** Seeing which function is eating CPU across the fleet.
    - **Flame Graphs:** Visualizing the stack.

### 2. Advanced Alerting
- **Concept:** Math-based alerts.
- **Key Knowledge:**
    - **Burn Rate Alerts:** "We are burning our error budget too fast" (predicting failure).
    - **Multi-Window Alerts:** Reducing false positives by checking short and long windows.

### 3. Data Management
- **Concept:** Handling massive volume.
- **Key Knowledge:**
    - **Sampling:** Keeping only 1% of traces to save money.
    - **Retention Policies:** Downsampling old metrics.
    - **Cardinality:** Understanding why "User ID" as a metric label crashes Prometheus.
