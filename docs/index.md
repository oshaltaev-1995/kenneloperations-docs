# Kennel Operations documentation

Kennel Operations supports the daily operation of a Rovaniemi sled-dog kennel. It joins dog lifecycle and housing records with operational planning, training, work capture, reconciliation, printing, exports, and workload analytics.

## Current scope

- Dog registry, lifecycle, status periods, photos, pedigree text, and historical profiles
- Date-effective housing history and kennel map
- Work/activity history and workload safety projections
- Operations Plans fed manually or through the read-only Explores integration
- Winter automatic team generation and persisted harness geometry
- Planned-to-Actual reconciliation and corrections
- Saved Training Groups, Daily Plans, Autumn harnesses, and Carousel sessions
- Daily Entry and Vanha/Uusi TULOSTE work tally sheets
- Analytics with XLSX, PDF, and CSV outputs
- Invite-only email authentication and role-based authorization

## Architecture at a glance

```text
Browser / Angular
        |
        v
FastAPI application ----> Explores (read only)
        |                SMTP/email provider
        |                photo/media storage
        v
PostgreSQL

Scheduled backup process -> database dump + media archive + checksums
```

## Choose a starting point

- **Operator:** the illustrated Quick Start and User Guide are planned as separate, access-controlled documentation. Use the Domain pages here for system semantics.
- **Developer:** start with [Architecture](overview/architecture.md), [Local development](development/local-development.md), and [Testing](development/testing.md).
- **Administrator:** use [Deployment](administration/deployment.md), [Backups and recovery](administration/backups-and-recovery.md), and [Authentication and roles](administration/authentication-and-roles.md).
- **Integrator:** read the [Explores contract](integrations/explores.md).

!!! note "Publication boundary"
    This site is sanitized technical documentation. It intentionally contains no production credentials, staff/customer records, real operational notes, or production screenshots.
