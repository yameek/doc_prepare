[← Back to Index](./README.md)

# 8. Git, Scripting & Automation Glue

The "Glue" that holds the platform together.

## Junior -> Mid: The Basics
**Goal:** Can write a script to automate a manual task.

### 1. Bash Scripting
- **Concept:** The universal language.
- **Key Skills:**
    - **Safety:** `set -euo pipefail` (Stop on error, stop on undefined var).
    - **Pipes:** `curl | jq | grep`.
    - **Loops:** `for i in server1 server2; do ... done`.

### 2. Git
- **Concept:** Version control.
- **Key Skills:**
    - **Basic Commands:** `add`, `commit`, `push`, `pull`.
    - **Merge Conflicts:** Resolving them without panic.

### 3. Tools
- **Concept:** JSON/YAML wrangling.
- **Key Skills:**
    - **jq:** Parsing JSON in the terminal.
    - **yq:** Parsing YAML.
    - **Make:** Creating a `Makefile` to standardize commands (`make deploy`).

---

## Mid -> Senior: Advanced Automation
**Goal:** Writes robust tooling for the team.

### 1. Python / Go
- **Concept:** When Bash is too messy.
- **Key Knowledge:**
    - **Python:** Great for AWS Boto3 scripts.
    - **Go:** Great for binaries (CLIs) and Kubernetes controllers.

### 2. Advanced Git
- **Concept:** Managing complex repos.
- **Key Knowledge:**
    - **Submodules / Subtrees:** Including other repos.
    - **Worktrees:** Working on two branches at once.
    - **Pre-commit Hooks:** Running linters before commit.

### 3. Templating
- **Concept:** Generating config.
- **Key Knowledge:**
    - **envsubst:** Replacing `$VAR` in a file.
    - **Go Templates:** The engine behind Helm and Hugo.

---

## Senior -> Lead: Platform Tooling
**Goal:** Builds the "Internal Developer Platform" (IDP).

### 1. Kubernetes Scripting
- **Concept:** Automating the cluster.
- **Key Knowledge:**
    - **JSONPath:** Extracting specific fields from `kubectl get -o json`.
    - **Custom Columns:** Formatting `kubectl` output.
    - **Client-go:** Writing a real Kubernetes controller in Go.

### 2. CLI Design
- **Concept:** UX for developers.
- **Key Knowledge:**
    - **Cobra (Go):** Building standard CLIs with flags and subcommands.
    - **Idempotency:** Ensuring the script can run 10 times without breaking things.

### 3. ChatOps
- **Concept:** Operations in Slack.
- **Key Knowledge:**
    - **Bots:** Writing a bot to trigger a deployment or check status.
    - **Approval Flows:** Interactive buttons in Slack to approve a release.
