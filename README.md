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