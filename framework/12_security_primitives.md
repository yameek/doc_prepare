[← Back to Index](./README.md)

# 12. Security Primitives

Security isn't a feature; it's a requirement. Frameworks provide tools to protect against common attacks.

## Junior -> Mid: The Basics
**Goal:** Knows the OWASP Top 10 and uses framework defaults to stay safe.

### 1. Injection Attacks
- **Concept:** Untrusted data executing as code.
- **Key Skills:**
    - **SQL Injection:** ALWAYS use the ORM or Parameterized Queries. NEVER string concatenation.
    - **XSS (Cross-Site Scripting):** Relying on the template engine (React, Jinja2, Blade) to auto-escape HTML output.

### 2. Basic Headers
- **Concept:** Telling the browser how to behave.
- **Key Skills:**
    - **Helmet / Secure Headers:** Enabling default security headers (HSTS, X-Frame-Options, X-Content-Type-Options).
    - **CORS (Cross-Origin Resource Sharing):** Configuring who can call your API (e.g., only `my-frontend.com`).

---

## Mid -> Senior: Advanced Defense
**Goal:** Implements proactive security measures and handles complex attack vectors.

### 1. CSRF (Cross-Site Request Forgery)
- **Concept:** Tricking a user into clicking a link that performs an action.
- **Key Knowledge:**
    - **CSRF Tokens:** How to generate and validate tokens for state-changing requests (POST/PUT).
    - **SameSite Cookies:** Using `SameSite=Strict` or `Lax` to prevent the browser from sending cookies on cross-site requests.

### 2. Rate Limiting
- **Concept:** Preventing abuse.
- **Key Knowledge:**
    - **Throttling:** Limiting users to 100 requests/minute.
    - **Strategies:** Fixed Window vs Sliding Window vs Token Bucket.
    - **Storage:** Using Redis to track counters across multiple servers.

### 3. Sensitive Data Handling
- **Concept:** Protecting PII.
- **Key Knowledge:**
    - **Encryption at Rest:** Encrypting credit card numbers or SSNs in the database.
    - **Redaction:** Ensuring logs don't contain passwords or tokens.

---

## Senior -> Lead: Security Architecture
**Goal:** Designs secure systems and manages compliance.

### 1. Content Security Policy (CSP)
- **Concept:** The ultimate XSS defense.
- **Key Knowledge:**
    - **Allow-lists:** Telling the browser exactly which domains scripts/images can load from.
    - **Reporting:** Configuring CSP to report violations to a monitoring endpoint.

### 2. Supply Chain Security
- **Concept:** Your dependencies are a risk.
- **Key Knowledge:**
    - **SCA (Software Composition Analysis):** Automatically scanning `package.json` or `pom.xml` for known vulnerabilities (CVEs).
    - **Dependency Locking:** Using lockfiles to ensure reproducible builds.

### 3. Threat Modeling
- **Concept:** Thinking like an attacker.
- **Key Knowledge:**
    - **STRIDE:** Analyzing the system for Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, and Elevation of Privilege.
    - **Zero Trust:** Assuming the internal network is hostile.
