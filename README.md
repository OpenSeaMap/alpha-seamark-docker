# Overview

This is the image we're using for our tile server at http://t1.openseamap.org.
It is based on [phusion/baseimage-docker](https://github.com/phusion/baseimage-docker).
The Dockerfile is based on [raumzeitlabor/mediawiki-docker](https://github.com/raumzeitlabor/mediawiki-docker).

The image serves tiles from the `/data` volume. In case a file is not found
`/data/empty.png` is returned.

## Setup

To set up this container, simply copy the `tiles.service` file to 
`/etc/systemd/system/multi-user.target.wants/web@seamark.service` and 
`docker-compose.yml` to `/etc/docker/compose/seamark/docker-compose.yml`

run `systemctl daemon-reload`, followed by `systemctl start tiles.service`.

The service file mounts `/var/data/tiles` as `/data` inside the container.
