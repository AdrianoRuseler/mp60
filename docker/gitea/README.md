
Easiest, fastest, and most painless way of setting up a self-hosted Git service.

- https://github.com/go-gitea/gitea
- https://github.com/go-gitea/gitea/tree/main/docker
- https://docs.gitea.com
- https://docs.gitea.com/installation/install-with-docker
- https://docs.gitea.com/usage/actions/act-runner
- https://gitea.com/gitea/act_runner
- https://hub.docker.com/r/gitea/act_runner
  

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

goemaxima Logs: Check why the container might be rejecting the connection:
```bash
docker logs -f gitea-act-runner-1

docker logs -f gitea-act-runner
```

- https://gitea.mini.pc

```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout /etc/ssl/private/gitea.mini.pc-selfsigned.key -out /etc/ssl/certs/gitea.mini.pc-selfsigned.crt \
  -subj "/CN=gitea.mini.pc" \
  -addext "subjectAltName=DNS:gitea.mini.pc"
```