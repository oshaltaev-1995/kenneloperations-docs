# Testing

## Backend

```bash
docker compose exec -T backend pytest tests -q
docker compose exec -T backend ruff check app tests
docker compose exec -T backend mypy app
```

The ordinary suite covers unit and service/API integration behavior. Destructive PostgreSQL tests use separately configured disposable databases. Important isolated suites include historical D1 migration fixtures and archived-dog permanent-delete E2E. Never point them at the normal local or production database.

## Frontend

```bash
cd frontend
npm test -- --watch=false --browsers=ChromeHeadless
npx tsc -p tsconfig.app.json --noEmit
npx tsc -p tsconfig.spec.json --noEmit
npm run build -- --configuration production --progress=false
```

Karma covers components, routing, presentation, print DOM, and service contracts. TypeScript app/spec checks catch compile-time drift independently of Karma. The production build validates the deployable Angular bundle.

## Release acceptance

Use focused tests while developing, then full gates proportional to the change. Browser/E2E and rendered print acceptance close workflows that DOM/unit tests cannot. Production-derived clone rehearsals are reserved for schema/data/domain changes where historical production shape matters.

Documentation-only changes require `mkdocs build --strict`, link/workflow validation, a privacy/secret review, and diff classification; they do not justify rerunning all application suites when no application source changed.
