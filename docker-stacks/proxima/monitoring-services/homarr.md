mkdir -p /srv/docker/appdata/homarr/{data,configs,logs,icons}
mkdir -p /srv/docker/appdata/homarr/imgs/backgrounds
mkdir -p /srv/docker/stacks/homarr

sudo chown -R 1000:1000 /srv/docker/appdata/homarr
chmod -R 750 /srv/docker/appdata/homarr
sudo chown -R $USER:$USER /srv/docker/stacks/homarr

chmod -R 755 /srv/docker/stacks/homarr
