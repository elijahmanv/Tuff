# Base44 Setup Notes

## Project Overview
This is a single-file static HTML project: `tuff.html` (~30 MB). It is a self-contained EaglercraftX 1.12 (WASM-GC) game client with all assets embedded as base64 data URIs. No backend, no database, no external dependencies.

## How to Run
```bash
docker compose -f docker-compose.base44.yml up -d
```
Serves `tuff.html` via nginx on host port 3000.

## Verification
- `curl -s -o /dev/null -w "%{http_code}" http://localhost:3000/` should return 200.
- The page shows a launch countdown screen, then loads the game client.

## Notes
- No credentials or secrets are required.
- No live-reload dev server; the file is static. After editing `tuff.html`, call `reload_preview`.
