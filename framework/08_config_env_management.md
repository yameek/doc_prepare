[← Back to Index](./README.md)

# 8. Configuration & Environment Management

Hardcoding secrets is a sin. Managing configuration correctly allows your code to run anywhere (local, staging, prod) without changes.

## Junior -> Mid: The Basics
**Goal:** Can run the app locally and change settings without editing code.

### 1. Environment Variables
- **Concept:** Variables set outside the app.
- **Key Skills:**
    - Reading `process.env.PORT` or `os.environ['DB_URL']`.
    - Using `.env` files (dotenv) for local development.
    - **Rule #1:** NEVER commit `.env` files to Git.

### 2. Basic Config Files
- **Concept:** Grouping settings.
- **Key Skills:**
    - Using `config.json` or `settings.py` to organize values.
    - Distinguishing between "Secrets" (API Keys) and "Config" (Page Size).

---

## Mid -> Senior: The 12-Factor App
**Goal:** strict separation of config from code.

### 1. Typed Configuration
- **Concept:** Fail fast if config is missing.
- **Key Knowledge:**
    - **Validation:** Checking that `DB_PORT` is actually a number at startup.
    - **Config Objects:** Using a singleton class `Config.db.url` instead of scattered `getenv()` calls.

### 2. Hierarchy & Overrides
- **Concept:** Defaults -> Config File -> Env Vars -> CLI Args.
- **Key Knowledge:**
    - **Layering:** How to have a base `default.json` and override it with `production.json`.
    - **Precedence:** Understanding which source wins when a value is defined in two places.

---

## Senior -> Lead: DevOps & Secrets
**Goal:** Manages configuration securely at scale across dynamic environments.

### 1. Secret Management Systems
- **Concept:** `.env` files don't scale to Kubernetes.
- **Key Knowledge:**
    - **Vault / AWS Secrets Manager:** Fetching secrets at runtime from a secure vault.
    - **Rotation:** Handling database password rotation without restarting the app.

### 2. Dynamic Configuration / Feature Flags
- **Concept:** Changing behavior without redeploying.
- **Key Knowledge:**
    - **Feature Toggles:** Enabling/disabling new features for a subset of users (Canary releases).
    - **Hot Reloading:** Watching for config changes and applying them instantly (e.g., changing log level from INFO to DEBUG).

### 3. Infrastructure as Code (IaC)
- **Concept:** Config is code too.
- **Key Knowledge:**
    - **Terraform / Helm:** Defining environment variables in deployment scripts.
    - **Immutable Infrastructure:** Why you shouldn't SSH into a server to change a config file.
