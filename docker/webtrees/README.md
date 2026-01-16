The WordPress rich content management system can utilize plugins, widgets, and themes.

- https://wordpress.org/
- https://hub.docker.com/_/wordpress


```bash
export LOCALSITENAME="webtrees"
export SITETYPE="PROXY"
./CreateApacheLocalSite.sh
```
  
```bash
nano docker-compose.yml
docker compose up -d
```

nano /etc/apache2/sites-available/webtrees.mini.pc-ssl.conf

```bash
# Proxy Settings
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:8078/
    ProxyPassReverse / http://127.0.0.1:8079/

    # Security Headers
    RequestHeader set X-Forwarded-Proto "https"
```

webtrees Logs: Check why the container might be rejecting the connection:
```bash
docker logs -f webtrees
```
