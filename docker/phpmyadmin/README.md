
Bringing MySQL to the web

- https://www.phpmyadmin.net/
- https://docs.linuxserver.io/images/docker-phpmyadmin/
  
```bash
nano docker-compose.yml
docker compose up -d
```

nano /etc/apache2/sites-available/phpmyadmin.mini.pc-ssl.conf

```bash
    # Standard HTTP Proxy
    ProxyPreserveHost On
    ProxyPass / http://localhost:8081/
    ProxyPassReverse / http://localhost:8081/

    # Forward necessary headers
    RequestHeader set X-Forwarded-Proto "https"
    RequestHeader set X-Forwarded-Port "443"
```


```bash
docker network ls
```
