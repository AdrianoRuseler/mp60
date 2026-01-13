
Mailpit - email & SMTP testing tool with API for developers
- https://mailpit.axllent.org/ 
  
```bash
docker compose up -d
```

nano /etc/apache2/sites-available/mailpit.mini.pc-ssl.conf

```bash
    # Proxy config
    ProxyPreserveHost On
    ProxyRequests On
    ProxyVia On

    # General proxy
    ProxyPass / http://localhost:8025/
    ProxyPassReverse / http://localhost:8025/
```

