
OpenLDAP container image.

- https://github.com/osixia/docker-openldap
- https://www.openldap.org/
- https://github.com/osixia/docker-openldap

phpLDAPadmin
- https://github.com/leenooks/phpLDAPadmin
- https://hub.docker.com/r/phpldapadmin/phpldapadmin/tags
  
```bash
docker pull phpldapadmin/phpldapadmin:latest
docker compose up -d
```

```bash
export LOCALSITENAME="webtrees"
export SITETYPE="PROXY"
./CreateApacheLocalSite.sh
```

```bash
nano /etc/apache2/sites-available/openldap.mini.pc-ssl.conf
```

```bash
# Security Header
    Header set X-Content-Type-Options "nosniff"

    # Proxy for MediaWiki
    ProxyPass / http://mediawiki:8082/
    ProxyPassReverse / http://mediawiki:8082/
```



docker run -d -p 389:389 -p 636:636 --name openldap -v ldap-data:/var/lib/openldap -v ldap-config:/etc/openldap/slapd.d openldap-alpine

```bash
# Start services
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```