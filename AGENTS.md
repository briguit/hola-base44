# Base44 Dev Environment

## Overview
Vite + React frontend (todo app) that connects to the **Base44 hosted backend** via `@base44/sdk`. No local database or backend service — the SDK calls Base44's remote API using a hardcoded `appId` in `src/api/base44Client.js`.

## Running
```
docker compose -f docker-compose.base44.yml up -d --build
```
The app is served on host port 3000 (mapped to Vite's 5173 inside the container).

## Key details
- Node 22 (per `.nvmrc`).
- Dependencies install on container startup via `npm install` (no lockfile-frozen flag since `package-lock.json` is present but install-on-boot is the pattern).
- Vite dev server binds `0.0.0.0` and accepts the preview's external hostname via `__VITE_ADDITIONAL_SERVER_ALLOWED_HOSTS` (passed through from the platform environment).
- No external secrets or credentials are required — the Base44 SDK uses only the hardcoded `appId`.
- Frontend edits hot-reload via Vite; no backend to restart.
