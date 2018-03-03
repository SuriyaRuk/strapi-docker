<p align="center"><img src="https://cldup.com/7umchwdUBh.png" /></p>
<h3 align="center">API creation made simple, secure and fast.</h3>
<p align="center">The most advanced open-source Content Management Framework to build powerful API with no effort.</p>

***

# [Strapi](https://github.com/strapi/strapi) containerized

> [Read the Medium post to have full explaination](https://medium.com/@lucaperret/strapi-quickstart-with-docker-d77ca7c86c1f)

[![Travis](https://img.shields.io/travis/strapi/strapi-docker.svg?style=for-the-badge)](https://travis-ci.org/strapi/strapi-docker)
[![GitHub release](https://img.shields.io/github/release/strapi/strapi-docker.svg?style=for-the-badge)](https://github.com/strapi/strapi-docker/releases)
[![Docker Pulls](https://img.shields.io/docker/pulls/strapi/strapi.svg?style=for-the-badge)](https://hub.docker.com/r/strapi/strapi)

## Quickstart (recommended)

1. `git clone https://github.com/strapi/strapi-docker && cd strapi-docker`
2. Run using `docker-compose up`

## Pull from Docker Hub

```bash
docker pull strapi/strapi
```

### Then run image

Start a database (e.g. MongoDB)

```bash
docker run -e MONGO_INITDB_DATABASE=strapi \
           -v `pwd`/db/:/data/db \
           -p 27017 \
           --name mongo \
           -d mongo
```

Start strapi

```bash
docker run -e APP_NAME=strapi-app \
           -e DATABASE_CLIENT=mongo \
           -e DATABASE_HOST=mongo \
           -e DATABASE_PORT=27017 \
           -e DATABASE_NAME=strapi \
           -v `pwd`/strapi-app:/usr/src/api/strapi-app \
           -v /usr/src/api/strapi-app/node_modules \
           --link mongo \
           -p 1337:1337 \
           --name strapi -d strapi/strapi
```

You should the be able to access your Strapi installation at [localhost:1337](http://localhost:1337).

## Use as base image

```Dockerfile
FROM strapi/strapi
```

## Environment variables

- `APP_NAME` to override the `strapi-app` generated folder name (you should also update the volumes paths).
- `DATABASE_CLIENT` a database providers supported by Strapi: MongoDB, Postgres, MySQL, Sqlite3 and Redis.
- `DATABASE_HOST` database service name.
- `DATABASE_PORT` depends on your database client.
- `DATABASE_NAME` initializes a database with specific name (default strapi). When using MongoDB, you should also update the `MONGO_INITDB_DATABASE` environment in the db service.
- `DATABASE_USERNAME` set the username of the database connection.
- `DATABASE_PASSWORD` set the password of the database connection.
