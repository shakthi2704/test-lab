mkdir -p /srv/docker/appdata/beszel/{data,config,logs}
mkdir -p /srv/docker/stacks/beszel
sudo chown -R 1000:1000 /srv/docker/appdata/beszel
chmod -R 750 /srv/docker/appdata/beszel

sudo chown -R $USER:$USER /srv/docker/stacks/beszel
chmod -R 755 /srv/docker/stacks/beszel

cd /srv/docker/stacks/beszel

agent

mkdir -p /srv/docker/appdata/beszel-agent/data
mkdir -p /srv/docker/stacks/beszel-agent

chown -R 1000:1000 /srv/docker/appdata/beszel-agent
chmod -R 750 /srv/docker/appdata/beszel-agent

chown -R $USER:$USER /srv/docker/stacks/beszel-agent
chmod -R 755 /srv/docker/stacks/beszel-agent
