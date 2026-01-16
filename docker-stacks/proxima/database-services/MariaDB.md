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


mkdir -p /srv/docker/appdata/mariadb/data
mkdir -p /srv/docker/stacks/mariadb
sudo chown -R 1000:1000 /srv/docker/appdata/mariadb
chmod -R 750 /srv/docker/appdata/mariadb

sudo chown -R $USER:$USER /srv/docker/stacks/mariadb
chmod -R 755 /srv/docker/stacks/mariadb

cd /srv/docker/stacks/mariadb
```

#### 3 — Create docker-compose.yml

```

nano docker-compose.yml
```

```
services:
  mariadb:
    image: mariadb:latest
    container_name: mariadb
    restart: unless-stopped

    environment:
      MARIADB_ROOT_PASSWORD: "@Edith2705#"
      MARIADB_USER: proxima
      MARIADB_PASSWORD: "@Edith2705#"
      MARIADB_DATABASE: proximadatabase

    volumes:
      - /srv/docker/appdata/mariadb/data:/var/lib/mysql

    ports:
      - "3306:3306"

    networks:
      - core_net

networks:
  core_net:
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
