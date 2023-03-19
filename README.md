# otel-grafana-demo

# 🚀 Demo application showing how to instrument a Node application with OpenTelemetry, Prometheus, Jaeger, Loki, and Grafana. Built with Next.js, Fastify, and Postgres. 🚀

https://github.com/coding-to-music/otel-grafana-demo

From / By https://github.com/connorlindsey/otel-grafana-demo

https://www.youtube.com/watch?v=ifwfyMNcMiM&ab_channel=UtahJS

## Environment variables:

```java

```

## GitHub

```java
git init
git add .
git remote remove origin
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:coding-to-music/otel-grafana-demo.git
git push -u origin main
```

# OpenTelemetry - Grafana Demo
Author: Connor Lindsey

This demo application demonstrates how to monitor a JavaScript application using open source observability software. The following projects are used:

- [OpenTelemetry](https://opentelemetry.io/) - Instrument the application and send observability data to each backend.
- [Jaeger](https://www.jaegertracing.io/) - Distributed tracing backend.
- [Prometheus](https://prometheus.io/) - Metrics and alerting backend.
- [Loki](https://grafana.com/oss/loki/) - Logs aggregation system.
- [Grafana](https://grafana.com/) - Visualize all of our observability data.

## Project Structure
![App architecture](./docs/assets/app_architecture.png)
- api/ - Fastify API. Instrumented with OpenTelemetry
- app/ - Simple Next.js app.
- db/  - Stores copy of Postgres data for persistence.
- config/ - Standard configuration for Prometheus, Promtail, Loki, etc.
- data/ - Stores server logs

## Running the app
1. Run with `npm run dev`. Requires [Docker](https://www.docker.com/) and docker-compose.
1. Optionally, run `npm install` in `/api` and `/app`.
1. Open the app at http://localhost
1. View traces, logs, and metrics in Grafana at http://localhost:3000

## Additional Resources
- [Grafana Demo](https://play.grafana.org/d/000000012/grafana-play-home?orgId=1)
- [Grafana Cloud](https://grafana.com/products/cloud/) - Actually useful free tier
- [OpenTelemetry Key Terms](https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/overview.md)
- [OpenTelemetry JS](https://github.com/open-telemetry/opentelemetry-js)
- [OpenTelemetry JS Contrib](https://github.com/open-telemetry/opentelemetry-js-contrib)
- [OpenTelemetry Status](https://opentelemetry.io/status/)
- [UtahJS Slides](https://bit.ly/3oBobaQ)

## Overview of services ports and purpose 

## Working

| Status | Service | Port | Description | Comments |
| -------- | -------- | -------- | -------- | -------- |
| Verify | Postgres | localpost@db:5432/otel-grafana-demo | Database | No Errors |
| Works | Grafana | [http://localhost:4000](http://localhost:4000) | Visualize all | No Errors |
| Works | Jaeger | [http://localhost:16686/search](http://localhost:16686/search) | Distributed tracing backend | No Errors |
| Works | Promtail | ???? | ???? | error="Post \"http://loki:3100/loki/api/v1/push\": dial tcp: lookup loki on 127.0.0.11:53: server misbehaving" |
| Mostly Works | app NextJS App | [http://localhost:3000](http://localhost:3000) | NextJS app that we will monitor | Category does not load, cannot save data |
| Works | Prisma | NA | Database Schema abstraction | Loaded by api service |
| Works | API | [http://localhost:8080](http://localhost:8080) | via Nodeman, calls prisma, connects to DB | node crypto hash: error:0308010C:digital envelope routines::unsupported |

## Issues and need to verify

| Status | Service | Port | Description | Comments |
| -------- | -------- | -------- | -------- | -------- |
| Errors | Loki | [http://localhost:XXXX](http://localhost:XXXX) | Logs aggregation system | creating WAL folder at "/wal": mkdir wal: permission denied |
| Works | Prometheus | [http://localhost:9090](http://localhost:9090) | Metrics and alerting backend | EEEEE |
| Verify | API - Metrics | [http://localhost:9464](http://localhost:9464) | ZZZZ | EEEEE |
| Verify | OpenTelemetry | YYYY | Instrument the application | EEEEE |

## Ports

- [Jaeger http://localhost:16686/search](http://localhost:16686/search) - Distributed tracing backend.
- [Prometheus http://localhost:9090](http://localhost:9090) - Metrics and alerting backend.


- [Grafana http://localhost:4000](http://localhost:4000) - Visualize all of our observability data.
- [NextJS App http://localhost:3000](http://localhost:3000) - NextJS app that we will monitor using OpenTelemetry and Grafana
- [API http://localhost:8080](http://localhost:8080)

DATABASE_URL: "postgresql://postgres:localpost@db:5432/otel-grafana-demo"


## Not working:

There is no pre-built dashboard for Grafana
 
- [API - Metrics http://localhost:9464](http://localhost:9464)

- [Loki http://localhost:XXXX](http://localhost:XXXX) - Logs aggregation system.
- [OpenTelemetry http://localhost:XXXX](http://localhost:XXXX) - Instrument the application and send observability data to each backend.

http://localhost:9080/
http://localhost:3100/ Loki

## Docker commands

```java
# General
alias dve="docker -v"
alias dl="docker login --username=dragol" 
# Explanation
# dve - prints out current docker version
# dl - docker login, will prompt you for password

# Images
alias dil="docker images"
alias dip="docker image prune -f"
# Explanation
# dil - list all docker images available on my machine
# dip - remove all dangling images -f is flag for force

# Containers
alias dcl="docker ps"
alias dcla="docker ps -a"
alias dcp="docker container prune -f"
alias dci="docker inspect"
alias dciip="docker inspect -f \"{{ .NetworkSettings.IPAddress }}\""
alias dcs="docker start"
alias dcd="docker down"
alias dcr="docker restart"
# Explanation
# dcl - list running containers
# dcla - list all containers
# dcp - remove all dangling containers
# dci - here you need to pass container id in order to get various information about particular container
# dciip - returns container IP address
# dcs - here you need to pass container id in order to start container
# dcd - here you need to pass container id in order to stop container
# dcr - here you need to pass container id in order to restart container

# Networks
alias dnl="docker network ls"
alias dni="docker network inspect"
alias dnrm="docker network rm"
alias dnp="docker network prune -f"
# Explanation
# dnl - list networks
# dni - here you need to pass network id in order to see it's details
# dnrm - here you need to pass network id in order to delete it
# dnp - remove all dangling networks

# Volumes
alias dvc="docker volume create"
alias dvl="docker volume ls"
alias dvrm="docker volume rm"
alias dvp="docker volume prune -f"
alias dvi="docker volume inspect"
# Explanation
# dvc - here you need to pass volume name in order to create it
# dvl - list volumes
# dvrm - here you need to pass volume id in order to delete it
# dvp - remove all dangling volumes
# dvi - here you need to pass volumeid in order to see it's details

# Docker-Compose
alias dcv="docker-compose -v"
alias dcu="docker-compose up"
alias dcd="docker-compose down"
alias dcb="docker-compose build --no-cache"
alias dcc="docker-compose config"
# Explanation
# dcv - prints out docker compose version
# dcu - start docker compose
# dcd - stop docker compose
# dcb - new docker compose build from ground up
# dcc - check if docker-compose.yml file is valid
```

## docker-compose.yml

```java
version: "3.7"

services:
  db:
    container_name: db
    image: postgres
    environment:
      POSTGRES_USER: postgres
      POSTGRES_DB: otel-grafana-demo
      POSTGRES_PASSWORD: localpost
    volumes:
      - ./db/data/:/var/lib/postgresql/data/ # Persist data locally
    ports:
      - 5432:5432
  api:
    container_name: api
    build: ./api
    environment:
      DATABASE_URL: "postgresql://postgres:localpost@db:5432/otel-grafana-demo"
    volumes:
      - ./api:/usr/api
      - ./data/api/:/usr/api/data/
      - /usr/api/node_modules
    ports:
      - 8080:8080 # API
      - 9464:9464 # Metrics API
    command: ./setup.sh
    depends_on: 
      - db
  app:
    container_name: app
    build: ./app
    command: npm run dev -- -p 80
    volumes:
      - ./app:/usr/app
      - /usr/app/node_modules
    ports:
      - 80:80
    depends_on: 
      - api
      - db
  # Observability services
  jaeger:
    image: jaegertracing/all-in-one:latest
    ports:
      - "5775:5775/udp"
      - "6831:6831/udp"
      - "6832:6832/udp"
      - "5778:5778"
      - "16686:16686"
      - "14268:14268"
      - "9411:9411"
  prometheus:
    image: prom/prometheus:latest
    user: root
    command:
      - --config.file=/etc/prometheus/prometheus.yml
    volumes:
      - ./config/prometheus.yml:/etc/prometheus/prometheus.yml
    ports:
      - 9090:9090

  promtail:
    image: grafana/promtail
    volumes:
      - ./config/promtail/promtail-config.yaml:/etc/promtail/promtail-config.yaml
      - ./data/api/:/usr/api/data/
    command: -config.file=/etc/promtail/promtail-config.yaml
    depends_on:
      - api
      - loki

  loki:
    image: grafana/loki
    ports:
      - 3100:3100
    volumes:
      - ./config/loki/loki-config.yaml:/etc/loki/loki-config.yaml
      - ./data/loki/data:/data/loki
    command: -config.file=/etc/loki/loki-config.yaml

  grafana:
    image: grafana/grafana:main
    environment: 
      # Disable authentication
      - GF_AUTH_DISABLE_LOGIN_FORM=true
      - GF_AUTH_ANONYMOUS_ENABLED=true
      - GF_AUTH_ANONYMOUS_ORG_NAME=Main Org.
      - GF_AUTH_ANONYMOUS_ORG_ROLE=Admin
      - GF_USERS_ALLOW_SIGN_UP=false
    volumes:
      - ./config/provisioning/:/etc/grafana/provisioning
    ports:
      - 4000:3000
```

## Start via 

```
# from the main root directory

npm run dev --ask-become-pass
```

Output

```java
> otel-grafana-demo@0.1.0 dev
> docker-compose up

Starting otel-grafana-demo_jaeger_1     ... done
Starting otel-grafana-demo_grafana_1    ... done
Starting otel-grafana-demo_prometheus_1 ... done
Starting db                             ... done
Starting otel-grafana-demo_loki_1       ... done
Starting api                            ... done
Starting app                            ... done
Starting otel-grafana-demo_promtail_1   ... done
Attaching to otel-grafana-demo_grafana_1, otel-grafana-demo_prometheus_1, otel-grafana-demo_loki_1, otel-grafana-demo_jaeger_1, db, api, app, otel-grafana-demo_promtail_1
db            | 
db            | PostgreSQL Database directory appears to contain a database; Skipping initialization
db            | 
db            | 2023-03-19 01:25:14.356 UTC [1] LOG:  starting PostgreSQL 15.2 (Debian 15.2-1.pgdg110+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 10.2.1-6) 10.2.1 20210110, 64-bit
db            | 2023-03-19 01:25:14.363 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
db            | 2023-03-19 01:25:14.367 UTC [1] LOG:  listening on IPv6 address "::", port 5432
db            | 2023-03-19 01:25:14.377 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
db            | 2023-03-19 01:25:14.382 UTC [32] LOG:  database system was shut down at 2023-03-18 22:15:57 UTC
db            | 2023-03-19 01:25:14.442 UTC [1] LOG:  database system is ready to accept connections
```

## More messages

```
app           | node:internal/crypto/hash:71
app           |   this[kHandle] = new _Hash(algorithm, xofLen);
app           |                   ^
app           | 
app           | Error: error:0308010C:digital envelope routines::unsupported
app           |     at new Hash (node:internal/crypto/hash:71:19)
app           |     at Object.createHash (node:crypto:140:10)
app           |     at BulkUpdateDecorator.hashFactory (/usr/app/node_modules/next/dist/compiled/webpack/bundle5.js:133863:18)
app           |     at BulkUpdateDecorator.update (/usr/app/node_modules/next/dist/compiled/webpack/bundle5.js:133764:50)
app           |     at OriginalSource.updateHash (/usr/app/node_modules/next/dist/compiled/webpack-sources2/index.js:1:21039)
app           |     at NormalModule._initBuildHash (/usr/app/node_modules/next/dist/compiled/webpack/bundle5.js:65771:17)
app           |     at handleParseResult (/usr/app/node_modules/next/dist/compiled/webpack/bundle5.js:65837:10)
app           |     at /usr/app/node_modules/next/dist/compiled/webpack/bundle5.js:65929:4
app           |     at processResult (/usr/app/node_modules/next/dist/compiled/webpack/bundle5.js:65646:11)
app           |     at /usr/app/node_modules/next/dist/compiled/webpack/bundle5.js:65710:5 {
app           |   opensslErrorStack: [ 'error:03000086:digital envelope routines::initialization error' ],
app           |   library: 'digital envelope routines',
app           |   reason: 'unsupported',
app           |   code: 'ERR_OSSL_EVP_UNSUPPORTED'
app           | }
app           | 
app           | Node.js v19.8.1
app exited with code 1

grafana_1     | logger=context userId=0 orgId=1 uname= t=2023-03-18T21:43:40.350818495Z level=info msg="Request Completed" method=GET path=/img/online.svg status=404 remote_addr=172.18.0.1 time_ms=116 duration=116.546774ms size=42827 referer=http://localhost:4000/ handler=notfound
grafana_1     | logger=context userId=0 orgId=1 uname= t=2023-03-18T21:43:40.363538127Z level=info msg="Request Completed" method=GET path=/img/warn-tiny.svg status=404 remote_addr=172.18.0.1 time_ms=119 duration=119.410824ms size=42827 referer=http://localhost:4000/ handler=notfound
grafana_1     | logger=context userId=0 orgId=1 uname= t=2023-03-18T21:43:40.473223813Z level=info msg="Request Completed" method=GET path=/img/background_tease.jpg status=404 remote_addr=172.18.0.1 time_ms=114 duration=114.927195ms size=42827 referer=http://localhost:4000/ handler=notfound
grafana_1     | logger=context userId=0 orgId=1 uname= t=2023-03-18T21:43:40.486267017Z level=info msg="Request Completed" method=GET path=/img/critical.svg status=404 remote_addr=172.18.0.1 time_ms=123 duration=123.021154ms size=42827 referer=http://localhost:4000/ handler=notfound
grafana_1     | logger=context userId=0 orgId=1 uname= t=2023-03-18T21:43:46.74551337Z level=info msg="Request Completed" method=GET path=/api/live/ws status=-1 remote_addr=172.18.0.1 time_ms=22 duration=22.050758ms size=0 referer= handler=/api/live/ws
grafana_1     | logger=context userId=0 orgId=1 uname= t=2023-03-18T21:44:01.565225119Z level=info msg="Request Completed" method=GET path=/api/live/ws status=-1 remote_addr=172.18.0.1 time_ms=23 duration=23.609034ms size=0 referer= handler=/api/live/ws

db            | 2023-03-18 21:56:32.835 UTC [98] ERROR:  insert or update on table "transaction" violates foreign key constraint "transaction_categoryId_fkey"
db            | 2023-03-18 21:56:32.835 UTC [98] DETAIL:  Key (categoryId)=(0) is not present in table "category".
db            | 2023-03-18 21:56:32.835 UTC [98] STATEMENT:  INSERT INTO "public"."transaction" ("createdAt","updatedAt","title","amount","categoryId") VALUES ($1,$2,$3,$4,$5) RETURNING "public"."transaction"."id"
db            | 2023-03-18 21:56:32.841 UTC [98] ERROR:  insert or update on table "transaction" violates foreign key constraint "transaction_categoryId_fkey"
db            | 2023-03-18 21:56:32.841 UTC [98] DETAIL:  Key (categoryId)=(0) is not present in table "category".
db            | 2023-03-18 21:56:32.841 UTC [98] STATEMENT:  INSERT INTO "public"."transaction" ("createdAt","updatedAt","title","amount","categoryId") VALUES ($1,$2,$3,$4,$5) RETURNING "public"."transaction"."id"
db            | 2023-03-18 21:56:32.846 UTC [98] ERROR:  insert or update on table "transaction" violates foreign key constraint "transaction_categoryId_fkey"
db            | 2023-03-18 21:56:32.846 UTC [98] DETAIL:  Key (categoryId)=(0) is not present in table "category".

promtail_1    | level=warn ts=2023-03-18T22:11:50.637727015Z caller=client.go:379 component=client host=loki:3100 msg="error sending batch, will retry" status=-1 error="Post \"http://loki:3100/loki/api/v1/push\": dial tcp: lookup loki on 127.0.0.11:53: server misbehaving"
promtail_1    | level=warn ts=2023-03-18T22:12:08.635364045Z caller=client.go:379 component=client host=loki:3100 msg="error sending batch, will retry" status=-1 error="Post \"http://loki:3100/loki/api/v1/push\": dial tcp: lookup loki on 127.0.0.11:53: server misbehaving"
promtail_1    | level=warn ts=2023-03-18T22:13:00.891646397Z caller=client.go:379 component=client host=loki:3100 msg="error sending batch, will retry" status=-1 error="Post \"http://loki:3100/loki/api/v1/push\": dial tcp: lookup loki on 127.0.0.11:53: server misbehaving"
promtail_1    | level=warn ts=2023-03-18T22:14:32.449980434Z caller=client.go:379 component=client host=loki:3100 msg="error sending batch, will retry" status=-1 error="Post \"http://loki:3100/loki/api/v1/push\": dial tcp: lookup loki on 127.0.0.11:53: server misbehaving"


Stopping otel-grafana-demo_grafana_1    ... done
Stopping otel-grafana-demo_promtail_1   ... done
Stopping api                            ... done
Stopping db                             ... done
Stopping otel-grafana-demo_jaeger_1     ... done
Stopping otel-grafana-demo_prometheus_1 ... done
```