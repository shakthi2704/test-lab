# Homelab - Resource Model

## Purpose

This document defines CPU, memory, and role-based resource allocation across all homelab nodes.

The goal is to ensure:

- Predictable performance
- No RAM exhaustion
- Clear scaling boundaries
- Minimal operational risk

This model reflects **current implementation**, not future aspirations.

---

## Physical Hardware Overview

# Device Constraints

This document records **hardware, resource, and time constraints** for each
homelab device. These constraints are used to guide workload placement,
capacity planning, and architectural decisions.

## Device 1 – lyra Workstation

### System Information

| Category            | Specification                                |
| ------------------- | -------------------------------------------- |
| Device Name         | lyra                                         |
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

---

## Device 2 – proxima Compute & Runtime Host

### System Information

| Category            | Specification                                |
| ------------------- | -------------------------------------------- |
| Device Name         | proxima                                      |
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

---

## Device 3 – rhea Open Media Vault

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

---

## Device 4 – nova Operations & Access Node

### System Information

| Category            | Specification                                |
| ------------------- | -------------------------------------------- |
| Device Name         | nova                                         |
| System Type         | 64-bit operating system, x64-based processor |
| Processor           | Intel Core i3-7100U                          |
| CPU Cores / Threads | 2 / 4                                        |
| Architecture        | x64                                          |
| Role                | Operations & access node                     |

### Memory Constraints

| Attribute               | Value     |
| ----------------------- | --------- |
| Installed RAM           | 12 GB     |
| RAM Speed               | 2133 MT/s |
| Memory Upgrade Possible | Yes       |
| Max Supported RAM       | 16 GB     |

### Storage Constraints

| Disk # | Type | Capacity | Usage / Notes |
| ------ | ---- | -------- | ------------- |
| Disk 1 | HDD  | 500 GB   | OS / Data     |

---

## Change Management

Any change to allocations must be recorded in:

- `infra-docs/CHANGELOG.md`
- Relevant ADR in `infra-docs/decisions/`

This document is the **single source of truth** for resource planning.
