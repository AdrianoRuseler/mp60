
A web-based collaborative LaTeX editor 

- https://www.overleaf.com/
- https://github.com/overleaf/toolkit
- https://github.com/overleaf/toolkit/blob/master/doc/quick-start-guide.md
  

Clean list of just the names and ports.
```bash
docker ps --format "table {{.Names}}\t{{.Ports}}"
```

Clone the toolkit:
```bash
git clone https://github.com/overleaf/toolkit.git ./overleaf-toolkit
cd overleaf-toolkit
```

Initialize the configuration:
```bash
./bin/init

nano config/overleaf.rc
nano config/variables.env

./bin/up
./bin/up -d
./bin/start

./bin/stop
```

```bash
nano config/variables.env

OVERLEAF_BEHIND_PROXY=true
OVERLEAF_SITE_URL=https://overleaf.mini.pc
SIBLING_CONTAINERS_ENABLED=false
```

```bash
export LOCALSITENAME="overleaf"
export SITETYPE="PROXY"
./CreateApacheLocalSite.sh
```

```bash
nano /etc/apache2/sites-available/overleaf.mini.pc-ssl.conf
```

```bash
<VirtualHost *:80>
    ServerName sharelatex.example.com

    # Redirect all traffic to HTTPS (Recommended)
    RewriteEngine On
    RewriteCond %{HTTPS} off
    RewriteRule ^/?(.*) https://%{SERVER_NAME}/$1 [R,L]
</VirtualHost>

<VirtualHost *:443>
    ServerName sharelatex.example.com

    SSLEngine on
    SSLCertificateFile /path/to/cert.pem
    SSLCertificateKeyFile /path/to/key.pem

    # Handle WebSockets (Crucial for the editor to work)
    ProxyPass /socket.io/ ws://127.0.0.1:8077/socket.io/
    ProxyPassReverse /socket.io/ ws://127.0.0.1:8077/socket.io/

    # Handle standard HTTP traffic
    ProxyPass / http://127.0.0.1:8077/
    ProxyPassReverse / http://127.0.0.1:8077/

    # Increase timeout for long-running LaTeX compilations
    ProxyTimeout 300
</VirtualHost>
```

```bash
systemctl reload apache2
```

```bash
docker network ls
```
