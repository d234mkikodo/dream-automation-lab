# AI Automation Infrastructure (Self-Hosted)

This project documents the design and deployment of a self-hosted AI automation system running on a secured VPS environment.

The goal is to build production-ready AI infrastructure without relying fully on managed cloud services.

---

## 🚀 Core Components

- OpenClaw (AI execution layer)
- n8n (Workflow automation engine)
- Docker-based container deployment
- Reverse proxy routing
- Secure API exposure
- VPS hardening & firewall configuration

---

## 🏗 Infrastructure Overview

- Linux-based VPS
- SSH hardening & brute-force protection
- Subnet & firewall rule configuration
- Environment isolation using .env files
- Containerized services with restart policies

---

## 🔐 Security Considerations

- Restricted port exposure
- Fail login protection
- Secure API routing
- Environment variable management
- Separation of public and internal services

---

## 📈 Engineering Focus

This project demonstrates:

- AI infrastructure deployment
- Docker networking
- Reverse proxy debugging
- API response troubleshooting (HTML vs JSON misrouting)
- MCP integration for workflow automation
