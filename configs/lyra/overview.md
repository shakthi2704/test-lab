# Homelab - Lyra

## Purpose

This document defines CPU, memory, and role-based resource allocation across all homelab nodes.This model reflects **current implementation**, not future aspirations.

---

## Device – lyra Workstation

### System Information

| Category            | Specification                                |
| ------------------- | -------------------------------------------- |
| Device Name         | lyra                                         |
| Device OS           | Fedora Linux                                 |
| System Type         | 64-bit operating system, x64-based processor |
| Processor           | Intel Core i5-10400                          |
| CPU Cores / Threads | 6 / 12                                       |
| Architecture        | x64                                          |
| Role                | Development, control plane, tooling          |

### Memory Constraints

| Attribute               | Value     |
| ----------------------- | --------- |
| Installed RAM           | 20 GB     |
| RAM Speed               | 2400 MT/s |
| Memory Upgrade Possible | Yes       |
| Max Supported RAM       | 128 GB    |

### Storage Constraints

| Disk # | Type | Capacity | Usage / Notes |
| ------ | ---- | -------- | ------------- |
| Disk 1 | NVMe | 256 GB   | OS            |
| Disk 2 | NVMe | 240 GB   | Data          |

##### OS vesions

| name                                  | Vesrion | updated    |
| ------------------------------------- | ------- | ---------- |
| Fedora Linux 43 (Workstation Edition) | 43      | 13/01/2026 |

---
