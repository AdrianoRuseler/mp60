Web UI for yt-dlp fork with yt-dlp Nightly version and -x default option for twitch streams.

- https://hub.docker.com/r/ruseler/yt-dlp-webui-xbuild
- https://github.com/AdrianoRuseler/yt-dlp-web-ui


```bash
nano docker-compose.yml
docker compose up -d
```

```bash
export LOCALSITENAME="ytdlp"
export SITETYPE="PROXY"
./CreateApacheLocalSite.sh
```

```bash
nano /etc/apache2/sites-available/ytdlp.mini.pc-ssl.conf
```

```bash
    # Proxy to yt-dlp container
    # ProxyRequests Off

    ProxyPreserveHost On
    ProxyPass / http://localhost:3033/ upgrade=websocket
    ProxyPassReverse / http://localhost:3033/

    # WebSocket proxy for RPC
    RewriteEngine On
    RewriteCond %{HTTP:Upgrade} =websocket [NC]
    RewriteRule /(.*)           ws://localhost:3033/$1 [P,L]
    RewriteCond %{HTTP:Upgrade} !=websocket [NC]
    RewriteRule /(.*)           http://localhost:3033/$1 [P,L]    

    # WebSocket support headers
    ProxyTimeout 3600
    ProxyBadHeader Ignore

    # Crucial: Tell Grafana it's being accessed via HTTPS
    RequestHeader set X-Forwarded-Proto "https"
```

```bash
# BASIC AUTHENTICATION DIRECTIVES ADDED HERE
        <Location />
                AuthType Basic
                AuthName "Restricted yt-dlp Access"
    #AuthUserFile /etc/apache2/.htpasswd  # <<< REPLACE WITH YOUR SECURE PATH
                AuthUserFile /etc/apache2/.ytdlp.htpasswd
                Require valid-user

                ProxyPass http://localhost:3033/ upgrade=websocket
                ProxyPassReverse http://localhost:3033/
    </Location>
# END OF AUTH DIRECTIVES
```