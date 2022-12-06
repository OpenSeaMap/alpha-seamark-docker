# Overview

This is the image we're using for our tile server at http://t1.openseamap.org.
It is based on [phusion/baseimage-docker](https://github.com/phusion/baseimage-docker).
The Dockerfile is based on [raumzeitlabor/mediawiki-docker](https://github.com/raumzeitlabor/mediawiki-docker).

The image serves tiles from the `/data` volume. In case a file is not found
`/data/empty.png` is returned.

## build image
docker-compose build 

## push image to github package registry

### login to github
```
CR_PAT=<TOKEN>
USERNAME=<USERNAME>
echo $CR_PAT | docker login ghcr.io -u $USERNAME --password-stdin
```

### tag image ###
```
docker tag seamark ghcr.io/openseamap/seamark:latest
```

### push image to github
```
docker push ghcr.io/openseamap/seamark:latest
```

## Setup

To set up this container, simply copy the startup script and docker compose file to host.
```
sudo cp tiles.service /etc/systemd/system/multi-user.target.wants/web@seamark.service
sudo cp docker-compose.yml /etc/docker/compose/seamark/docker-compose.yml
```

run `sudo systemctl daemon-reload`, followed by `sudo systemctl start web@seamark.service`.

The service file mounts `/var/data/tiles` as `/data` inside the container.
