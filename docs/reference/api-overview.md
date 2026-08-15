# API overview

The application API is rooted at `/api/v1`. Local development exposes FastAPI's generated OpenAPI documentation; this page describes stable capability families without duplicating every route.

| Family | Concepts |
| --- | --- |
| Health | Process/database readiness |
| Auth | Login, logout, session, invitation/password account actions |
| Users | Admin-only invitation, role, activation, email, session revocation, deletion |
| Dogs | Registry, lifecycle/archive, housing, status periods, Front Yard, photo, workload/risk/history, permanent-delete preflight |
| Activity and worklogs | Canonical sessions, Daily Entry upsert/correction, compatibility reads |
| Operations Plans | Plans, departures, teams, Explores Preview/Apply/status, Actual and reconciliation |
| Team Builder | Candidate evaluation and Winter proposal generation |
| Training Groups | Profiles, candidates, roster, archive/restore, print overview |
| Training Plans | Snapshot creation, roster/substitution, Ready/cancel/reopen, Actual/correction |
| Analytics/exports | Kennel profile, weekly/compare/snapshot, XLSX/PDF/CSV and TULOSTE exports |
| Seasons/imports | Season configuration and controlled administrative imports |

All families require authenticated roles except the explicitly designed authentication/account-action endpoints. Write authorization and state checks are enforced on the server. Clients must preserve expected revision fields for optimistic concurrency and render structured validation conflicts without retrying unsafe writes blindly.
