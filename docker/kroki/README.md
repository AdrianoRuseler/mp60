
Creates diagrams from textual descriptions!
- https://kroki.io/
- https://docs.kroki.io/kroki/setup/use-docker-or-podman/
  
```bash
nano docker-compose.yml
docker compose up -d
```

nano /etc/apache2/sites-available/kroki.mini.pc-ssl.conf

```bash
# Preserve the original Host header from the client
    ProxyPreserveHost On

    # Forward all requests to the Kroki backend
    # Assuming Kroki is running on the same machine at port 8000
    ProxyPass / http://127.0.0.1:8000/
    ProxyPassReverse / http://127.0.0.1:8000/

    # Optional: Handle large URI/header sizes if you use very complex diagrams
    LimitRequestLine 16384
    LimitRequestFieldSize 16384
```

