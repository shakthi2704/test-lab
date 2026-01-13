# Homelab - Proxima

## Purpose

This document defines CPU, memory, and role-based resource allocation across all homelab nodes.This model reflects **current implementation**, not future aspirations.

---

## Device – proxima Compute & Runtime Host

### System Information

| Category            | Specification                                |
| ------------------- | -------------------------------------------- |
| Device Name         | proxima                                      |
| Device OS           | Debian GNU/Linux                             |
| System Type         | 64-bit operating system, x64-based processor |
| Processor           | Intel Core i5-10400                          |
| CPU Cores / Threads | 6 / 12                                       |
| Architecture        | x64                                          |
| Role                | Hypervisor (LXC only)                        |

### Memory Constraints

| Attribute               | Value     |
| ----------------------- | --------- |
| Installed RAM           | 8 GB      |
| RAM Speed               | 2400 MT/s |
| Memory Upgrade Possible | Yes       |
| Max Supported RAM       | 64 GB     |

### Storage Constraints

| Disk # | Type | Capacity | Usage / Notes |
| ------ | ---- | -------- | ------------- |
| Disk 1 | NVMe | 120 GB   | OS / Backup   |
| Disk 2 | HDD  | 1 TB     | Data / LXC    |

##### OS vesions

| name        | Vesrion | updated    |
| ----------- | ------- | ---------- |
| 13 (trixie) | 13.2    | 13/01/2026 |

##### Proxmox VE vesions

| name        | Vesrion             | updated    |
| ----------- | ------------------- | ---------- |
| 13 (trixie) | 8.0.6-1 (Synchrony) | 13/01/2026 |

---
