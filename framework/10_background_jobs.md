[← Back to Index](./README.md)

# 10. Background Jobs & Task Queues

Users hate waiting. If a task takes more than 500ms, put it in the background.

## Junior -> Mid: The Basics
**Goal:** Can offload a simple task (like sending email) to a worker.

### 1. The Concept of Async Work
- **Concept:** Fire and forget.
- **Key Skills:**
    - Identifying slow tasks: Image resizing, PDF generation, Email sending.
    - Understanding the flow: Web App -> Queue -> Worker.

### 2. Basic Job Implementation
- **Concept:** Defining the work.
- **Key Skills:**
    - Creating a Job Class (e.g., `SendWelcomeEmailJob`).
    - Dispatching the job: `Queue.push(new SendWelcomeEmailJob(user))`.

---

## Mid -> Senior: Reliability & Scale
**Goal:** Ensures jobs are processed reliably, even when things fail.

### 1. Queue Backends
- **Concept:** Where the jobs live.
- **Key Knowledge:**
    - **Redis (Sidekiq/Bull):** Fast, in-memory. Good for most cases.
    - **SQS / RabbitMQ:** Durable, persistent queues for critical data.

### 2. Failure Handling
- **Concept:** Jobs fail.
- **Key Knowledge:**
    - **Retries:** Automatically retrying a job 3 times with exponential backoff.
    - **Dead Letter Queues (DLQ):** Where jobs go to die after max retries, so you can inspect them later.
    - **Idempotency:** Ensuring that running the same job twice doesn't send two emails.

### 3. Scheduling
- **Concept:** Cron jobs.
- **Key Knowledge:**
    - **Recurring Tasks:** Running a report every night at 2 AM.
    - **Delayed Jobs:** "Send this reminder in 24 hours."

---

## Senior -> Lead: Distributed Systems
**Goal:** Manages high-throughput queues and complex workflows.

### 1. Workflow Orchestration
- **Concept:** Jobs that depend on other jobs.
- **Key Knowledge:**
    - **Chains / Batches:** "Run Job A, then Job B." or "Run 100 jobs, then notify me when ALL are done."
    - **Sagas:** Managing long-running distributed transactions across multiple services.

### 2. Scaling Workers
- **Concept:** Processing faster.
- **Key Knowledge:**
    - **Concurrency:** Threading vs Event Loops in workers.
    - **Autoscaling:** Spinning up more worker servers based on queue depth (lag).
    - **Priority Queues:** Processing "Premium User" jobs before "Free User" jobs.

### 3. Observability
- **Concept:** Monitoring the factory floor.
- **Key Knowledge:**
    - **Throughput & Latency:** Measuring how many jobs/sec and how long they wait in the queue.
    - **Stuck Workers:** Detecting when a worker process has hung.
