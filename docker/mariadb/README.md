
Mailpit - email & SMTP testing tool with API for developers
- https://mailpit.axllent.org/ 
  
```bash
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
docker ps
```

```bash
docker exec -u root -it <container_name> mkdir -p /app/www/public/tmp
docker exec -u root -it <container_name> chown -R abc:abc /app/www/public/tmp
docker exec -u root -it <container_name> chmod 700 /app/www/public/tmp
```
