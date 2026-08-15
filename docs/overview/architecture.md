# Architecture

## Runtime topology

```text
User browser
  -> Caddy (TLS and routing)
     -> Angular static application
     -> FastAPI /api/v1
        -> PostgreSQL 17
        -> dog photo/media storage
        -> SMTP/email provider
        -> Explores HTTPS API (read only)
```

Docker Compose defines PostgreSQL, backend, frontend, and Caddy services in production. The Angular client uses route guards for presentation, while every protected operation is independently authorized by FastAPI.

## Backend

FastAPI endpoint families delegate business rules to services. SQLAlchemy models persist domain state, Alembic advances the schema, and Pydantic schemas define request and response contracts. Business operations that change plans, Actuals, or destructive state use explicit validation and transactional writes.

## Frontend

Angular 19 provides routed feature areas for Dashboard, Dogs, Kennel Map, Daily Entry, Operations Plans, Training, Analytics, and user administration. It renders operational PDF print views in the browser; backend export services generate spreadsheet and other data exports.

## External and file boundaries

- Explores is read-only from Kennel Operations. Preview data is stored before Apply.
- SMTP delivers invitations, login/account actions, and password recovery messages. Secrets stay in environment configuration.
- Dog photos are application-owned media referenced from the database and mounted into the backend/frontend topology.
- Backup scripts create separate database and media artifacts with checksum sidecars.

## Trust model

The browser is not a security boundary. Backend role checks, state validation, optimistic concurrency, eligibility checks, and transactional rechecks remain authoritative.
