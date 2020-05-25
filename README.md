traefik-for-dev
===============

This is a basic way to use traefik in dev with docker.

Let's imagine you have a project named "myproject" and two docker-compose services "web" and "admin"

This traefik container will make these services accessible with the local urls :

* http://web-myproject.docker.localhost
* http://admin-myproject.docker.localhost

Features

* link every dev containers to a default web entry point
* the port linked to the entrypoint is the exposed port. If there is several ports, you can force the port.
* every container of a docker compose is mapped to a url of the type http://web-myproject.docker.localhost

Quick start
-----------

```bash
docker-compose up -d
```

you can check the [traefik interface http://localhost:8080](http://localhost:8080) to see all the websites accessible on your desktop

More advanced config
--------------------

Let's imagine you have a project named "myproject" and a docker-compose service "web". This service listens the 8887 port.

example of a docker-compose.override.yml

```yaml
version: '3.7'
services:
  web:
    labels:
      # force the port to bind to the entrypoint
      - "traefik.http.services.web-myproject.loadbalancer.server.port=8887"
      # allows to change the url that will match this service
      - "traefik.http.routers.my_router.rule=Host(`web.localhost`)"
```
