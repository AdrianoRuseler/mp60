
Portainer
- https://docs.portainer.io/start/install-ce/server/docker/linux
 
```bash
nano docker-compose.yml
docker compose up -d
```

nano /etc/apache2/sites-available/portainer.mini.pc-ssl.conf

```bash
# Required for proxying to a self-signed backend
    SSLProxyEngine on
    SSLProxyVerify none
    SSLProxyCheckPeerCN off
    SSLProxyCheckPeerName off
    SSLProxyCheckPeerExpire off

    # WebSocket Support for port 9443
    RewriteEngine on
    RewriteCond %{HTTP:Upgrade} websocket [NC]
    RewriteCond %{HTTP:Connection} upgrade [NC]
    RewriteRule ^/?(.*) "wss://127.0.0.1:9443/$1" [P,L]

    ProxyPreserveHost On
    ProxyPass / https://127.0.0.1:9443/
    ProxyPassReverse / https://127.0.0.1:9443/
```

Portainer Logs: Check why the container might be rejecting the connection:
```bash
docker logs -f portainer
```