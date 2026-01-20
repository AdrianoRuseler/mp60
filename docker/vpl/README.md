
Official VPL Jail System full install on Alpine

- https://hub.docker.com/r/jcrodriguezvpl/jail-alpine-full

```bash
docker compose up -d
```

```bash
export LOCALSITENAME="vpl"
export SITETYPE="PROXY"
./CreateApacheLocalSite.sh
```

```bash
nano /etc/apache2/sites-available/vpl.mini.pc-ssl.conf
```

```bash
# Security headers
    Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains"
    Header always set X-Frame-Options DENY
    Header always set X-Content-Type-Options nosniff

# WebSocket proxy configuration - CRITICAL for VPL functionality
    # VPL uses WebSockets for real-time communication
    RewriteEngine On
    RewriteCond %{HTTP:Upgrade} websocket [NC]
    RewriteCond %{HTTP:Connection} upgrade [NC]
    RewriteRule ^/?(.*) "ws://127.0.0.1:7000/$1" [P,L]

 # Standard HTTP proxy configuration
    ProxyPreserveHost On
    ProxyPassMatch ^/(.*) http://127.0.0.1:7000/$1
    ProxyPassReverse / http://127.0.0.1:7000/

    # Handle WebSocket upgrade headers
    ProxyPass / http://127.0.0.1:7000/
    ProxyPassReverse / http://127.0.0.1:7000/
```

vpljail Logs: Check why the container might be rejecting the connection:
```bash
docker logs -f vpljail
```
