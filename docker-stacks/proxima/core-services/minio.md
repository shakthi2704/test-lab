# minio – Core Service

## Purpose

Self-hosted Git service for homelab and projects.

---

| Item       | Value               |
| ---------- | ------------------- |
| Node       | Proxima             |
| Runtime    | Docker              |
| Host       | LXC `core-services` |
| service    | `minio`             |
| IP Address | `192.168.8.21`      |
| OS         | Ubuntu Server       |
| Exposure   | LAN only            |

### Deployment — Full Procedure

#### Phase 1 — Decide the Docker User (Important)

```
id dockeruser
```

#### 2 — Create Gitea Directories

```
mkdir -p /srv/docker/appdata/minio/{data,config,logs}
mkdir -p /srv/docker/stacks/minio
sudo chown -R 1000:1000 /srv/docker/appdata/minio
chmod -R 750 /srv/docker/appdata/minio

sudo chown -R $USER:$USER /srv/docker/stacks/minio
chmod -R 755 /srv/docker/stacks/minio


```

#### 3 — Create docker-compose.yml

```
cd /srv/docker/stacks/minio
```

```
nano docker-compose.yml
```

```
services:
  minio:

    image: minio/minio:RELEASE.2024-05-10T01-41-38Z
    container_name: minio
    command: server /data --console-address :9001
    restart: unless-stopped
    user: "1000:1000"

    environment:
      MINIO_ROOT_USER: proxima
      MINIO_ROOT_PASSWORD:"@Edith2705#"
    volumes:
      - /srv/docker/appdata/minio/data:/data
      - /srv/docker/appdata/minio/config:/root/.minio

    ports:
      - "9000:9000"
      - "9001:9001"

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
docker compose up -d
```

```
docker ps
```

````
docker logs minio --tail 50
```
````

#### Phase 5 — Validate File Placement

```
ls /srv/docker/appdata/minio/config
ls /srv/docker/appdata/minio/logs
ls /srv/docker/appdata/minio/data

```

```

| Item                   | Value                   |
| ---------------------- | ----------------------- |
| Administrator Username | Proxima                 |
| password          | <password> |
```
