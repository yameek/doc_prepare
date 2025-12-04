[← Back to Index](./README.md)

# 1. Core OS & Networking

You can't automate what you don't understand. This is the bedrock of everything else.

## Junior -> Mid: The Basics
**Goal:** Can debug a server issue and understand basic connectivity.

### 1. Linux Internals
- **Concept:** How the OS runs your code.
- **Key Skills:**
    - **Systemd:** Managing services (`systemctl status/start/enable`).
    - **Cron:** Scheduling recurring tasks.
    - **Permissions:** Understanding `chmod`, `chown`, and users/groups.
    - **Filesystem:** Knowing `/etc` (config), `/var/log` (logs), `/proc` (kernel info).

### 2. CLI Fluency
- **Concept:** Living in the terminal.
- **Key Skills:**
    - **Text Processing:** `grep` (search), `tail -f` (watch logs).
    - **Process Management:** `ps aux`, `kill`, `htop` (CPU/RAM usage).
    - **Network Checks:** `ping`, `curl -v` (debug HTTP), `dig` (DNS lookup).

### 3. Networking Basics
- **Concept:** How computers talk.
- **Key Skills:**
    - **IP Addresses:** Public vs Private IPs, CIDR notation (`/24`).
    - **Ports:** Knowing standard ports (22 SSH, 80 HTTP, 443 HTTPS, 5432 Postgres).
    - **DNS:** How `google.com` becomes an IP address.

---

## Mid -> Senior: Performance & Security
**Goal:** Can tune the kernel and debug complex network latency/packet loss.

### 1. Advanced Linux
- **Concept:** Resource isolation and tuning.
- **Key Knowledge:**
    - **Namespaces & Cgroups:** The technology behind containers (Docker).
    - **Journald:** Advanced logging and querying.
    - **PAM:** Pluggable Authentication Modules (how login works).

### 2. Advanced Networking
- **Concept:** The layers below HTTP.
- **Key Knowledge:**
    - **TCP/IP Handshake:** SYN, SYN-ACK, ACK. Debugging connection timeouts.
    - **TLS Handshake:** How HTTPS works, certificates, and termination.
    - **VPNs:** Tunneling traffic securely between networks.

### 3. Debugging Tools
- **Concept:** Seeing the invisible.
- **Key Knowledge:**
    - **strace:** Tracing system calls (what files is this process opening?).
    - **tcpdump / Wireshark:** Capturing and analyzing network packets.
    - **lsof:** Listing open files and network sockets.

---

## Senior -> Lead: Kernel & Architecture
**Goal:** Designs networks and understands low-level system behavior.

### 1. Kernel Tuning
- **Concept:** Optimizing for high throughput.
- **Key Knowledge:**
    - **Sysctl:** Tuning TCP buffer sizes, file descriptor limits (`ulimit`).
    - **eBPF:** Safe, high-performance kernel tracing and networking (Cilium).

### 2. Network Architecture
- **Concept:** Designing for scale and failure.
- **Key Knowledge:**
    - **BGP:** How the internet routes traffic.
    - **Anycast:** Routing users to the nearest data center via the same IP.
    - **SDN (Software Defined Networking):** Programmable network configuration.
