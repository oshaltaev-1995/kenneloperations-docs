# Release process

```text
scoped feature or fix
  -> focused tests
  -> full automated gates appropriate to changed code
  -> risk-based release audit
  -> controlled deployment
  -> production smoke and evidence
```

Each package states expected HEAD/schema, scope boundaries, tests, migration expectations, and acceptance decision. Keep unrelated changes out of the release commit.

## Risk proportionality

- A documentation-only or small presentation fix does not automatically require a P11-scale audit.
- Authorization, irreversible deletion, Actual/workload, print operations, and integration ownership merit workflow-specific acceptance.
- A large schema/domain release—especially a data remap—may require a production-derived clone, historical migration fixtures, destructive E2E in disposable PostgreSQL, and rendered/browser acceptance.

## Release closure

Before deployment, record the exact commit, clean/fast-forward Git state, migration chain, all gate totals, rollback backup identity, and go/no-go decision. Deployment follows the [controlled runbook](../administration/deployment.md). After smoke acceptance, preserve evidence without committing production data or credentials.
