# Database and migrations

PostgreSQL is the only supported persistent database. SQLAlchemy models define runtime mappings; Alembic is the schema history. The current head is:

```text
a7c3d9e1f502
```

## Routine commands

```bash
docker compose exec -T backend alembic current
docker compose exec -T backend alembic heads
docker compose exec -T backend alembic upgrade head
```

Create a revision only for an intentional schema/model change, then review generated SQL and data transforms manually.

## Recent release migrations

| Revision | Purpose |
| --- | --- |
| `d4f6a8b0c913` | Persist Winter harness rows |
| `e5b7c9d1a204` | Persist Autumn manual harness layout metadata |
| `f6a8c0d2e415` | Cut D1 from seven cells to the current five-cell structure and remap history safely |
| `a7c3d9e1f502` | Add archive outcome/date metadata |

The preceding D1 revision introduced the seven-cell 2026-07-29 layout; `f6` is the current head-era cutover. Historical PostgreSQL migration tests cover real old-state shapes, already-cut-over states, invariants, and failure safety.

## Migration safety

- Back up before upgrade and verify the dump.
- Rehearse data migrations on an isolated production-derived clone for high-risk releases.
- Fail if preconditions or row-count invariants do not match.
- Do not stamp around a failed transform.
- For D1 rollback, restore the old database snapshot; many-to-one remapping is not safely reversed by downgrade.
