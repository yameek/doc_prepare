[← Back to Index](./README.md)

# 4. Validation & Serialization

The gateway guards of your data. Validation ensures bad data doesn't get in, and serialization ensures sensitive data doesn't get out.

## Junior -> Mid: The Basics
**Goal:** Can validate simple forms and return clean JSON.

### 1. Input Validation
- **Concept:** Checking if the data sent by the user is correct.
- **Key Skills:**
    - **Required Fields:** Ensuring `email` and `password` are present.
    - **Type Checking:** Ensuring `age` is a number.
    - **Format Checking:** Ensuring `email` looks like an email.
    - **Returning Errors:** Sending a 400 Bad Request with a list of what's wrong.

### 2. Basic Serialization
- **Concept:** Converting your code objects into JSON.
- **Key Skills:**
    - **Automatic Conversion:** Relying on the framework to turn a Class/Dict into JSON.
    - **Renaming Fields:** Mapping `firstName` in code to `first_name` in JSON (snake_case vs camelCase).

---

## Mid -> Senior: Robustness & Security
**Goal:** Handles complex validation rules and strict output schemas.

### 1. Advanced Validation
- **Concept:** Rules that depend on context or other fields.
- **Key Knowledge:**
    - **Custom Validators:** Writing a function to check if a username is unique in the DB.
    - **Cross-Field Validation:** Ensuring `startDate` is before `endDate`.
    - **Sanitization:** Cleaning inputs (e.g., trimming whitespace, stripping HTML tags) before validation.

### 2. Output Filtering (DTOs / Views)
- **Concept:** Controlling exactly what the API returns.
- **Key Knowledge:**
    - **Allow-lists:** Explicitly defining which fields are public. NEVER return a raw DB model (risk of leaking password hashes).
    - **Serialization Groups:** Returning different fields for "Admin View" vs "Public View".
    - **Handling Dates:** Standardizing on ISO-8601 (UTC) for all date outputs.

---

## Senior -> Lead: Systems & Standards
**Goal:** Enforces data contracts and performance at scale.

### 1. Schema-First Design
- **Concept:** Defining the API contract before writing code.
- **Key Knowledge:**
    - **OpenAPI / Swagger:** Using tools to generate validation code *from* a spec file.
    - **Contract Testing:** Verifying that the implementation actually matches the documentation.

### 2. High-Performance Serialization
- **Concept:** JSON is slow.
- **Key Knowledge:**
    - **Alternative Formats:** Using Protocol Buffers (gRPC) or MessagePack for internal microservices to save bandwidth and CPU.
    - **Streaming Parsers:** Processing massive JSON payloads without loading the whole file into RAM.

### 3. Global Validation Strategies
- **Concept:** Validation as a cross-cutting concern.
- **Key Knowledge:**
    - **Domain Invariants:** Ensuring business rules (e.g., "Account balance cannot be negative") are enforced in the Domain Model, not just the Controller.
    - **Internationalization (i18n):** Returning validation error messages in the user's language.
