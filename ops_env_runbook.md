## Dev vs Prod (Reproducible Setup)

### Development (local)
- Local file: `.env.dev` (ignored via `.gitignore`)
- Compose file: `docker-compose.dev.yml`

Run:
docker compose --env-file .env.dev -f docker-compose.dev.yml up -d

### Production (reproducible)
- File: `.env.prod` (committed; secrets must be replaced before deployment)
- Compose file: `docker-compose.prod.yml`
- Backend image: GHCR (`ghcr.io/tkaz-de/fastapi-backend:latest`)
- No image build in production

Run:
docker compose --env-file .env.prod -f docker-compose.prod.yml up -d
