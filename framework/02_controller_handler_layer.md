[← Back to Index](./README.md)

# 2. Controller / Handler Layer

The controller is the "traffic cop" of your application. It receives the request, decides what to do, and returns the response.

## Junior -> Mid: The Basics
**Goal:** Can write a clean controller method that handles a specific feature.

### 1. The Handler Function
- **Concept:** A function or class method that maps 1-to-1 with a route.
- **Key Skills:**
    - Accessing request data (params, body).
    - Calling a function to get data (e.g., `getUser(id)`).
    - Returning the result as JSON.

### 2. Basic Separation of Concerns
- **Concept:** Don't put everything in the controller.
- **Key Skills:**
    - **"Fat Models, Skinny Controllers":** Moving complex logic out of the controller.
    - **Service Delegation:** Calling a `UserService` instead of writing raw SQL inside the controller.

### 3. Dependency Injection (Basic)
- **Concept:** Getting access to services.
- **Key Skills:**
    - Constructor injection (e.g., passing `UserService` into `UserController`).
    - Using framework annotations like `@Autowired` or `Inject`.

---

## Mid -> Senior: Patterns & Best Practices
**Goal:** Writes maintainable, testable controllers that adhere to strict architectural boundaries.

### 1. Advanced Input Handling
- **Concept:** Robustly handling what the user sends.
- **Key Knowledge:**
    - **DTOs (Data Transfer Objects):** Defining explicit classes/types for incoming data instead of using raw maps/dictionaries.
    - **Binding & Validation:** Automatically mapping JSON to DTOs and validating fields (e.g., `@Valid` in Spring, Pydantic in FastAPI).

### 2. Response Standardization
- **Concept:** Consistent API responses.
- **Key Knowledge:**
    - **Global Response Wrappers:** Ensuring every response has a standard format `{ "data": ..., "meta": ... }`.
    - **Presenters / Serializers:** Transforming domain entities into public-facing JSON (hiding password hashes, formatting dates).

### 3. Asynchronous Handlers
- **Concept:** Non-blocking operations.
- **Key Knowledge:**
    - **Async/Await:** Writing controllers that don't block the thread while waiting for DB/Network.
    - **Promises/Futures:** Handling concurrent operations within a single request.

---

## Senior -> Lead: Architecture & Abstractions
**Goal:** Designs the controller layer to be framework-agnostic and highly decoupled.

### 1. Hexagonal Architecture (Ports & Adapters)
- **Concept:** The controller is just an "Adapter".
- **Key Knowledge:**
    - **Decoupling:** Ensuring the core business logic knows *nothing* about HTTP, JSON, or the web framework.
    - **Interface-based Design:** Controllers depend on interfaces (Ports), not concrete service implementations.

### 2. Generic & Meta-Programming
- **Concept:** Reducing boilerplate.
- **Key Knowledge:**
    - **Generic Controllers:** Creating a base `CrudController<T>` that handles standard GET/POST/PUT/DELETE for any resource.
    - **Decorators/Annotations:** Creating custom decorators to handle cross-cutting concerns (e.g., `@RateLimit`, `@Cache(ttl=60)`).

### 3. API Versioning Strategies
- **Concept:** Evolving the API without breaking clients.
- **Key Knowledge:**
    - **URI Versioning:** `/v1/users` vs `/v2/users`.
    - **Header Versioning:** `Accept: application/vnd.myapi.v1+json`.
    - **Evolutionary Database Design:** How controller versioning impacts the underlying data model.
