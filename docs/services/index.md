# Services

All services run as Docker Compose containers directly on the homelab server (`192.168.1.30`), alongside two host-level (non-containerized) services. There's currently **no reverse proxy** — everything is accessed directly by IP and port.

## Host-level services

| Service | Purpose |
|---|---|
| OpenSSH | Remote shell access |
| Tailscale | WireGuard-based mesh VPN for remote access without port-forwarding |

## Docker containers

| Service | URL | Notes |
|---|---|---|
| [Immich](immich.md) | `http://192.168.1.30:2283` | Self-hosted photo/video backup |
| [Seafile](seafile.md) | `http://192.168.1.30:8181` | File sync & share |
| [Mealie](mealie.md) | `http://192.168.1.30:9000` | Recipe manager |
| [Stirling PDF](stirling-pdf.md) | `http://192.168.1.30:40000` | PDF toolkit |
| [Dockhand](dockhand.md) | `http://192.168.1.30:3000` | Docker container management UI |
| Redis | — (internal only) | Cache/queue backend for Immich |
| MariaDB | — (internal only) | Database backend |

!!! note "No reverse proxy yet"
    Services are reached directly by port. If a reverse proxy (Traefik, Nginx Proxy Manager, Caddy) gets added later, update each service page's "Access" section and add a new page here describing the proxy setup.
