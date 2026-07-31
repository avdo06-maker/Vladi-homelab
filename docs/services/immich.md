# Immich

Self-hosted photo and video backup solution (Google Photos alternative).

## Access
- URL: `http://192.168.1.30:2283`
- Reverse proxy: none currently

!!! note "Verify against your real setup"
    This is a standard reference compose based on Immich's official deployment docs, backed by Postgres (with the pgvector/pgvecto.rs extension for ML search) and this host's existing Redis container. Confirm the actual database container/version and volume paths match what you have running, and adjust if not.

## docker-compose.yml

```yaml
services:
  immich-server:
    image: ghcr.io/immich-app/immich-server:release
    container_name: immich_server
    restart: unless-stopped
    volumes:
      - <UPLOAD_LOCATION>:/usr/src/app/upload   # where photos/videos are actually stored on disk
      - /etc/localtime:/etc/localtime:ro
    environment:
      - DB_HOSTNAME=immich_postgres
      - DB_USERNAME=postgres
      - DB_PASSWORD=<SECRET_TOKEN>
      - DB_DATABASE_NAME=immich
      - REDIS_HOSTNAME=redis
    ports:
      - "2283:2283"      # web UI + API, exposed directly (no reverse proxy yet)
    depends_on:
      - redis
      - immich_postgres

  immich_postgres:
    image: ghcr.io/immich-app/postgres:14-vectorchord0.3.0
    container_name: immich_postgres
    restart: unless-stopped
    environment:
      - POSTGRES_PASSWORD=<SECRET_TOKEN>
      - POSTGRES_USER=postgres
      - POSTGRES_DB=immich
    volumes:
      - ./immich-db:/var/lib/postgresql/data   # database files, back this up

  redis:
    image: redis:6.2-alpine
    container_name: immich_redis
    restart: unless-stopped
```

## Notes
Immich's machine-learning container (for face/object detection) is omitted here since it wasn't mentioned as running — add it if you're using smart search or facial recognition features.
