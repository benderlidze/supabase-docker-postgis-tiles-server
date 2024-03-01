Install a PostGis tile server with Supabase(as api provider)

Ububntu 20.4
1) Install docker
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04
2) Supabase Self Hosted
https://supabase.com/docs/guides/self-hosting/docker#using-an-external-database
3) psql https://www.timescale.com/blog/how-to-install-psql-on-mac-ubuntu-debian-windows/
4) CREATE EXTENSION postgis; https://postgis.net/documentation/getting_started/
5) install https://t-rex.tileserver.ch/doc/serve/#usage (should be httpS)
6) t_rex serve --dbconn postgresql://postgres:your-super-secret-and-long-postgres-password@localhost:5432/ --bind 172.245.*.*

