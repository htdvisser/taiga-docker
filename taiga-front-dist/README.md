# htdvisser/taiga-front-dist

[Taiga](https://taiga.io/) is a project management platform for startups and agile developers & designers who want a simple, beautiful tool that makes work truly enjoyable.

This Docker image can be used for running the Taiga frontend. It works together with the [htdvisser/taiga-back](https://registry.hub.docker.com/u/htdvisser/taiga-back/) image.

[![GitHub forks](https://img.shields.io/github/forks/htdvisser/taiga-docker.svg?style=flat-square)](https://github.com/htdvisser/taiga-docker)
[![GitHub issues](https://img.shields.io/github/issues/htdvisser/taiga-docker.svg?style=flat-square)](https://github.com/htdvisser/taiga-docker/issues)

## Running

A [htdvisser/taiga-back](https://registry.hub.docker.com/u/htdvisser/taiga-back/) container should be linked to the taiga-front-dist container. Also connect the volumes of this the taiga-back container if you want to serve the static files for the admin panel.

```
docker run --name taiga-front-dist --link taiga_back_container_name:taigaback --volumes-from taigaback htdvisser/taiga-back
```

## Environment

* ``PUBLIC_REGISTER_ENABLED`` defaults to ``true``
* ``API`` defaults to ``"/api/v1"``
