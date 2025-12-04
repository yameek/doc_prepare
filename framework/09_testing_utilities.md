[← Back to Index](./README.md)

# 9. Testing Utilities

If it's not tested, it's broken. Frameworks provide tools to make testing easy and fast.

## Junior -> Mid: The Basics
**Goal:** Can write a simple unit test and run the test suite.

### 1. Unit Testing
- **Concept:** Testing one function in isolation.
- **Key Skills:**
    - Using the test runner (Jest, Pytest, JUnit).
    - Assertions: `expect(result).toBe(5)`.
    - Mocking: Faking a helper function.

### 2. The Test Client
- **Concept:** Testing API endpoints without a browser.
- **Key Skills:**
    - Sending a fake GET request to your controller.
    - Asserting the status code is 200.
    - Asserting the JSON body contains the right data.

---

## Mid -> Senior: Integration & State
**Goal:** Writes reliable integration tests that involve the database.

### 1. Fixtures & Factories
- **Concept:** Setting up the data before the test.
- **Key Knowledge:**
    - **Factories:** "Create a User with random email" (e.g., FactoryBot).
    - **Seeding:** Populating the DB with a known state.
    - **Cleanup:** Ensuring the DB is clean for the next test.

### 2. Transactional Tests
- **Concept:** Fast DB tests.
- **Key Knowledge:**
    - **Rollback Strategy:** Starting a transaction at the beginning of the test and rolling it back at the end. This keeps the DB clean without slow truncate/delete operations.

### 3. Test Coverage
- **Concept:** Knowing what you missed.
- **Key Knowledge:**
    - **Coverage Reports:** Identifying lines of code that are never executed.
    - **Branch Coverage:** Testing both the `if` and the `else`.

---

## Senior -> Lead: Strategy & Culture
**Goal:** Maintains a healthy test suite that enables rapid deployment.

### 1. Testing Pyramid
- **Concept:** Balance.
- **Key Knowledge:**
    - **Unit vs Integration vs E2E:** Knowing that you should have many fast unit tests, fewer integration tests, and very few slow E2E tests.
    - **Shift Left:** Testing early in the pipeline.

### 2. Performance & Load Testing
- **Concept:** Will it crash on Black Friday?
- **Key Knowledge:**
    - **k6 / JMeter:** Simulating thousands of concurrent users.
    - **Profiling:** Identifying bottlenecks under load.

### 3. Testability Design
- **Concept:** Writing code *to be* tested.
- **Key Knowledge:**
    - **Dependency Injection:** The key to testable architecture.
    - **Contract Testing (Pact):** Ensuring microservices don't break each other's expectations.
    - **Flaky Tests:** Identifying and fixing tests that fail randomly (the enemy of CI).
