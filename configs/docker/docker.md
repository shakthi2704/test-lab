# Homelab - Docker setup

Below is a cleaned, corrected, and properly ordered Docker installation and setup procedure for Ubuntu/Debian-based systems, with errors fixed, inconsistencies removed, and best practices applied. I also explain what was wrong and why it is fixed, but concisely.

### 1.Reconfigure Timezone (Optional but Recommended -proxmox)

```

sudo dpkg-reconfigure tzdata

```

### 2. System Update & Base Packages

```
sudo apt update
sudo apt upgrade -y
sudo apt install -y \
  ca-certificates \
  curl \
  gnupg \
  lsb-release \
  sudo

```

### 3. (Optional) Create a Dedicated Non-Root User for Docker

```
sudo adduser `username`
sudo usermod -aG sudo `username`

```

```
su - `username`


```

### 4. Add Docker Official Repository (Correct Method)

```
sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg \
  | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" \
  | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update

```

### 5. Install Docker Engine & Tools

```
sudo apt install -y \
  docker-ce \
  docker-ce-cli \
  containerd.io \
  docker-buildx-plugin \
  docker-compose-plugin

```

### 6. Create Docker Group & Add User

```
sudo groupadd docker 2>/dev/null || true
sudo usermod -aG docker `username`
```

```
newgrp docker
```

```
id
```

### 7. Enable and Start Docker

```
sudo systemctl enable docker
sudo systemctl start docker
sudo systemctl status docker
```

```
docker ps
```

### 8. Docker Directory Layout (Before daemon.json)

```
sudo systemctl stop docker
```

```
sudo mkdir -p /srv/docker/{appdata,volumes,networks,logs}
sudo chown -R $USER:$USER /srv/docker
sudo chmod -R 755 /srv/docker
```

### 9. Docker Daemon Configuration

```
sudo nano /etc/docker/daemon.json
```

{
"log-driver": "json-file",
"log-opts": {
"max-size": "50m",
"max-file": "5"
},
"data-root": "/srv/docker/volumes",
"storage-driver": "overlay2"
}

```

```

sudo systemctl start docker

```

```

docker info | grep "Docker Root Dir"

```

### 10. Verify Docker Installation (Sanity Check)

```

docker --version
docker compose version
systemctl status docker

```

```
