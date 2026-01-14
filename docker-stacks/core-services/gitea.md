# Gitea – Core Service

## Purpose

Self-hosted Git service for homelab and projects.

---

| Item       | Value               |
| ---------- | ------------------- |
| Node       | Proxima             |
| Runtime    | Docker              |
| Host       | LXC `core-services` |
| IP Address | `192.168.8.21`      |
| OS         | Ubuntu Server       |
| Exposure   | LAN only            |

### Deployment — Full Procedure

#### Phase 1 — Decide the Docker User (Important)

```
id dockeruser
```

Phase 2 — Create Gitea Directories

```
mkdir -p /srv/docker/appdata/gitea/{data,config,logs}
chown -R dockeruser:dockeruser /srv/docker/appdata/gitea
chmod -R 750 /srv/docker/appdata/gitea

```

```
/srv/docker/appdata/gitea/
├── data
├── config
└── logs

```

Phase 3 — Create docker-compose.yml

```
cd /srv/docker/appdata/gitea
nano docker-compose.yml
```

```
version: "3.9"

services:
  gitea:
    image: gitea/gitea:latest
    container_name: gitea
    restart: unless-stopped

    ports:
      - "3000:3000"
      - "222:22"

    environment:
      USER_UID: 1000
      USER_GID: 1000

      GITEA_CUSTOM: /data/custom
      GITEA_APP_INI: /data/custom/conf/app.ini
      GITEA_LOG_ROOT_PATH: /data/log

    volumes:
      - /srv/docker/appdata/gitea/data:/data
      - /srv/docker/appdata/gitea/config:/data/custom/conf
      - /srv/docker/appdata/gitea/logs:/data/log

```

Phase 4 — Start Gitea

```
docker compose up -d
```

```
docker ps
docker logs gitea --tail 50

```

Phase 5 — Web Installation (One-Time)

```
http://<LXC-IP>:3000

```

Phase 6 — Validate File Placement

```
ls /srv/docker/appdata/gitea/config
ls /srv/docker/appdata/gitea/logs
ls /srv/docker/appdata/gitea/data

```

Phase 7 — Validate Git Operations

```
git clone ssh://git@<LXC-IP>:222/<user>/<repo>.git

```

Phase 8 — Operational Checks

```
docker inspect gitea | grep RestartPolicy

```
