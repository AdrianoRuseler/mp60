
Mailpit - email & SMTP testing tool with API for developers
- https://mailpit.axllent.org/ 
  
```bash
docker compose up -d
```

```bash
export LOCALSITENAME="openwiki"
export SITETYPE="PROXY"
./CreateApacheLocalSite.sh
```

```bash
nano /etc/apache2/sites-available/openwiki.mini.pc-ssl.conf
```

```bash
    # Security Header
    Header set X-Content-Type-Options "nosniff"

    # Proxy for MediaWiki
    ProxyPass / http://0.0.0.0:8083/
    ProxyPassReverse / http://0.0.0.0:8083/
```

