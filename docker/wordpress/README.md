The WordPress rich content management system can utilize plugins, widgets, and themes.

- https://wordpress.org/
- https://hub.docker.com/_/wordpress
  
```bash
nano docker-compose.yml
docker compose up -d
```

nano /etc/apache2/sites-available/site.mini.pc-ssl.conf

```bash
   ProxyRequests Off
   KeepAlive Off
   <Proxy *>
      Order deny,allow
      Allow from all
   </Proxy>

   # These are required for https reverse proxy to work with wordpress  (They are read from `wp-config.php`)
   RequestHeader set X-Forwarded-Proto "https"
   RequestHeader set X-Forwarded-Port "443"  
   
   ProxyPass / http://0.0.0.0:8084/
   ProxyPassReverse / http://0.0.0.0:8084/

   ProxyPreserveHost On
```

wordpress Logs: Check why the container might be rejecting the connection:
```bash
docker logs -f wordpress
```