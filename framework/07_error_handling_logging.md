[← Back to Index](./README.md)

# 7. Error Handling & Logging

When things go wrong (and they will), you need to handle it gracefully and know exactly what happened.

## Junior -> Mid: The Basics
**Goal:** Can catch errors and print logs.

### 1. Try / Catch
- **Concept:** preventing the server from crashing.
- **Key Skills:**
    - Wrapping risky code (DB calls) in try/catch blocks.
    - Returning a 500 status code instead of a raw stack trace to the user.

### 2. Basic Logging
- **Concept:** `print` is not enough.
- **Key Skills:**
    - Using a logger library (not `console.log` or `System.out`).
    - Understanding Log Levels: DEBUG, INFO, WARN, ERROR.

---

## Mid -> Senior: Observability
**Goal:** Creates a system where errors are predictable and debugging is easy.

### 1. Centralized Error Handling
- **Concept:** Don't repeat try/catch in every controller.
- **Key Knowledge:**
    - **Global Exception Handler:** A single place that catches all uncaught errors.
    - **Custom Exceptions:** Throwing `UserNotFoundException` and mapping it automatically to 404.
    - **Standard Error Responses:** Always returning `{ "error": "code", "message": "..." }`.

### 2. Structured Logging
- **Concept:** Logs for machines, not just humans.
- **Key Knowledge:**
    - **JSON Logs:** Outputting logs as JSON objects so tools like Splunk/ELK can parse them.
    - **Context:** Including `userId`, `ipAddress`, and `endpoint` in every log line automatically.

### 3. Request Tracing
- **Concept:** Following a request through the system.
- **Key Knowledge:**
    - **Correlation IDs:** Generating a unique ID (UUID) for every request and passing it to all logs and downstream services.

---

## Senior -> Lead: Reliability Engineering
**Goal:** Proactively monitors system health and debugs distributed failures.

### 1. Distributed Tracing
- **Concept:** Visualizing the path across microservices.
- **Key Knowledge:**
    - **OpenTelemetry:** The standard for collecting traces.
    - **Spans:** Measuring exactly how long the DB took vs the external API call.
    - **Tools:** Jaeger, Zipkin, Datadog.

### 2. Error Budgeting & Alerting
- **Concept:** Knowing when to wake up the on-call engineer.
- **Key Knowledge:**
    - **Sentry / Rollbar:** Tools that aggregate crash reports and notify you of new bugs.
    - **Alert Fatigue:** Tuning alerts so you only get paged for real problems (high error rate), not just one random failure.

### 3. Audit Logging
- **Concept:** Legal and security requirements.
- **Key Knowledge:**
    - **Immutability:** Ensuring logs cannot be changed.
    - **Business vs System Logs:** Recording "User X changed setting Y" separately from "DB connection failed".
