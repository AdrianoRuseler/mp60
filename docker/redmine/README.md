The WordPress rich content management system can utilize plugins, widgets, and themes.

- https://www.redmine.org/
- https://hub.docker.com/_/wordpress


```bash
export LOCALSITENAME="redmine"
export SITETYPE="PROXY"
./CreateApacheLocalSite.sh
```
  
```bash
nano docker-compose.yml
docker compose up -d
```

Clean list of just the names and ports.
```bash
docker ps --format "table {{.Names}}\t{{.Ports}}"
```

```bash
nano /etc/apache2/sites-available/redmine.mini.pc-ssl.conf

systemctl reload apache2
```

```bash
    # Proxy Settings
    ProxyPreserveHost On
    ProxyRequests Off
    ProxyPass / http://0.0.0.0:3000/
    ProxyPassReverse / http://0.0.0.0:3000/

    # Optional: Security headers
    <Location />
        Order allow,deny
        Allow from all
    </Location>

    # Forward necessary headers
#    RequestHeader set X-Forwarded-Proto "https"
 #   RequestHeader set X-Forwarded-Port "443"
```

redmine Logs: Check why the container might be rejecting the connection:
```bash
docker logs -f redmine
```
