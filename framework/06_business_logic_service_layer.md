# 6. Business Logic / Service Layer

This is the heart of your application. It contains the rules that make your business unique, independent of the web framework or database.

## Junior -> Mid: The Basics
**Goal:** Can write code that solves the problem, separated from the controller.

### 1. The Service Class
- **Concept:** A place to put the logic.
- **Key Skills:**
    - Creating a `UserService` class.
    - Writing methods like `registerUser(email, password)` that handle the steps (hash password, save to DB, send email).
    - Calling this service from the Controller.

### 2. Basic Reusability
- **Concept:** Don't repeat yourself (DRY).
- **Key Skills:**
    - Reusing the same service method for the API and a CLI command.
    - Keeping the Controller "dumb" (it just passes data).

---

## Mid -> Senior: Isolation & Testability
**Goal:** Writes pure business logic that is easy to test and change.

### 1. Dependency Injection (DI)
- **Concept:** Asking for what you need, not creating it.
- **Key Knowledge:**
    - **Inversion of Control:** The service asks for a `UserRepository` interface, not a specific SQL implementation.
    - **Mocking:** Easily swapping real DB calls for fake ones during unit tests.

### 2. Domain Models vs Data Models
- **Concept:** The database table is not the business object.
- **Key Knowledge:**
    - **Rich Domain Models:** Classes that have methods (`order.calculateTotal()`), not just data bags.
    - **Anemic Domain Model (Anti-pattern):** Avoiding services that just do `get` and `set` on dumb objects.

### 3. Transaction Management
- **Concept:** Ensuring data consistency.
- **Key Knowledge:**
    - **Transactional Boundaries:** Marking a service method as `@Transactional` so that if the email fails, the DB insert rolls back.
    - **Propagation:** How transactions behave when one service calls another.

---

## Senior -> Lead: Domain-Driven Design (DDD)
**Goal:** Models complex business requirements using advanced architectural patterns.

### 1. DDD Concepts
- **Concept:** Aligning code with business language.
- **Key Knowledge:**
    - **Ubiquitous Language:** Using the same terms in code as the business experts use.
    - **Bounded Contexts:** Defining clear boundaries where a specific model applies (e.g., "Product" means something different in Sales vs Shipping).
    - **Aggregates & Roots:** Grouping related objects that must be treated as a single unit for data changes.

### 2. Event-Driven Architecture
- **Concept:** Decoupling services via events.
- **Key Knowledge:**
    - **Domain Events:** Publishing `UserRegistered` event instead of directly calling `EmailService.sendWelcome()`.
    - **Side Effects:** Handling non-critical actions asynchronously to keep the main request fast.

### 3. Hexagonal / Clean Architecture
- **Concept:** The "Core" depends on nothing.
- **Key Knowledge:**
    - **The Dependency Rule:** Dependencies point inwards. The DB depends on the Core, not the other way around.
    - **Use Cases:** Explicitly defining "What the user wants to do" as first-class citizens in the codebase.
