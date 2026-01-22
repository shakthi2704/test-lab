# beszel-agent – Core Service

## Purpose

Self-hosted Git service for homelab and projects.

---

| Item       | Value               |
| ---------- | ------------------- |
| Node       | Proxima             |
| Runtime    | Docker              |
| Host       | LXC `core-services` |
| service    | `beszel-agent`      |
| IP Address | `192.168.8.21`      |
| OS         | Ubuntu Server       |
| Exposure   | LAN only            |

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

mkdir -p /srv/docker/appdata/beszel-agent/data
mkdir -p /srv/docker/stacks/beszel-agent

chown -R 1000:1000 /srv/docker/appdata/beszel-agent
chmod -R 750 /srv/docker/appdata/beszel-agent

chown -R $USER:$USER /srv/docker/stacks/beszel-agent
chmod -R 755 /srv/docker/stacks/beszel-agent
