# Nginx Container with Certbot

## Feature
this container can communicate with https.
the container create a SSL certification with Certbot

### How to create a SSL Certification
- first of all, replace www.example.com to your desired domain name in http/conf.d/default.conf.
- build & run nginx-certpod container
```
docker-compose up -d --build
```
- better to confirm that the container is communicated with http
- exec this command 

```
docker exec -it nginx-certpod certbot certonly --webroot -w /var/www -d [your desired domain name]
```
- that's it. You can communicate the container with https 
- if you want the certificated update automatically, you would use cron of host OS with below syntax

```
39 1,13 * * * root  docker exec -it nginx-certpod certbot renew --no-self-upgrade && docker exec -it nginx-certpod nginx -s reload
```
