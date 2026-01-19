
Mailpit - email & SMTP testing tool with API for developers
- https://mailpit.axllent.org/ 
  
```bash
docker compose up -d
```

nano /etc/apache2/sites-available/wiki.mini.pc-ssl.conf

```bash
# Security Header
    Header set X-Content-Type-Options "nosniff"

    # Proxy for MediaWiki
    ProxyPass / http://mediawiki:8082/
    ProxyPassReverse / http://mediawiki:8082/
```

```bash
docker ps
docker exec -it <container_name> php maintenance/run.php update
```
