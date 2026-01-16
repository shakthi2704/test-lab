# portainer Agent– Core Service

## Purpose

Self-hosted Git service for homelab and projects.

---

| Item       | Value                  |
| ---------- | ---------------------- |
| Node       | Proxima                |
| Runtime    | Docker                 |
| Host       | LXC `database-servces` |
| service    | `portainer_edge_agent` |
| IP Address | `192.168.8.23`         |
| OS         | Ubuntu Server          |
| Exposure   | LAN only               |

### Deployment — Full Procedure

#### Phase 1 — Decide the Docker User (Important)

```
id dockeruser
```

```
docker run -d \
  --name portainer_agent \
  --restart=unless-stopped \
  -p 9001:9001 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /var/lib/docker/volumes:/var/lib/docker/volumes \
  portainer/agent:latest

```

#### Phase 2 — Start portainer

```
docker compose up -d
```
