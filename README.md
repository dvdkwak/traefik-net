# Traefik v2.6

This docker-compose file is made to keep track of all changes in my traefik v2 and web localsetup.

Network name: web
Traefik container name: traefik_traefik

See the .env file to change names of the container and/or the generated network.

## environment variables

**COMPOSE_PROJECT_NAME**: Name of the project (traefik)
**NETWORK_NAME**: Name of the network you want to generate or connect traefik to. (web)
**DOMAIN_NAME**: Name of the domain (localhost)
**TRAEFIK_VERSION**: Treafik version to use. (v2.6)
**TRAEFIK_DASHBOARD_INSECURE**: Allow insecure access to the dashboard, can be true of false. (true)
**TRAEFIK_DASHBOARD**: Enable the traefik dashboard, true or false. (true)
**TRAEFIK_EXPOSED_DEFAULT**: Control wether containers are exposed in traefik by default or not. (false)
**CERT_MAIL**: Mail address you want to use to generate ssl certificates. (mail@localhost.com)

## How to connect a service with use of SSL

```yaml
nginx:
  container_name: ${COMPOSE_PROJECT_NAME}_test
  image: nginx
  restart: unless-stopped
  networks:
    - web
  labels:
    traefik.enable: true
    traefik.http.routers.test.rule: Host(`web.localhost`)
    traefik.http.routers.test.entrypoints: websecure
    traefik.http.routers.test.tls: true
    traefik.http.routers.test.tls.certresolver: le
```