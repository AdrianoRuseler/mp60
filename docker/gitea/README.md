
Easiest, fastest, and most painless way of setting up a self-hosted Git service.

- https://github.com/go-gitea/gitea
- https://github.com/go-gitea/gitea/tree/main/docker
- https://docs.gitea.com
- https://docs.gitea.com/installation/install-with-docker
- https://docs.gitea.com/usage/actions/act-runner
- https://gitea.com/gitea/act_runner
- https://hub.docker.com/r/gitea/act_runner
- https://about.gitea.com/products/tea/
  

Clean list of just the names and ports.
```bash
docker ps --format "table {{.Names}}\t{{.Ports}}"
```

```bash
nano docker-compose.yml
docker compose up -d
```

```bash
export LOCALSITENAME="gitea"
export SITETYPE="PROXY"
./CreateApacheLocalSite.sh
```

```bash
nano /etc/apache2/sites-available/gitea.mini.pc-ssl.conf
systemctl reload apache2
```

```bash
    # Proxy settings
    ProxyPreserveHost On
    ProxyRequests Off
    
    # Pass headers
    RequestHeader set X-Forwarded-Proto "https"
    RequestHeader set X-Real-IP %{REMOTE_ADDR}s
    
    # Proxy to Gitea
    ProxyPass / http://localhost:3000/
    ProxyPassReverse / http://localhost:3000/
    
    # WebSocket support for live updates
    RewriteEngine On
    RewriteCond %{HTTP:Upgrade} websocket [NC]
    RewriteCond %{HTTP:Connection} upgrade [NC]
    RewriteRule ^/?(.*) "ws://localhost:3000/$1" [P,L]
```

act_runner Logs: Check why the container might be rejecting the connection:
```bash
docker ps
docker logs -f act_runner
```

```bash
docker network ls
```

## Create the config.yaml
Run this command in your terminal (inside the same folder as your docker-compose.yml) to extract the default configuration file:

```bash
docker run --entrypoint="" --rm gitea/act_runner:latest act_runner generate-config > config.yaml
```

```bash
container:
  # Change this from "" to your network name
  network: "gitea-network"
```

- https://gitea.mini.pc

```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout /etc/ssl/private/gitea.mini.pc-selfsigned.key -out /etc/ssl/certs/gitea.mini.pc-selfsigned.crt \
  -subj "/CN=gitea.mini.pc" \
  -addext "subjectAltName=DNS:gitea.mini.pc"
```

## job container (the one that actually runs your CI steps) cannot find the Gitea server.
Even if the main act_runner container is connected to Gitea, it spawns new temporary containers for every job. By default, these new containers are isolated and don't know about your custom Docker networks or local hostnames.


Gitea, act runners spawns new temporary containers for every job in the same network as Gitea

docker compose file and config for gitea and act runner to spawn new temporary containers for every job in the same network as Gitea

