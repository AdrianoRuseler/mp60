pgAdmin
The Most Popular PostgreSQL Admin Tool

- https://www.pgadmin.org/
- https://www.postgresql.org/
- https://hub.docker.com/_/postgres
  
```bash
nano docker-compose.yml
docker compose up -d
```

nano /etc/apache2/sites-available/pgadmin.mini.pc-ssl.conf

```bash
ProxyPreserveHost On
ProxyPass / http://0.0.0.0:8079/
ProxyPassReverse / http://0.0.0.0:8079/
```

postgres_db Logs: Check why the container might be rejecting the connection:
```bash
docker logs -f postgres_db
```