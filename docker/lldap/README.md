
The Open Source for LDAP software and information. Home of OpenLDAP.

- https://docs.linuxserver.io/images/docker-ldap-auth/
- https://hub.docker.com/r/bitnami/openldap
- https://github.com/osixia/docker-openldap
- https://github.com/lldap/lldap
- https://github.com/lldap/lldap/tree/main/example_configs
  
```bash
docker compose up -d
```

```bash
export LOCALSITENAME="lldap"
export SITETYPE="PROXY"
./CreateApacheLocalSite.sh
```

```bash
nano /etc/apache2/sites-available/lldap.mini.pc-ssl.conf
systemctl reload apache2
```

```bash
    # Proxy settings
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:17170/
    ProxyPassReverse / http://127.0.0.1:17170/

    # Security Headers
    Header always set X-Frame-Options "SAMEORIGIN"
    Header always set X-Content-Type-Options "nosniff"
```

