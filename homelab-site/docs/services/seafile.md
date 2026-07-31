# Seafile

Self-hosted file sync & share (Dropbox alternative).

## Access
- URL: `http://192.168.1.30:8181`
- Reverse proxy: none currently

!!! note "Verify against your real setup"
    Seafile Community Edition officially requires MariaDB + memcached as backing services. This is written assuming the host's existing MariaDB container backs Seafile — confirm that's the case (rather than MariaDB backing something else) and adjust credentials/volumes to match.

## docker-compose.yml

```yaml
services:
  seafile:
    image: seafileltd/seafile-mc:latest
    container_name: seafile
    restart: unless-stopped
    ports:
      - "8181:80"          # web UI, exposed directly (no reverse proxy yet)
    volumes:
      - ./seafile-data:/shared   # persistent Seafile data (libraries, config, logs)
    environment:
      - DB_HOST=mariadb
      - DB_ROOT_PASSWD=<SECRET_TOKEN>
      - TIME_ZONE=<TIMEZONE>
      - SEAFILE_ADMIN_EMAIL=<ADMIN_EMAIL>
      - SEAFILE_ADMIN_PASSWORD=<SECRET_TOKEN>
      - SEAFILE_SERVER_HOSTNAME=192.168.1.30
    depends_on:
      - mariadb
      - memcached

  mariadb:
    image: mariadb:10.11
    container_name: mariadb
    restart: unless-stopped
    environment:
      - MYSQL_ROOT_PASSWORD=<SECRET_TOKEN>
    volumes:
      - ./mariadb-data:/var/lib/mysql   # database files, back this up

  memcached:
    image: memcached:1.6
    container_name: seafile-memcached
    restart: unless-stopped
    entrypoint: memcached -m 256
```
