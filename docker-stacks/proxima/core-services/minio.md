# minio – Core Service

## Purpose

Self-hosted Git service for homelab and projects.

---

| Item       | Value           |
| ---------- | --------------- |
| Node       | Proxima         |
| Runtime    | Docker          |
| Host       | `core-services` |
| service    | `minio`         |
| IP Address | `192.168.8.21`  |
| OS         | Ubuntu Server   |
| Exposure   | LAN only        |

### Deployment — Full Procedure

#### Phase 1 — Decide the Docker User (Important)

```
id dockeruser
```

#### 2 — Create minio Directories

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

    image: minio/minio:latest
    container_name: minio
    command: server /data --console-address :9002
    restart: unless-stopped
    user: "1000:1000"

    environment:
      MINIO_ROOT_USER: proxima
      MINIO_ROOT_PASSWORD: "@Edith2705#"
    volumes:
      - /srv/docker/appdata/minio/data:/data
    ports:
      - "9000:9000"
      - "9002:9002"

    networks:
      - core_net

networks:
  core_net:
    external: true
```

#### Phase 4 — Start minio

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


```
