# Backups and recovery

The tracked backup architecture creates separate artifacts:

- `scripts/backup_postgres.sh`: PostgreSQL custom-format dump and SHA-256 sidecar;
- `scripts/backup_media.sh`: compressed media archive, manifest, and SHA-256 sidecar;
- `scripts/verify_backup.sh`: checksum plus format/listing validation.

Production scheduling is provided by an automatic service/timer outside the application request path. Its private host path, account details, and environment are not part of this public-safe documentation. A successful timer invocation is not enough: operators must check artifact age, non-zero size, checksums, and validation output.

## Verify an existing backup

```bash
./scripts/verify_backup.sh /safe/path/database_TIMESTAMP.dump
./scripts/verify_backup.sh /safe/path/media_TIMESTAMP.tar.gz
```

Database verification requires:

- a non-empty custom-format dump;
- a matching checksum when a sidecar is present;
- a successful `pg_restore --list`.

Media verification requires:

- a non-empty archive;
- a matching checksum when a sidecar is present;
- a successful archive listing and expected manifest/content roots.

## Recovery assurance

Periodically restore a selected database artifact into isolated PostgreSQL of the supported major version, apply only the intended rehearsal migrations, and check invariants. Extract media into an isolated directory and compare its manifest. Never test restore by overwriting production.

For a deployment, keep a fresh write-stop database/media set and an off-host copy. Backup files, manifests containing operational filenames, and hashes belong outside Git.
