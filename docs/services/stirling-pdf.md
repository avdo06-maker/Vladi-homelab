# Stirling PDF

Self-hosted, all-in-one PDF toolkit (merge, split, convert, OCR, etc.).

## Access
- URL: `http://192.168.1.30:40000`
- Reverse proxy: none currently

## docker-compose.yml

```yaml
services:
  stirling-pdf:
    image: stirlingtools/stirling-pdf:latest
    container_name: stirling-pdf
    restart: unless-stopped
    ports:
      - "40000:8080"        # host:container — container listens on 8080 internally
    volumes:
      - ./stirling/data:/usr/share/tessdata    # OCR language data
      - ./stirling/config:/configs             # app configuration
      - ./stirling/logs:/logs
    environment:
      - DOCKER_ENABLE_SECURITY=false   # true if you set up login/auth
      - TZ=<TIMEZONE>
```
