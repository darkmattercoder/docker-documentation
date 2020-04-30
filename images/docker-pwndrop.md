# [linuxserver/pwndrop](https://github.com/linuxserver/docker-pwndrop)

[![GitHub Stars](https://img.shields.io/github/stars/linuxserver/docker-pwndrop.svg?style=flat-square&color=E68523&logo=github&logoColor=FFFFFF)](https://github.com/linuxserver/docker-pwndrop)
[![GitHub Release](https://img.shields.io/github/release/linuxserver/docker-pwndrop.svg?style=flat-square&color=E68523&logo=github&logoColor=FFFFFF)](https://github.com/linuxserver/docker-pwndrop/releases)
[![GitHub Package Repository](https://img.shields.io/static/v1.svg?style=flat-square&color=E68523&label=linuxserver.io&message=GitHub%20Package&logo=github&logoColor=FFFFFF)](https://github.com/linuxserver/docker-pwndrop/packages)
[![GitLab Container Registry](https://img.shields.io/static/v1.svg?style=flat-square&color=E68523&label=linuxserver.io&message=GitLab%20Registry&logo=gitlab&logoColor=FFFFFF)](https://gitlab.com/Linuxserver.io/docker-pwndrop/container_registry)
[![Quay.io](https://img.shields.io/static/v1.svg?style=flat-square&color=E68523&label=linuxserver.io&message=Quay.io)](https://quay.io/repository/linuxserver.io/pwndrop)
[![MicroBadger Layers](https://img.shields.io/microbadger/layers/linuxserver/pwndrop.svg?style=flat-square&color=E68523)](https://microbadger.com/images/linuxserver/pwndrop "Get your own version badge on microbadger.com")
[![Docker Pulls](https://img.shields.io/docker/pulls/linuxserver/pwndrop.svg?style=flat-square&color=E68523&label=pulls&logo=docker&logoColor=FFFFFF)](https://hub.docker.com/r/linuxserver/pwndrop)
[![Docker Stars](https://img.shields.io/docker/stars/linuxserver/pwndrop.svg?style=flat-square&color=E68523&label=stars&logo=docker&logoColor=FFFFFF)](https://hub.docker.com/r/linuxserver/pwndrop)
[![Build Status](https://ci.linuxserver.io/view/all/job/Docker-Pipeline-Builders/job/docker-pwndrop/job/master/badge/icon?style=flat-square)](https://ci.linuxserver.io/job/Docker-Pipeline-Builders/job/docker-pwndrop/job/master/)
[![](https://lsio-ci.ams3.digitaloceanspaces.com/linuxserver/pwndrop/latest/badge.svg)](https://lsio-ci.ams3.digitaloceanspaces.com/linuxserver/pwndrop/latest/index.html)

[Pwndrop](https://github.com/kgretzky/pwndrop) is a self-deployable file hosting service for sending out red teaming payloads or securely sharing your private files over HTTP and WebDAV.

## Supported Architectures

Our images support multiple architectures such as `x86-64`, `arm64` and `armhf`. We utilise the docker manifest for multi-platform awareness. More information is available from docker [here](https://github.com/docker/distribution/blob/master/docs/spec/manifest-v2-2.md#manifest-list) and our announcement [here](https://blog.linuxserver.io/2019/02/21/the-lsio-pipeline-project/).

Simply pulling `linuxserver/pwndrop` should retrieve the correct image for your arch, but you can also pull specific arch images via tags.

The architectures supported by this image are:

| Architecture | Tag |
| :----: | --- |
| x86-64 | amd64-latest |
| arm64 | arm64v8-latest |
| armhf | arm32v7-latest |


## Usage

Here are some example snippets to help you get started creating a container from this image.

### docker

```
docker create \
  --name=pwndrop \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Europe/London \
  -e SECRET_PATH=/pwndrop `#optional` \
  -p 8080:8080 \
  -v /path/to/appdata:/config \
  --restart unless-stopped \
  linuxserver/pwndrop
```


### docker-compose

Compatible with docker-compose v2 schemas.

```yaml
---
version: "2.1"
services:
  pwndrop:
    image: linuxserver/pwndrop
    container_name: pwndrop
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - SECRET_PATH=/pwndrop #optional
    volumes:
      - /path/to/appdata:/config
    ports:
      - 8080:8080
    restart: unless-stopped
```

## Parameters

Docker images are configured using parameters passed at runtime (such as those above). These parameters are separated by a colon and indicate `<external>:<internal>` respectively. For example, `-p 8080:80` would expose port `80` from inside the container to be accessible from the host's IP on port `8080` outside the container.

### Ports (`-p`)

| Parameter | Function |
| :----: | --- |
| `8080` | web gui |


### Environment Variables (`-e`)

| Env | Function |
| :----: | --- |
| `PUID=1000` | for UserID - see below for explanation |
| `PGID=1000` | for GroupID - see below for explanation |
| `TZ=Europe/London` | Specify a timezone to use EG Europe/London |
| `SECRET_PATH=/pwndrop` | Secret path for admin access. Defaults to `/pwndrop`. This parameter only takes effect during initial install; it can later be changed in the web gui. |

### Volume Mappings (`-v`)

| Volume | Function |
| :----: | --- |
| `/config` | Contains all relevant configuration and data. |




## User / Group Identifiers

When using volumes (`-v` flags), permissions issues can arise between the host OS and the container, we avoid this issue by allowing you to specify the user `PUID` and group `PGID`.

Ensure any volume directories on the host are owned by the same user you specify and any permissions issues will vanish like magic.

In this instance `PUID=1000` and `PGID=1000`, to find yours use `id user` as below:

```
  $ id username
    uid=1000(dockeruser) gid=1000(dockergroup) groups=1000(dockergroup)
```

## Application Setup

Access the web gui at `http://<your-ip>:8080/pwndrop` (replace `/pwndrop` with your SECRET_PATH if you set one).


## Docker Mods
[![Docker Mods](https://img.shields.io/badge/dynamic/yaml?style=for-the-badge&color=E68523&label=mods&query=%24.mods%5B%27pwndrop%27%5D.mod_count&url=https%3A%2F%2Fraw.githubusercontent.com%2Flinuxserver%2Fdocker-mods%2Fmaster%2Fmod-list.yml)](https://mods.linuxserver.io/?mod=pwndrop "view available mods for this container.")

We publish various [Docker Mods](https://github.com/linuxserver/docker-mods) to enable additional functionality within the containers. The list of Mods available for this image (if any) can be accessed via the dynamic badge above.


## Support Info

* Shell access whilst the container is running:
  * `docker exec -it pwndrop /bin/bash`
* To monitor the logs of the container in realtime:
  * `docker logs -f pwndrop`
* Container version number
  * `docker inspect -f '{{ index .Config.Labels "build_version" }}' pwndrop`
* Image version number
  * `docker inspect -f '{{ index .Config.Labels "build_version" }}' linuxserver/pwndrop`

## Versions

* **17.04.20:** - Initial Release.