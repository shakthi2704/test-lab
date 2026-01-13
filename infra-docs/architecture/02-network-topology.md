# Homelab - Network Topology

## Purpose

This document describes the logical and physical network topology of the homelab.
It defines IP addressing, node connectivity, service exposure, and traffic boundaries.

This topology prioritizes:

- Simplicity over complexity
- Clear service boundaries
- Minimal attack surface
- Easy troubleshooting

---

## Physical Network

| Component        | Description                                          |
| ---------------- | ---------------------------------------------------- |
| Router / Gateway | Home router providing DHCP, NAT, and internet access |
| Switch           | Layer 2 unmanaged switch                             |
| Proxima          | Proxmox hypervisor (hosts LXCs)                      |
| Lyra             | Main development workstation                         |
| Rhea             | NAS / Media server (OMV)                             |
| Nova             | Operations & Access Node                             |

---

## Logical Network Layout

All nodes reside on a single trusted LAN.

| Network | CIDR             | Purpose                 |
| ------- | ---------------- | ----------------------- |
| LAN     | `192.168.8.0/24` | Primary homelab network |

Gateway: `192.168.8.1`

DNS: Provided by router :

- Primary DNS: `192.168.8.1`
- Secondary DNS: `1.1.1.1`

---

## Node IP Allocation

| Node                 | IP Address     | Notes     |
| -------------------- | -------------- | --------- |
| Proxima              | `192.168.8.20` | DHCP      |
| Lyra                 | `192.168.8.10` | DHCP      |
| Rhea                 | `192.168.8.50` | DHPC      |
| Nova                 | `192.168.8.30` | DHCP      |
| Core Services LXC    | `192.168.8.21` | Static IP |
| Monitor Services LXC | `192.168.8.22` | Static IP |
| Monitor Services LXC | `192.168.8.23` | Static IP |
| sandbox Services LXC | `192.168.8.24` | Static IP |

---

## Proxima Internal Networking

Proxima uses Linux bridges for VM and LXC networking.

| Bridge | Type    | Purpose             |
| ------ | ------- | ------------------- |
| vmbr0  | Bridged | External LAN access |

All VMs and LXCs attach to `vmbr0`.

---

## Service Exposure Model

### Externally Accessible (LAN)

These services are reachable from trusted LAN only.

| Service      | Host             | Port |
| ------------ | ---------------- | ---- |
| Gitea Web UI | Core Services VM | 3000 |

No services are exposed directly to the internet.

---

## Internal-Only Services

These services are **not exposed** outside the Proxima host.

| Service    | Location        | Access        |
| ---------- | --------------- | ------------- |
| PostgreSQL | DB Services LXC | Internal only |
| MariaDB    | DB Services LXC | Internal only |
| Redis      | DB Services LXC | Internal only |

Access is restricted to:

- Core Services LXC
- Monitor Services LXC (if needed)

---

## Traffic Flow Summary

- Lyra → Gitea (HTTP/SSH)
- Core Services LXC → DB Services LXC (internal DB traffic)
- Monitor Services LXC → All nodes (metrics only)
- Rhea ← Proxima (backup traffic)

No direct traffic:

- Internet → Internal services
- Lyra → Databases
- DB Services → Internet

---

## Security Boundaries

- Single trusted LAN
- No port forwarding on router
- Databases isolated in LXC
- Monitoring is read-only
- Proxmox UI accessible only from LAN

---

## Future Considerations (Not Implemented)

- Reverse proxy (Traefik / Nginx)
- Dedicated management VLAN
- WireGuard VPN for remote access
- Firewall rules per service

---
