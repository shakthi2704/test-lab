# IP Address & Port Registry

This document is the **single authoritative reference** for:

- Static IP addresses
- Exposed service ports
- Node-to-service mapping

No configuration logic lives here — **reference only**.

---

## Network Overview

- **Subnet:** 192.168.8.0/24
- **Gateway:** 192.168.8.1
- **DNS:** Router / Local DNS
- **Environment:** Homelab (LAN only)

---

## Node IP Allocation

| Node Name | Role                     | IP Address   | OS         |
| --------- | ------------------------ | ------------ | ---------- |
| Proxima   | Proxmox host             | 192.168.8.20 | Proxmox VE |
| Lyra      | Main Dev Workstation     | 192.168.8.10 | Fedora     |
| Rhea      | Storage / Backup         | 192.168.8.50 | OMV        |
| Nova      | Operations & Access Node | 192.168.8.30 | Windows    |

---

## Proxima – LXC / VM IP Allocation

| Container / VM   | Type | Purpose                      | IP Address   |
| ---------------- | ---- | ---------------------------- | ------------ |
| core-services    | LXC  | Core infrastructure services | 192.168.8.21 |
| db-services      | LXC  | Databases                    | 192.168.8.22 |
| monitor-services | LXC  | Monitoring & observability   | 192.168.8.23 |

---

## Service Port Matrix

### Core Services (core-services LXC – 192.168.8.21)

| Service       | Purpose       | Port | Protocol | Access |
| ------------- | ------------- | ---- | -------- | ------ |
| Gitea         | Git hosting   | 3000 | TCP      | LAN    |
| Gitea SSH     | Git over SSH  | 2222 | TCP      | LAN    |
| Reverse Proxy | HTTP routing  | 80   | TCP      | LAN    |
| Reverse Proxy | HTTPS routing | 443  | TCP      | LAN    |

---

### Database Services (db-services LXC – 192.168.8.22)

| Service    | Purpose | Port | Protocol | Access        |
| ---------- | ------- | ---- | -------- | ------------- |
| PostgreSQL | App DB  | 5432 | TCP      | Internal only |
| MariaDB    | App DB  | 3306 | TCP      | Internal only |
| Redis      | Cache   | 6379 | TCP      | Internal only |

---

### Monitoring Services (monitor-services LXC – 192.168.8.23)

| Service    | Purpose    | Port | Protocol | Access   |
| ---------- | ---------- | ---- | -------- | -------- |
| Grafana    | Dashboards | 3000 | TCP      | LAN      |
| Prometheus | Metrics    | 9090 | TCP      | Internal |

---

## Lyra – Local Development Ports

| Service         | Purpose       | Port    | Scope          |
| --------------- | ------------- | ------- | -------------- |
| Docker Dev Apps | Local testing | Dynamic | Localhost only |

---

## Rhea – Storage & Backup

| Service    | Purpose            | Port     | Protocol |
| ---------- | ------------------ | -------- | -------- |
| OMV Web UI | Storage management | 80 / 443 | TCP      |
| NFS        | File sharing       | 2049     | TCP/UDP  |
| SMB        | File sharing       | 445      | TCP      |

---

## Rules

- No two services may share the same port on the same IP
- Databases must **not** be publicly exposed
- Changes here must be reflected in:
  - `home-lab-config`
  - service-specific README (if applicable)

---

## Change Control

All IP or port changes must be recorded in:

- `infra-docs/CHANGELOG.md`
