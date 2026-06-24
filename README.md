# Custom LGL/LGTM Observability & Security Research Lab

A production-ready, containerized security operations and telemetry pipeline running on a Raspberry Pi 4. This infrastructure pairs a deliberately vulnerable target application with a centralized logging and metrics architecture to simulate real-world security monitoring and log analysis.

## 🏗️ Architecture Overview

The lab uses a multi-container Docker Compose design isolated within a private internal bridge network, fronted by an Nginx reverse proxy.

* **Target Application:** OWASP Juice Shop (Node.js/Express application).
* **Reverse Proxy:** Nginx (Handles traffic routing, TLS termination readiness, and access logging).
* **Log Shipper:** Grafana Promtail (Parses local system logs and container log streams).
* **Log Engine:** Grafana Loki (Centralized data store optimized for log aggregation).
* **Visualization:** Grafana Dashboard (Telemetry interface for log analysis and security monitoring).

## 🔒 Security & Optimization Features

* **Secrets Decoupling:** All administrative passwords, environment variables, and local IP strings are completely extracted into an un-tracked `.env` file, leaving the core repository entirely sanitized.
* **Network Isolation:** Containers bypass exposed host ports where possible, communicating entirely over a private, internal Docker bridge network (`lab_network`) using native container name resolution.
* **Log Rotation:** Strict Docker logging drivers restrict proxy log sizes to prevent storage exhaustion on resource-constrained single-board computers (Max size: 10MB, Max files: 3).

## 🚀 Quick Start / Deployment

### Prerequisites
* Docker and Docker Compose V2 installed.
* Git configured on your host system.

### 1. Clone and Navigate
```bash
git clone [https://github.com/gusthescripter/home_lab-stack_1.git](https://github.com/gusthescripter/home_lab-stack_1.git)
cd home_lab-stack_1
```
## Tear Down
* Use this command to clean up any dead Docker volumes hanging around.
* docker compose down -v
