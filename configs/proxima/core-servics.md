# Proxima – LXC Inventory: Core Services

This document records the **Core Services LXC** running on **Proxima**.
It is a **high-level inventory**, not an installation guide.

---

## LXC Summary

| Field              | Value                        |
| ------------------ | ---------------------------- |
| **Container Name** | core-services                |
| **Node**           | Proxima                      |
| **Purpose**        | Core infrastructure services |
| **OS**             | Ubuntu Server                |
| **OS Version**     | 24.04 LTS                    |
| **Last OS Update** | 14 Jan 2026                  |
| **Container Type** | Unprivileged LXC             |
| **Nesting**        | Enabled                      |
| **Docker**         | Yes                          |

---

## Resource Allocation

| Resource  | Allocation |
| --------- | ---------- |
| CPU Cores | 2          |
| RAM       | 2 GB       |
| Swap      | 1 GB       |
| Storage   | 100 GB     |

---

## Network

| Item       | Value          |
| ---------- | -------------- |
| IP Address | 192.168.8.21   |
| Bridge     | vmbr0          |
| Subnet     | 192.168.8.0/24 |
| Gateway    | 192.168.8.1    |
| DNS        | LAN / Router   |

---

## Active Services

| Service       | Purpose       | Status  |
| ------------- | ------------- | ------- |
| Gitea         | Git hosting   | Running |
| Reverse Proxy | HTTP routing  | Planned |
| CI/CD         | Gitea Actions | Planned |

---

## Exposed Ports

| Service      | Port | Protocol | Access |
| ------------ | ---- | -------- | ------ |
| Gitea Web UI | 3000 | TCP      | LAN    |
| Gitea SSH    | 2222 | TCP      | LAN    |

---

## Docker Layout

```text
/srv/docker/
├── appdata/
│   ├── gitea/
│   │   └── data/
│   ├── postgres/
│   │   └── data/
│   ├── redis/
│   │   └── data/
│   └── nginx/
│       ├── conf/
│       └── certs/
│
├── stacks/
│   ├── gitea/
│   │   └── docker-compose.yml
│   ├── postgres/
│   │   └── docker-compose.yml
│   └── nginx/
│       └── docker-compose.yml
│
└── backups/


```
