# Authentication and roles

Production uses invite-only email onboarding. Account-action links support initial password setup and forgotten-password recovery. Passwords are hashed; browser sessions are server-managed and may be revoked when account security or role changes require it. SMTP credentials and session secrets are environment-only values.

Frontend route guards improve navigation, but FastAPI role dependencies are authoritative.

## Roles

| Role | High-level responsibility |
| --- | --- |
| Admin | User/account administration plus all Manager and Planner capabilities |
| Manager | Operational management, Explores sync/apply, Actual/correction, archive metadata, Daily Entry correction, and archived-dog permanent-delete preflight/delete |
| Planner | Dog management, Operations and Training planning, Daily Entry writes, Team Builder, seasons, and exports |
| Staff | Authenticated read access to operational data |
| Viewer | Authenticated read-only access |

## Capability matrix

| Capability | Admin | Manager | Planner | Staff | Viewer |
| --- | :---: | :---: | :---: | :---: | :---: |
| Read application data | ✓ | ✓ | ✓ | ✓ | ✓ |
| Manage users/invitations | ✓ | — | — | — | — |
| Manual import administration | ✓ | — | — | — | — |
| Manage dogs and current statuses | ✓ | ✓ | ✓ | — | — |
| Edit archive metadata | ✓ | ✓ | — | — | — |
| Permanent-delete archived unreferenced dog | ✓ | ✓ | — | — | — |
| Manage Operations/Training/Daily Entry plans | ✓ | ✓ | ✓ | — | — |
| Explores Preview/Apply management | ✓ | ✓ | — | — | — |
| Confirm initial Operations/Training Actual | ✓ | ✓ | ✓ | — | — |
| Correct/cancel an existing Actual | ✓ | ✓ | — | — | — |
| Correct canonical manual Daily Entry work | ✓ | ✓ | — | — | — |
| Export analytics | ✓ | ✓ | ✓ | — | — |

The table is intentionally high-level. Endpoint guards remain the source of truth; new capabilities require explicit backend authorization and corresponding frontend presentation tests.
