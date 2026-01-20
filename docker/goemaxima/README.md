
A maxima CAS server for STACK 

- https://github.com/mathinstitut/goemaxima
- https://hub.docker.com/r/mathinstitut/goemaxima
  

Clean list of just the names and ports.
```bash
docker ps --format "table {{.Names}}\t{{.Ports}}"
```

```bash
docker compose up -d
```

```bash
export LOCALSITENAME="goemaxima"
export SITETYPE="PROXY"
./CreateApacheLocalSite.sh
```

```bash
nano /etc/apache2/sites-available/goemaxima.mini.pc-ssl.conf
```

```bash
    # Proxy for goemaxima
    ProxyPass / http://0.0.0.0:7080/
    ProxyPassReverse / http://0.0.0.0:7080/
```

goemaxima Logs: Check why the container might be rejecting the connection:
```bash
docker logs -f goemaxima
```
