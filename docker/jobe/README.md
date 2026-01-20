
The dockerfile and doc for building the Docker image JobeInABox 

- https://github.com/trampgeek/jobeinabox
- https://github.com/trampgeek/jobe

```bash
docker compose up -d
```

```bash
export LOCALSITENAME="jobe"
export SITETYPE="PROXY"
./CreateApacheLocalSite.sh
```

```bash
nano /etc/apache2/sites-available/jobe.mini.pc-ssl.conf
```

```bash
    # Proxy for Jobe
    ProxyPass / http://0.0.0.0:4000/
    ProxyPassReverse / http://0.0.0.0:4000/
```

jobeinabox Logs: Check why the container might be rejecting the connection:
```bash
docker logs -f jobeinabox-jobe-1
```