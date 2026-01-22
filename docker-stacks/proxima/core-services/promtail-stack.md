mkdir -p /srv/docker/appdata/promtail/{data,config,logs}
mkdir -p /srv/docker/stacks/promtail
sudo chown -R 1000:1000 /srv/docker/appdata/promtail-stack
chmod -R 750 /srv/docker/appdata/gitea

sudo chown -R $USER:$USER /srv/docker/stacks/promtail
chmod -R 755 /srv/docker/stacks/promtail

cd /srv/docker/stacks/promtail

# Persistent storage for Promtail

mkdir -p /srv/docker/appdata/promtail/{data,config,logs}

# YAML files (docker-compose + config)

mkdir -p /srv/docker/stacks/promtail

# Data folder for container use

sudo chown -R 1000:1000 /srv/docker/appdata/promtail
chmod -R 750 /srv/docker/appdata/promtail

# Stack/config files

sudo chown -R $USER:$USER /srv/docker/stacks/promtail
chmod -R 755 /srv/docker/stacks/promtail

cd /srv/docker/stacks/promtail
