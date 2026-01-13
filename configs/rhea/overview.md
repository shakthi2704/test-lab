# Homelab - Rhea

## Purpose

This document defines CPU, memory, and role-based resource allocation across all homelab nodes.This model reflects **current implementation**, not future aspirations.

---

## Device – rhea Open Media Vault

### System Information

| Category            | Specification                                |
| ------------------- | -------------------------------------------- |
| Device Name         | rhea                                         |
| System Type         | 64-bit operating system, x64-based processor |
| Processor           | Intel Core i3-3220                           |
| CPU Cores / Threads | 2 / 4                                        |
| Architecture        | x64                                          |
| Role                | NAS, backups only, media server              |

### Memory Constraints

| Attribute               | Value     |
| ----------------------- | --------- |
| Installed RAM           | 4 GB      |
| RAM Speed               | 1600 MT/s |
| Memory Upgrade Possible | Yes       |
| Max Supported RAM       | 16 GB     |

### Storage Constraints

| Disk # | Type | Capacity | Usage / Notes |
| ------ | ---- | -------- | ------------- |
| Disk 1 | HDD  | 250 GB   | OS            |
| Disk 2 | HDD  | 1 TB     | Data          |
| Disk 3 | HDD  | 1 TB     | Data          |
| Disk 4 | HDD  | 1 TB     | Data          |

##### OS vesions

| name        | Vesrion | updated    |
| ----------- | ------- | ---------- |
| 13 (trixie) | 13.2    | 13/01/2026 |

---
