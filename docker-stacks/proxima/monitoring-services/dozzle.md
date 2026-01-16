# Gitea – Core Service

## Purpose

Self-hosted Git service for homelab and projects.

---

| Item       | Value                     |
| ---------- | ------------------------- |
| Node       | Proxima                   |
| Runtime    | Docker                    |
| Host       | LXC `monitoring-services` |
| service    | `dozzle`                  |
| IP Address | `192.168.8.22`            |
| OS         | Ubuntu Server             |
| Exposure   | LAN only                  |

### Deployment — Full Procedure

#### Phase 1 — Decide the Docker User (Important)

```
id dockeruser
```

#### Phase 2 — Create portainer Directories

```

mkdir -p /srv/docker/stacks/dozzle
sudo chown -R $USER:$USER /srv/docker/stacks/dozzle
chmod -R 755 /srv/docker/stacks/dozzle

cd /srv/docker/stacks/dozzle

```

#### Phase 3 — Create docker-compose.yml

```

c
```

```
services:
  portainer:
    container_name: portainer
    # Using 'lts' tag is good practice for stability
    image: portainer/portainer-ce:lts
    restart: always
    volumes:
      - /srv/docker/appdata/portainer/data:/data
      - /var/run/docker.sock:/var/run/docker.sock
    ports:
      - 9443:9443
      - 8000:8000
networks:
  default:
    name: portainer_network


```

#### Phase 4 — Start portainer

```
docker compose up -d
```

```
docker ps
docker logs portainer --tail 50

```

#### Phase 5 — Web Installation (One-Time)

```
http://<LXC-IP>:3000

```

#### Phase 6 — Validate File Placement

```
ls /srv/docker/appdata/portainer/data
ls /srv/docker/appdata/portainer/config


```

#### Phase 7 — Validate Git Operations

```
git clone ssh://git@<LXC-IP>:222/<user>/<repo>.git

```

#### Phase 8 — Operational Checks

```
docker inspect portainer | grep RestartPolicy

```

| Item                   | Value   |
| ---------------------- | ------- |
| Administrator Username | Proxima |
