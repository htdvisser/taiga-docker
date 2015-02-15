# htdvisser/taiga-back

[Taiga](https://taiga.io/) is a project management platform for startups and agile developers & designers who want a simple, beautiful tool that makes work truly enjoyable.

This Docker image can be used for running the Taiga backend. It works together with the [htdvisser/taiga-front-dist](https://registry.hub.docker.com/u/htdvisser/taiga-front-dist/) image.

[![GitHub forks](https://img.shields.io/github/forks/htdvisser/taiga-docker.svg?style=flat-square)](https://github.com/htdvisser/taiga-docker)
[![GitHub issues](https://img.shields.io/github/issues/htdvisser/taiga-docker.svg?style=flat-square)](https://github.com/htdvisser/taiga-docker/issues)

## Running

A [postgres](https://registry.hub.docker.com/_/postgres/) container should be linked to the taiga-back container. The taiga-back container will use the ``POSTGRES_USER`` and ``POSTGRES_PASSWORD`` environment variables that are supplied to the postgres container.

```
docker run --name taiga-back --link postgres_container_name:postgres htdvisser/taiga-back
```

## Database Initialization

To initialize the database, use ``docker exec -it taiga-back bash`` and execute the following commands:

```
cd /usr/local/taiga/taiga-back/
python manage.py loaddata initial_user
python manage.py loaddata initial_project_templates
python manage.py loaddata initial_role
```

## Environment

* ``SECRET_KEY`` defaults to ``"insecurekey"``, but you might want to change this.
* ``DEBUG`` defaults to ``False``
* ``TEMPLATE_DEBUG`` defaults to ``False``
* ``PUBLIC_REGISTER_ENABLED`` defaults to ``True``

URLs for static files and media files from taiga-back:

* ``MEDIA_URL`` defaults to ``"http://$HOSTNAME/media/"``
* ``STATIC_URL`` defaults to ``"http://$HOSTNAME/static/"``

Domain configuration:

* ``API_SCHEME`` defaults to ``"http"``
* ``API_DOMAIN`` defaults to ``"$HOSTNAME"``
* ``FRONT_SCHEME`` defaults to ``"http"``
* ``FRONT_DOMAIN`` defaults to ``"$HOSTNAME"``

Email configuration:

* ``EMAIL_USE_TLS`` defaults to ``False``
* ``EMAIL_HOST`` defaults to ``"localhost"``
* ``EMAIL_PORT`` defaults to ``"25"``
* ``EMAIL_HOST_USER`` defaults to ``""``
* ``EMAIL_HOST_PASSWORD`` defaults to ``""``
* ``DEFAULT_FROM_EMAIL`` defaults to ``"no-reply@example.com"``
