# 1. Request / Response Life-cycle

Understanding how a web framework processes an incoming HTTP request and generates a response is the foundation of backend development.

## Junior -> Mid: The Basics
**Goal:** Can build a simple API endpoint, read inputs, and return outputs.

### 1. Router
- **Concept:** The entry point. It maps an HTTP Method (GET, POST) + URL Path (`/users/1`) to a specific function (Handler/Controller).
- **Key Skills:**
    - Defining static routes (`/health`).
    - Defining dynamic routes with parameters (`/items/:id`).
    - Understanding HTTP verbs: GET (read), POST (create), PUT/PATCH (update), DELETE (remove).

### 2. Middleware (The "In-Between" Code)
- **Concept:** Functions that run *before* or *after* your main handler.
- **Key Skills:**
    - Using built-in middleware (e.g., a logger that prints "GET /users 200 OK").
    - Understanding that middleware runs in a sequence.

### 3. Request Object
- **Concept:** Represents what the client sent.
- **Key Skills:**
    - Reading Query Parameters (`?search=apple`).
    - Reading Path Parameters (`/users/123` -> `id: 123`).
    - Reading the Body (JSON payloads).
    - Reading Headers (e.g., `User-Agent`).

### 4. Response Object
- **Concept:** Represents what you send back.
- **Key Skills:**
    - Setting HTTP Status Codes (200 OK, 404 Not Found, 500 Error).
    - Sending JSON data (`res.json({...})`).
    - Setting basic Headers (e.g., `Content-Type`).

---

## Mid -> Senior: Deep Dive & Control
**Goal:** Can handle complex flows, optimize performance, and debug lifecycle issues.

### 1. Advanced Routing
- **Concept:** Complex matching and grouping.
- **Key Knowledge:**
    - **Route Groups/Mounting:** Organizing routes by feature (`/api/v1/users`, `/api/v1/orders`).
    - **Regex Constraints:** Matching routes only if parameters match a pattern (e.g., `id` must be numeric).
    - **Reverse Routing:** Generating URLs from route names (prevents hardcoded strings).

### 2. Middleware Patterns
- **Concept:** Middleware as a powerful control flow tool.
- **Key Knowledge:**
    - **Ordering Matters:** Why Auth middleware must run before Business Logic.
    - **Short-circuiting:** Stopping the request early (e.g., returning 403 Forbidden inside middleware).
    - **Context Passing:** Attaching data to the request object (e.g., `req.user`) for downstream handlers to use.
    - **Error Handling Middleware:** Special middleware that catches exceptions thrown in the chain.

### 3. Request/Response Nuances
- **Concept:** Fine-grained control over HTTP.
- **Key Knowledge:**
    - **Content Negotiation:** Checking `Accept` headers to return JSON vs XML vs HTML.
    - **Cookies & Sessions:** Securely setting and reading HttpOnly cookies.
    - **Streaming Responses:** Sending data in chunks (e.g., large file downloads) to avoid loading everything into memory.
    - **File Uploads:** Handling `multipart/form-data` streams efficiently.

---

## Senior -> Lead: Architecture & Internals
**Goal:** Understands how the framework works under the hood and can make high-level architectural decisions.

### 1. Routing Internals & Performance
- **Concept:** How the framework finds the right handler in microseconds.
- **Key Knowledge:**
    - **Radix Trees / Tries:** Understanding that high-performance routers don't just loop through a list (O(n)); they use tree structures (O(k)) for lookups.
    - **Route Caching:** Mechanisms to speed up route resolution.
    - **Framework Overhead:** Evaluating the latency cost of the routing engine itself.

### 2. The Application Lifecycle
- **Concept:** What happens from server boot to shutdown.
- **Key Knowledge:**
    - **Boot Process:** Dependency injection wiring, configuration loading, and warm-up tasks.
    - **Graceful Shutdown:** Handling `SIGTERM`, stopping accepting new requests, and allowing in-flight requests to finish (draining).
    - **Event Loops vs Thread Pools:** Understanding the concurrency model (Node.js event loop vs Java/Go thread-per-request) and how it impacts blocking middleware.

### 3. Advanced Interception (AOP)
- **Concept:** Cross-cutting concerns beyond simple middleware.
- **Key Knowledge:**
    - **Interceptors vs Filters:** Subtle differences in some frameworks (e.g., Spring) regarding access to the actual handler method or exception context.
    - **Zero-Copy Handling:** Techniques to pass data from socket to disk/network without copying buffers in userspace (performance critical for proxies/gateways).
