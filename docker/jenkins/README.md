
The leading open source automation server, Jenkins provides hundreds of plugins to support building, deploying and automating any project. 

- https://www.jenkins.io/
- https://hub.docker.com/r/jenkins/jenkins
- https://www.jenkins.io/doc/book/installing/docker/
  
```bash
docker compose up -d
```

```bash
docker ps
```

```bash
docker exec <container_name_or_id> cat /var/jenkins_home/secrets/initialAdminPassword
```

- https://www.jenkins.io/doc/book/system-administration/reverse-proxy-configuration-with-jenkins/reverse-proxy-configuration-apache/
  
```bash
nano /etc/apache2/sites-available/jenkins.mini.pc-ssl.conf
```

```bash
    ProxyRequests     Off
    ProxyPreserveHost On
    AllowEncodedSlashes NoDecode

    ProxyPass         /  http://localhost:8080/ nocanon
    ProxyPassReverse  /  http://localhost:8080/
    ProxyPassReverse  /  http://jenkins.mini.pc/
    RequestHeader set X-Forwarded-Proto "https"
    RequestHeader set X-Forwarded-Port "443"

    # Required for Jenkins websocket agents
    RewriteEngine on
    RewriteCond %{HTTP:Upgrade} websocket [NC]
    RewriteCond %{HTTP:Connection} upgrade [NC]
    RewriteRule ^/?(.*) "ws://localhost:8080/$1" [P,L]
```


```bash
#a2enmod rewrite
#a2enmod proxy
#a2enmod proxy_http
# Required for Jenkins websocket agents
#a2enmod proxy_wstunnel

a2enmod rewrite proxy proxy_http proxy_wstunnel
```