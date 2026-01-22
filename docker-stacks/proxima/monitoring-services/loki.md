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



mkdir -p /srv/docker/stacks/loki-stack
sudo chown -R $USER:$USER /srv/docker/stacks/loki-stack
chmod -R 755 /srv/docker/stacks/loki-stack

cd /srv/docker/stacks/loki-stack
```

#### Phase 3 — Create docker-compose.yml

```

nano docker-compose.yml
```

```
services:
  dozzle:
    image: amir20/dozzle:latest
    container_name: dozzle
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
    ports:
      - "8080:8080"
    restart: unless-stopped
    networks:
      - core_net
networks:
  core_net:
    external: true



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

mkdir -p /srv/docker/appdata/grafana/data
mkdir -p /srv/docker/stacks/loki-stack

# Set permissions for the Grafana data folder

sudo chown -R 1000:1000 /srv/docker/appdata/grafana/
chmod -R 750 /srv/docker/appdata/grafana/

# Navigate into the stack configuration directory

cd /srv/docker/stacks/loki-stack

chmod -R 755 /srv/docker/stacks/loki-stack

services:
loki:
image: grafana/loki:2.9.4
container_name: loki
restart: unless-stopped
ports: - "3100:3100"
command: -config.file=/etc/loki/config.yml
volumes: - ./loki-config.yml:/etc/loki/config.yml:ro - ./data:/loki
networks: - core_net

grafana:
image: grafana/grafana:10.3.1
container_name: grafana
restart: unless-stopped
ports: - "3000:3000"
environment:
GF_SECURITY_ADMIN_USER: admin
GF_SECURITY_ADMIN_PASSWORD: admin
GF_AUTH_ANONYMOUS_ENABLED: "false"
volumes: - /srv/docker/appdata/grafana/data:/var/lib/grafana
depends_on: - loki
networks: - core_net

networks:
core_net:
