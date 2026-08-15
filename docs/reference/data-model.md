# Data model

This is a conceptual map, not a replacement for SQLAlchemy models or Alembic.

| Entity | Responsibility and key relationships |
| --- | --- |
| `Dog` | Identity, profile, class, lifecycle, baseline, capabilities, current housing tuple, archive outcome, photo key |
| `DogHousingAssignment` | Date-effective housing intervals for a Dog |
| `DogStatusPeriod` | Temporary date-effective availability/status context |
| `DogOperationalAssignment` | Date-effective assignments such as Front Yard |
| `ActivitySession` | Canonical work event header and source identity |
| `DogActivityRecord` | Per-dog participation/result within a session |
| `Worklog` | Legacy/compatibility work representation; not an independent ledger when mirrored |
| `DailyOperationsPlan` | One date's Operations container |
| `PlannedDeparture` | Time/program/PAX/area/target context, planned teams, and Actual link |
| `PlannedTeam` | Saved roster within a departure |
| `PlannedTeamMember` | Dog, role/position, status, replacement/Actual context |
| `PlannedTeamHarnessRow` | Persisted Lead/Team/Wheel geometry for Winter or copied Training layout |
| `ActualDepartureChange` | Versioned Actual/correction audit snapshots |
| `TrainingGroup` / `TrainingGroupMember` | Organizational saved Training roster and optional manual harness metadata |
| Daily Training Plan | `PlannedDeparture`/team representation linked to a source Training Group snapshot |
| `User`, sessions, action tokens | Invite-only identity, roles, login/account actions, revocation |
| `AccessAuditEvent` | Security/destructive-action evidence such as permanent deletion |
| Explores preview/sync structures | Stored Preview, run/items, external identity, ownership and Apply result |

Foreign keys and ORM cascades are implementation details, not deletion policy. Destructive services preflight meaningful references and do not depend on a cascade to decide safety.
