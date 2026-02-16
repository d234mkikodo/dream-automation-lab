# Infrastructure Design

This document describes the infrastructure architecture and security model used to deploy the self-hosted AI automation platform.

---

## 1. VPS Configuration

The system runs on a Linux-based VPS hosted on Oracle Cloud Infrastructure (OCI).

### Configuration Highlights:

- Hardened SSH configuration
- Disabled insecure authentication methods
- Brute-force mitigation (fail2ban-style protection)
- Controlled system service management

### Design Goal

Ensure secure remote administration while minimizing attack surface.

---

## 2. Network Architecture

The infrastructure follows a segmented network model:

- VCN and subnet configuration (OCI)
- Firewall rule management at VPS level
- Controlled ingress and egress policies

### Design Goal

Isolate public access from internal services and enforce least privilege exposure.

---

## 3. Docker Deployment Model

All services run in isolated Docker containers.

### Implementation Details:

- Internal Docker networking (no direct public port bindings)
- Environment variable configuration via `.env`
- Restart policies for resilience
- Persistent volumes for stateful services

### Design Goal

Encapsulate services while maintaining internal communication security.

---

## 4. Reverse Proxy Layer

A reverse proxy is used as the only public-facing entry point.

### Responsibilities:

- TLS termination (HTTPS handling)
- Route separation (UI vs API endpoints)
- Internal container routing
- Prevention of direct container exposure

### Engineering Challenge Solved

Resolved JSON vs HTML misrouting caused by incorrect path handling in proxy configuration.

---

## 5. Network Exposure Policy

### Publicly Exposed Ports

- 80 (HTTP)
- 443 (HTTPS)

### Restricted Internal Ports

- 3000
- 5678
- 8080

These ports are accessible only within the Docker network and are not exposed via public IP.

### Access Flow

User → Domain → Reverse Proxy → Internal Docker Network → Services

### Security Principle Applied

- Least privilege port exposure
- Service isolation
- Layered access control

## Operational Considerations

- Logs monitored via Docker logs
- Service health verified post-deployment
- Environment variables separated per deployment context
