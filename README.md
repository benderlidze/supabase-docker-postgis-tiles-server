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
https://help.zerossl.com/hc/en-us/articles/360058295854-Installing-SSL-Certificate-on-Apache


Apache2 proxy settings 
`<VirtualHost 172.245.6.196:443>
    ServerName 172.245.6.196:8000

    SSLEngine on
    SSLProxyEngine On
    SSLCertificateFile /etc/ssl/certificate.crt
    SSLCertificateKeyFile /etc/ssl/private/private.key

    ProxyRequests Off
    ProxyPreserveHost On
    ProxyPass / http://172.245.6.196:8000/
    ProxyPassReverse / http://172.245.6.196:8000/
</VirtualHost>

SSLEngine                on
SSLCertificateFile       /etc/ssl/certificate.crt
SSLCertificateKeyFile    /etc/ssl/private/private.key
SSLCertificateChainFile  /etc/ssl/ca_bundle.crt`
