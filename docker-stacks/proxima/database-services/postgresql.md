# Gitea – Core Service

## Purpose

Self-hosted Git service for homelab and projects.

---

| Item       | Value                   |
| ---------- | ----------------------- |
| Node       | Proxima                 |
| Runtime    | Docker                  |
| Host       | LXC `database-services` |
| service    | `postgresql`            |
| IP Address | `192.168.8.21`          |
| OS         | Ubuntu Server           |
| Exposure   | LAN only                |

### Deployment — Full Procedure

#### Phase 1 — Decide the Docker User (Important)

```
id dockeruser
```

#### 2 — Create Gitea Directories

```

mkdir -p /srv/docker/appdata/postgresql/data
mkdir -p /srv/docker/stacks/postgresql
sudo chown -R 1000:1000 /srv/docker/appdata/postgresql
chmod -R 750 /srv/docker/appdata/postgresql
sudo chown -R 70:70 /srv/docker/appdata/postgresql/data

sudo chown -R $USER:$USER /srv/docker/stacks/postgresql
chmod -R 755 /srv/docker/stacks/postgresql


cd /srv/docker/stacks/postgresql

```

#### 3 — Create docker-compose.yml

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
http://<LXC-IP>:3000

```

Phase 6 — Validate File Placement

```
ls /srv/docker/appdata/gitea/config
ls /srv/docker/appdata/gitea/logs
ls /srv/docker/appdata/gitea/data

```

#### Phase 7 — Validate Git Operations

```
git clone ssh://git@<LXC-IP>:222/<user>/<repo>.git

```

#### Phase 8 — Operational Checks

```
docker inspect gitea | grep RestartPolicy

```

| Item                   | Value                   |
| ---------------------- | ----------------------- |
| Administrator Username | Proxima                 |
| Email Address          | <proxima@proxmox.local> |
