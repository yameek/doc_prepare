# 5. Authentication & Authorization

Security is paramount. You must know who the user is (Authentication) and what they are allowed to do (Authorization).

## Junior -> Mid: The Basics
**Goal:** Can implement a simple login system and protect routes.

### 1. Authentication (AuthN)
- **Concept:** "Who are you?"
- **Key Skills:**
    - **Session-based Auth:** Using cookies and server-side sessions.
    - **Token-based Auth:** Sending a token in the `Authorization` header.
    - **Password Handling:** NEVER storing plain text. Using hashing (bcrypt/argon2).

### 2. Basic Authorization (AuthZ)
- **Concept:** "Can you do this?"
- **Key Skills:**
    - **Protecting Routes:** Marking a controller as `@RequiresAuth`.
    - **Simple Roles:** Checking `if (user.role == 'admin')`.

---

## Mid -> Senior: Modern Standards
**Goal:** Implements stateless, scalable auth and fine-grained permissions.

### 1. JWT (JSON Web Tokens)
- **Concept:** Stateless authentication.
- **Key Knowledge:**
    - **Structure:** Header, Payload, Signature.
    - **Security:** Signing vs Encryption. Why you shouldn't put sensitive data in a JWT.
    - **Expiration:** Handling `exp` claims.

### 2. OAuth2 & OIDC
- **Concept:** "Log in with Google/Facebook".
- **Key Knowledge:**
    - **Flows:** Authorization Code Flow (for server-side apps) vs PKCE (for mobile/SPA).
    - **Scopes:** Requesting limited access (e.g., "read-only").
    - **Social Login:** Integrating third-party providers.

### 3. RBAC (Role-Based Access Control)
- **Concept:** Assigning permissions to roles, not users.
- **Key Knowledge:**
    - **Role Hierarchy:** Admin > Editor > Viewer.
    - **Middleware Checks:** `@HasRole('Editor')`.

---

## Senior -> Lead: Enterprise Security
**Goal:** Designs complex permission systems and federated identity solutions.

### 1. ABAC (Attribute-Based Access Control) & Policy Engines
- **Concept:** "Can User X do Action Y on Resource Z?"
- **Key Knowledge:**
    - **Dynamic Policies:** "User can edit this document IF they are the owner OR it is in 'Draft' status."
    - **Policy-as-Code:** Using tools like OPA (Open Policy Agent) to decouple logic from code.

### 2. Token Management Strategies
- **Concept:** Balancing security and UX.
- **Key Knowledge:**
    - **Refresh Tokens:** Rotating short-lived access tokens for long-lived sessions.
    - **Token Revocation:** How to ban a user instantly if tokens are stateless (blocklists).
    - **BFF Pattern (Backend for Frontend):** Storing tokens in HttpOnly cookies to prevent XSS attacks in SPAs.

### 3. SSO & Federation
- **Concept:** One login for the whole company.
- **Key Knowledge:**
    - **SAML:** The enterprise standard for SSO.
    - **Identity Providers (IdP):** Integrating with Okta, Auth0, or Keycloak.
    - **Multi-Tenancy:** Isolating users across different organizations within the same app.
