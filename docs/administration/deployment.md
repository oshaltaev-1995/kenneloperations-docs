# Deployment and rollback

Deployment is a controlled release operation, not a side effect of documentation publication.

## Preflight

1. Select an exact tested release commit and confirm the local branch and remote are clean and equal.
2. Require a normal fast-forward update; never force production history.
3. Review release migrations and define invariants and rollback criteria before write-stop.
4. Retain the old application images/source identity.
5. Create a fresh write-stop PostgreSQL custom dump and matching media archive if media changed.
6. Validate checksum sidecars, `pg_restore --list`, and archive listing; copy rollback artifacts off-host.
7. Restore the database backup into an isolated PostgreSQL instance and rehearse migrations when schema/domain risk warrants it.

## Candidate activation

1. Stop writes for the controlled window.
2. Build/pull the exact candidate without discarding old images.
3. Run `alembic upgrade head` once against the candidate database.
4. Verify schema head and release-specific database invariants.
5. Start the candidate services.
6. Check health, container state, logs, authentication, key read workflows, and release-specific smoke tests.
7. Reopen writes only after acceptance.

Do not place credentials in commands committed to Git. Resolve environment and host paths from the private runbook/environment at execution time.

## Rollback

Rollback is a coordinated restoration of:

```text
old database snapshot
+ compatible media snapshot (when required)
+ old application images/source
```

Do **not** rely on Alembic downgrade for the P7 housing cutovers. D1 includes many-to-one identity migrations; a downgrade cannot reconstruct the original source assignment unambiguously. Restore the verified pre-deployment snapshot instead.

Rollback criteria include migration/invariant failure, health failure, persistent application errors, authentication loss, corrupt critical workflows, or data correctness regression. Preserve evidence and keep writes stopped until either the candidate is accepted or the old release is fully restored and checked.
