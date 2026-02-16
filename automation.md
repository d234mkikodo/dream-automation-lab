# Automation Layer

The Automation Layer orchestrates AI-driven workflows and manages task execution across services.

It is designed to separate execution logic from routing and infrastructure concerns.

---

## 1. n8n Integration

n8n serves as the workflow automation engine.

### Responsibilities

- Event-based workflow triggers
- API calls to OpenClaw services
- Credential and environment-based configuration
- Internal-only service communication (via Docker network)

### Design Goal

Keep business automation logic decoupled from the application layer.

n8n does not expose public endpoints directly.  
All access is routed through the reverse proxy.

---

## 2. MCP Integration

The MCP (Model Context Protocol) layer handles AI task orchestration.

### Responsibilities

- Structured AI task execution
- Multi-client context separation
- Controlled interaction between services
- Logical routing of AI workflows

### Design Goal

Enable scalable AI workflow coordination without tightly coupling to UI or external routing.

---

## 3. Debugging & Operational Challenges

During development, several architectural issues were identified and resolved:

### 1. Incorrect Endpoint Exposure

Internal service ports were unintentionally exposed before implementing strict reverse proxy routing.

Resolution:
- Removed direct port bindings
- Restricted service access to internal Docker network

---

### 2. Authentication Mismatch

Misalignment between service-level authentication and proxy routing caused access failures.

Resolution:
- Unified authentication flow at reverse proxy layer
- Verified header forwarding configuration

---

### 3. JSON vs HTML Response Conflict

API endpoints were incorrectly routed to UI paths, resulting in HTML responses instead of JSON.

Resolution:
- Separated API and UI routing rules in reverse proxy
- Verified content-type response handling
