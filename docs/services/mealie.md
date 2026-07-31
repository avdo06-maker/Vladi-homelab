# Mealie

Self-hosted recipe manager and meal planner.

## Access
- URL: `http://192.168.1.30:9000`
- Reverse proxy: none currently

## docker-compose.yml

```yaml
services:
  mealie:
    image: ghcr.io/mealie-recipes/mealie:latest
    container_name: mealie
    restart: unless-stopped
    ports:
      - "9000:9000"        # web UI, exposed directly (no reverse proxy yet)
    volumes:
      - ./mealie-data:/app/data/   # recipes, images, and the SQLite database
    environment:
      - TZ=<TIMEZONE>
      - BASE_URL=http://192.168.1.30:9000
```

!!! note "Database"
    Mealie defaults to an embedded SQLite database (stored in the `mealie-data` volume above) unless configured for Postgres. Update this page if a separate database container is actually in use.
