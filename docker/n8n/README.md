
AI Workflow Automation Platform & Tools - n8n

- https://n8n.io/
  
```bash
nano docker-compose.yml
docker compose up -d
```

nano /etc/apache2/sites-available/n8n.mini.pc-ssl.conf

```bash
<VirtualHost *:80>
    ServerName n8n.mini.pc
    # Automatically redirect HTTP to HTTPS
    RewriteEngine On
    RewriteCond %{HTTPS} off
    RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
</VirtualHost>

<VirtualHost *:443>
    ServerName n8n.mini.pc

    SSLEngine on
    # Update these paths to your actual certificate and key files
    SSLCertificateFile /etc/ssl/certs/n8n.mini.pc.crt
    SSLCertificateKeyFile /etc/ssl/private/n8n.mini.pc.key

    # WebSocket Support (Critical for n8n)
    RewriteEngine On
    RewriteCond %{HTTP:Upgrade} =websocket [NC]
    RewriteRule /(.*)           ws://localhost:5678/$1 [P,L]

    # Standard HTTP Proxy
    ProxyPreserveHost On
    ProxyPass / http://localhost:5678/
    ProxyPassReverse / http://localhost:5678/

    # Forward necessary headers
    RequestHeader set X-Forwarded-Proto "https"
    RequestHeader set X-Forwarded-Port "443"

    ErrorLog ${APACHE_LOG_DIR}/n8n_error.log
    CustomLog ${APACHE_LOG_DIR}/n8n_access.log combined
</VirtualHost>
```

