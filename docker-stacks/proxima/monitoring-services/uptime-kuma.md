mkdir -p /srv/docker/appdata/uptime-kuma/{data,config,logs}
mkdir -p /srv/docker/stacks/uptime-kuma
sudo chown -R 1000:1000 /srv/docker/appdata/uptime-kuma
chmod -R 750 /srv/docker/appdata/uptime-kuma

sudo chown -R $USER:$USER /srv/docker/stacks/uptime-kuma
chmod -R 755 /srv/docker/stacks/uptime-kuma

cd /srv/docker/stacks/uptime-kuma
