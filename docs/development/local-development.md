# Local development

## Prerequisites

- Git and Docker with Docker Compose
- Optional native workflow: Python 3.12, Node.js 22, npm, and Chrome/Chromium

## Configure and start

```bash
git clone <authorized-private-application-repository-url> kenneloperations
cd kenneloperations
cp .env.example .env
cp backend/.env.example backend/.env
docker compose up -d --build
docker compose exec -T backend alembic upgrade head
docker compose ps
```

The templates contain local placeholders. Keep derived environment files untracked and never copy production values into them.

The application repository is private. These commands are intended for authorized developers who already have access; the public documentation repository does not contain application source.

Compose publishes the frontend on `http://localhost:4210`, the API on `http://localhost:8010`, and PostgreSQL on host port `5435` by default. Local FastAPI OpenAPI is available at `/docs`; do not expose production OpenAPI solely for documentation.

## Native backend

```bash
cd backend
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements-dev.txt
alembic upgrade head
uvicorn app.main:app --reload --port 8010
```

Point `DATABASE_URL` at an isolated local PostgreSQL database.

## Native frontend

```bash
cd frontend
npm ci
npm start
```

The Angular development server uses port 4200 and the local API base. Restart/rebuild containers after backend dependency or Dockerfile changes.

## Safe shutdown

`docker compose stop` preserves containers and volumes. `docker compose down` removes containers/network but normally preserves named volumes. Never add `-v` when the database must be retained.
