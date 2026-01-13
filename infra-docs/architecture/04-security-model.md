# # Homelab - Security Model

## Purpose

This document defines the baseline security posture of the homelab.
Security is implemented through isolation, least privilege, and simplicity.

---

## Trust Zones

| Zone     | Description              |
| -------- | ------------------------ |
| LAN      | Trusted internal network |
| Internal | VM/LXC east-west traffic |
| Host     | Proxmox and Rhea OS      |

No WAN exposure exists.

---

## Privilege Model

| Component         | Privilege       |
| ----------------- | --------------- |
| Proxmox Host      | Root            |
| Core Services LXC | Unprivileged    |
| DB LXC            | Unprivileged    |
| Monitor LXC       | Unprivileged    |
| sandbox LXC       | Unprivileged    |
| Lyra              | User-level only |
| Rhea              | Admin only      |
| nova              | User-level only |

---

## Container Security

- Docker runs only inside VM
- No Docker socket exposure
- No privileged containers
- Read-only volumes where possible

---

## Network Security

- Firewall enabled on Proxmox
- LXC firewall rules enforced
- DB ports blocked from LAN
- Monitoring ports internal-only

---

## Credential Handling

- No secrets in Git
- `.env` files excluded
- SSH keys only (no passwords)
- Gitea internal auth only

---

## Backup & Recovery

- Proxmox snapshots
- Offloaded backups to Rhea
- No backup services on Lyra

---

## Explicit Non-Goals

| Item            | Reason        |
| --------------- | ------------- |
| Zero Trust      | Overkill      |
| VPN mesh        | Not required  |
| Kubernetes RBAC | No Kubernetes |
| Cloud IAM       | Local-only    |

---

## Security Principle Summary

- Isolation > Hardening
- Documentation > Automation
- Predictability > Features
