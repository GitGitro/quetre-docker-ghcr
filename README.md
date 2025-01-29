# quetre-docker-ghcr
Images of Quetre updated daily hosted on GHCR

This repo fetches the content of QUetre everyday from the official <a href="https://github.com/zyachel/quetre">repo</a> and build+publish on ghcr.io 
Useful if you wanna track the updates with <a href="https://getwud.github.io/wud/#/">WUD</a> for example

Usage:
```shell
$ docker run --restart unless-stopped -p 8889:8889 -d --name "quetre" ghcr.io/gitgitro/quetre
```

Or with the docker compose file provided:
```shell
services:
  quetre:
    container_name: quetre
    image: ghcr.io/gitgitro/quetre:latest
    restart: unless-stopped
    ports:
      - "127.0.0.1:3000:3000" # Replace with "3000:3000" if you don't use a reverse proxy
    environment:
      - "NODE_ENV=production"
      - "PORT=3000"
      - "CACHE_PERIOD=1h"
      - "REDIS_URL=quetre-redis:6379"
      - "REDIS_TTL=3600"

  quetre-redis:
    container_name: quetre-redis
    image: docker.io/redis:alpine
    restart: unless-stopped
```

To build from scratch:
```shell
$ docker build . -t ghcr.io/gitgitro/quetre:latest
```