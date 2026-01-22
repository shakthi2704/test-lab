mkdir -p /srv/docker/appdata/pulse/{data,config,logs}
mkdir -p /srv/docker/stacks/pulse
sudo chown -R 1000:1000 /srv/docker/appdata/pulse
chmod -R 750 /srv/docker/appdata/pulse

sudo chown -R $USER:$USER /srv/docker/stacks/pulse
chmod -R 755 /srv/docker/stacks/pulse

cd /srv/docker/stacks/pulse
