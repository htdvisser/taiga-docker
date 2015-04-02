# htdvisser/taiga-front-dist

[Taiga](https://taiga.io/) is a project management platform for startups and agile developers & designers who want a simple, beautiful tool that makes work truly enjoyable.

This Docker image can be used for running the Taiga frontend. It works together with the [htdvisser/taiga-back](https://registry.hub.docker.com/u/htdvisser/taiga-back/) image.

[![GitHub forks](https://img.shields.io/github/forks/htdvisser/taiga-docker.svg?style=flat-square)](https://github.com/htdvisser/taiga-docker)
[![GitHub issues](https://img.shields.io/github/issues/htdvisser/taiga-docker.svg?style=flat-square)](https://github.com/htdvisser/taiga-docker/issues)

## Running

A [htdvisser/taiga-back](https://registry.hub.docker.com/u/htdvisser/taiga-back/) container should be linked to the taiga-front-dist container. Also connect the volumes of this the taiga-back container if you want to serve the static files for the admin panel.

```
docker run --name taiga_front_dist_container_name --link taiga_back_container_name:taigaback --volumes-from taiga_back_container_name htdvisser/taiga-front-dist
```

## Docker-compose

For a complete taiga installation (``htdvisser/taiga-back`` and ``htdvisser/taiga-front-dist``) you can use this docker-compose configuration:

```
data:
  image: tianon/true
  volumes:
    - /var/lib/postgresql/data
    - /usr/local/taiga/media
    - /usr/local/taiga/static
    - /usr/local/taiga/logs
db:
  image: postgres
  environment:
    - POSTGRES_USER=taiga
    - POSTGRES_PASSWORD=password
  volumes_from:
    - data
taigaback:
  image: htdvisser/taiga-back:stable
  hostname: dev.example.com
  environment:
    - SECRET_KEY=examplesecretkey
    - EMAIL_USE_TLS=True
    - EMAIL_HOST=smtp.gmail.com
    - EMAIL_PORT=587
    - EMAIL_HOST_USER=youremail@gmail.com
    - EMAIL_HOST_PASSWORD=yourpassword
  links:
    - db:postgres
  volumes_from:
    - data
taigafront:
  image: htdvisser/taiga-front-dist:stable
  hostname: dev.example.com
  links:
    - taigaback
  volumes_from:
    - data
  ports:
    - 0.0.0.0:80:80
```

## Environment

* ``PUBLIC_REGISTER_ENABLED`` defaults to ``true``
* ``API`` defaults to ``"/api/v1"``
