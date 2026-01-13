# Homelab & Development Infrastructure – Container Responsibility Map

## Document Context

This document defines **where containers are allowed to run** and **what class
of responsibility each container may have**.

It builds on:

- `00-overview.md`
- `01-architecture.md`
- `02-node-roles.md`
- `03-networking.md`
- `04-storage.md`

This file establishes **enforceable placement rules** for all containers.

## Container Design Principles

All containers in this environment follow these principles:

- Containers are long-running, not ad-hoc
- Each container has a single, well-defined purpose
- Containers do not cross responsibility boundaries
- Containers are replaceable; data is not

If a container cannot be clearly categorized, it should not exist.

## Container Execution Locations

### Lyra (Development Node)

**Allowed Container Types**

- Local development containers
- Test and sandbox environments
- Temporary build containers

**Characteristics**

- Short-lived
- Developer-initiated
- No persistent data

**Explicitly Disallowed**

- Infrastructure services
- Monitoring tools
- Databases with persistent state

All containers on Lyra are considered **ephemeral**.

### Proxima (Runtime Node)

Proxima is the **only node** where persistent containers may run.

Containers on Proxima run **inside LXC containers**.

## LXC-Level Responsibility Classes

Each LXC container on Proxima must belong to **one responsibility class**.

### Core Services LXC

**Purpose**

- Host foundational development services

**Container Examples**

- Local Git services
- CI-related services (local)
- Developer tooling services

**Constraints**

- No monitoring workloads
- No experimental services

### Monitoring & Observability LXC

**Purpose**

- Visibility into system and service health

**Container Examples**

- Container management UI
- Log aggregation
- Availability monitoring
- System health dashboards

**Constraints**

- Read-only or observational access
- No modification of core service state

### Database Services LXC

**Purpose**

- Host authoritative data stores for development and internal services
- Provide reliable, persistent database backends

**Container Examples**

- Relational databases (PostgreSQL, MySQL/MariaDB)
- Key-value or document stores (Redis, MongoDB)
- Local development databases shared by multiple services

**Constraints**

- No experimental or disposable data
- Controlled access only (no direct public exposure)
- Changes must be intentional and auditable
- Backups and persistence required

### Experimental / Sandbox LXC (Optional)

**Purpose**

- Isolated experimentation
- Learning or evaluation workloads

**Characteristics**

- Non-critical
- Easily disposable
- No authoritative data

This class is optional and must never host required services.

## Disallowed Patterns

The following are explicitly disallowed:

- Running Docker directly on the Proxmox host
- Mixing monitoring and core services in the same LXC
- Sharing persistent volumes across unrelated containers
- Running persistent services on Lyra or Nova

## Promotion Model (High-Level)

Container lifecycle follows a simple model:

1. Develop locally on Lyra
2. Validate behavior
3. Promote to Proxima as a persistent service
4. Retire when no longer needed

Implementation details are defined in runbooks.

## Summary

This responsibility map ensures:

- Clean separation of concerns
- Predictable container placement
- Easier scaling and recovery
- Reduced operational risk

When container boundaries are respected, the system remains maintainable.
