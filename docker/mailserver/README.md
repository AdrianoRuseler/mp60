
A production-ready fullstack but simple containerized mail server (SMTP, IMAP, LDAP, Anti-spam, Anti-virus, etc.).

- https://github.com/docker-mailserver/docker-mailserver

- https://hub.docker.com/r/bitnami/openldap
- https://github.com/osixia/docker-openldap
- https://github.com/lldap/lldap/blob/main/example_configs/mailserver.md
- https://www.youtube.com/watch?v=U_TYtCutTVE
  
```bash
docker compose up -d
```

```bash
export LOCALSITENAME="mail"
export SITETYPE="PROXY"
./CreateApacheLocalSite.sh
```

```bash
nano /etc/apache2/sites-available/mail.mini.pc-ssl.conf
```

```bash
# Security Header
    Header set X-Content-Type-Options "nosniff"

    # Proxy for Roundcube
    ProxyPass / http://mediawiki:8076/
    ProxyPassReverse / http://mediawiki:8076/
```


docker exec -ti <CONTAINER NAME> setup


mailserver Logs: Check why the container might be rejecting the connection:
```bash
docker logs -f mailserver
```
docker exec -ti 2eeb1d5416af setup email add user@example.com "yourpassword"
./setup.sh email add user@example.com "yourpassword"