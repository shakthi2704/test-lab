# Gitea – Core Service

## Purpose

Self-hosted Git service for homelab and projects.

---

| Item       | Value           |
| ---------- | --------------- |
| Node       | Proxima         |
| Runtime    | Docker          |
| Host       | `core-services` |
| service    | `gitea`         |
| IP Address | `192.168.8.21`  |
| OS         | Ubuntu Server   |
| Exposure   | LAN only        |

### Deployment — Full Procedure

#### Phase 1 — Decide the Docker User (Important)

```
id dockeruser
```

#### 2 — Create Gitea Directories

```
mkdir -p /srv/docker/appdata/gitea/{data,config,logs}
mkdir -p /srv/docker/stacks/gitea
sudo chown -R 1000:1000 /srv/docker/appdata/gitea
chmod -R 750 /srv/docker/appdata/gitea

sudo chown -R $USER:$USER /srv/docker/stacks/gitea
chmod -R 755 /srv/docker/stacks/gitea

```

#### 3 — Create docker-compose.yml

```
cd /srv/docker/stacks/gitea
```

```
nano docker-compose.yml
```

```
services:
  gitea:
    image: 'gitea/gitea:latest'
    container_name: gitea
    restart: unless-stopped
    ports:
      - '3000:3000'
      - '222:22'
    environment:
      USER_UID: 1000
      USER_GID: 1000
      TZ: Asia/Colombo
    volumes:
      - '/srv/docker/appdata/gitea/data:/data'
      - '/srv/docker/appdata/gitea/config:/etc/gitea'
      - '/srv/docker/logs/gitea/logs:/var/log/gitea'
networks:
  proxima-net:
    external: true

```

#### Phase 4 — Start Gitea

```
docker compose up -d
```

```
docker ps
docker logs gitea --tail 50

```

#### Phase 5 — Web Installation (One-Time)

```
http://192.168.8.21:3000

```

#### Phase 6 — Validate File Placement

```
ls /srv/docker/appdata/gitea/config
ls /srv/docker/appdata/gitea/logs
ls /srv/docker/appdata/gitea/data

```

#### Phase 7 — Validate Git Operations

```
git clone ssh://192.168.8.21:222/<user>/<repo>.git

```

#### Phase 8 — Operational Checks

```
docker inspect gitea | grep RestartPolicy

```

| Item                   | Value                   |
| ---------------------- | ----------------------- |
| Administrator Username | Proxima                 |
| Email Address          | <proxima@proxmox.local> |
