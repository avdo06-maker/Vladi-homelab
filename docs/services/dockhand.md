# Dockhand

Web UI for managing Docker containers, Compose stacks, images, volumes, and networks on the host.

## Access
- URL: `http://192.168.1.30:3000`
- Reverse proxy: none currently

!!! warning "Security"
    Dockhand needs access to the Docker socket to manage containers, which effectively grants it root-equivalent control over the host. Keep it on the trusted LAN only (or behind auth) — never expose it to the internet.

## docker-compose.yml

```yaml
services:
  dockhand:
    image: fnsys/dockhand:latest
    container_name: dockhand
    restart: unless-stopped
    ports:
      - "3000:3000"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock   # required to manage containers/stacks on the host
      - ./dockhand-data:/app/data                    # Dockhand's own config/state
```
