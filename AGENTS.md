# Base44 Dev Environment

## Project Overview
This repository contains a single self-contained HTML file (`eaglercraft-26.2-u1.html`, ~75MB) — Eaglercraft, a browser-based Minecraft port. All WASM, assets, and JavaScript are inlined in the HTML. No backend, no build step, no external dependencies or credentials.

## Running the App
```bash
docker compose -f docker-compose.base44.yml up -d
```
Serves the HTML on port 3000 via nginx.

## Architecture
- **nginx:alpine** serves the static HTML file.
- The file is not named `index.html`, so `nginx-default.conf` sets it as the index.
- `nginx.conf` overrides the default to run workers as `root` (the bind-mounted repo dir has restrictive 700 permissions from the sandbox).
- Healthcheck uses `127.0.0.1` (not `localhost`) to avoid IPv6 resolution issues.

## Key Files
- `docker-compose.base44.yml` — compose setup
- `nginx.conf` — top-level nginx config (runs as root)
- `nginx-default.conf` — server block (serves eaglercraft file as index)
- `.base44/environment.json` — Base44 metadata

## Notes
- No edits to the HTML file should be needed for the app to run.
- The file is very large (~75MB); first load may take a few seconds.
- No secrets or external credentials required.
