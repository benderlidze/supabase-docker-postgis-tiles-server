Install a PostGis tile server with Supabase(as api provider)
https://medium.com/@frederic.rodrigo/web-mapping-comparing-vector-tile-servers-from-postgres-postgis-405055e69084

Ububntu 20.4
1) Install docker
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04
2) Supabase Self Hosted
https://supabase.com/docs/guides/self-hosting/docker#using-an-external-database
3) psql https://www.timescale.com/blog/how-to-install-psql-on-mac-ubuntu-debian-windows/
4) CREATE EXTENSION postgis; https://postgis.net/documentation/getting_started/
5) install https://t-rex.tileserver.ch/doc/serve/#usage (should be httpS)
6) t_rex serve --dbconn postgresql://postgres:your-super-secret-and-long-postgres-password@localhost:5432/ --bind 172.245.*.*
7) ZeroSSL +  /usr/bin/python3 -m http.server 80

NGINX => https://help.zerossl.com/hc/en-us/articles/360058295894-Installing-SSL-Certificate-on-NGINX

```
NGINX

server {
    listen 8001 ssl;
    server_name 172.245.6.196;

    ssl_certificate /etc/ssl/certificate.crt;
    ssl_certificate_key /etc/ssl/private.key;

    location / {
        proxy_pass http://172.245.6.196:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
    }
}


server {
    listen 6868 ssl;
    server_name 172.245.6.196;

    ssl_certificate /etc/ssl/certificate.crt;
    ssl_certificate_key /etc/ssl/private.key;

    location / {
        proxy_pass http://172.245.6.196:6767;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
    }
}

8) supabase env -> root/supabase/docker/supabase/.env

```
