# Authentication and roles

Production uses invite-only email onboarding. Account-action links support initial password setup and forgotten-password recovery. Passwords are hashed; browser sessions are server-managed and may be revoked when account security or role changes require it. SMTP credentials and session secrets are environment-only values.

Frontend route guards improve navigation, but FastAPI role dependencies are authoritative.

## Roles

| Role | High-level responsibility |
| --- | --- |
| Admin | System administration plus full business management |
| Manager | Kennel/business management, Explores sync/apply, historical corrections, archive metadata, and archived-dog permanent-delete preflight/delete |
| Planner | Dog management, Operations and Training planning, normal operational writes, Team Builder, seasons, and exports |
| Staff | Everyday operational execution: read operational data, save ordinary Daily Entry work, and move Dogs between current housing pens |
| Viewer | Authenticated read-only access |

## Capability matrix

| Capability | Admin | Manager | Planner | Staff | Viewer |
| --- | :---: | :---: | :---: | :---: | :---: |
| Read application data | ✓ | ✓ | ✓ | ✓ | ✓ |
| Manage users/invitations | ✓ | — | — | — | — |
| Manual import administration | ✓ | — | — | — | — |
| General Dog/status management | ✓ | ✓ | ✓ | — | — |
| Move current housing | ✓ | ✓ | ✓ | ✓ | — |
| Edit archive metadata | ✓ | ✓ | — | — | — |
| Permanent-delete archived unreferenced dog | ✓ | ✓ | — | — | — |
| Manage Operations/Training plans | ✓ | ✓ | ✓ | — | — |
| Save ordinary Daily Entry work | ✓ | ✓ | ✓ | ✓ | — |
| Explores Preview/Apply management | ✓ | ✓ | — | — | — |
| Confirm initial Operations/Training Actual | ✓ | ✓ | ✓ | — | — |
| Correct/cancel an existing Actual | ✓ | ✓ | — | — | — |
| Correct/delete canonical manual Daily Entry work | ✓ | ✓ | — | — | — |
| Export analytics | ✓ | ✓ | ✓ | — | — |

Staff's two write capabilities are deliberately narrow. They do not grant Dog-profile editing, lifecycle or status-period changes, Front Yard changes, historical Daily Entry correction/delete, archive metadata, permanent deletion, planning, exports, or user administration. Viewer has no write capability.

The table is intentionally high-level. Endpoint guards remain the source of truth; new capabilities require explicit backend authorization and corresponding frontend presentation tests.
