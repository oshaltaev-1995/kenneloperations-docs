# Archive

Archive is a lifecycle-first historical profile for dogs no longer current in kennel operations. Archived and Deceased profiles do not expose operational availability, temporary-status editing, Front Yard assignment, or Team Builder controls.

## Historical metadata

- `exit_or_death_on`: date the dog left the kennel or died;
- `post_kennel_fate`: normalized outcome;
- `post_kennel_fate_details`: optional contextual text.

Supported fate values are:

| Value | Meaning |
| --- | --- |
| `adopted` | Moved to a private home |
| `another_kennel` | Moved to another kennel |
| `returned_to_breeder` | Returned to breeder |
| `euthanized` | Euthanized |
| `natural_death` | Natural death |
| `other` | Other known outcome |
| `unknown` | Outcome not known |

Archived can transition directly to Deceased. Death outcomes make the lifecycle presentation unambiguous without discarding earlier archive history.

The historical profile summarizes identity, pedigree text, former housing, lifecycle events, seasonal metrics, and meaningful work. Historical work is collapsed initially; its true total remains visible, while expansion projects only the latest ten records. No history is truncated in storage or excluded from analytics.

## Permanent deletion

Permanent deletion is exceptional, Archived-only, and restricted to Admin and Manager roles. It is intended for accidental/test/duplicate records with no meaningful references.

The server preflight checks housing, status, operational assignment, work/activity, Operations/Actual, Training, family, and rule/configuration references. Typed canonical-name confirmation is additional UX protection. The final transaction locks/rechecks eligibility and deletes only the dog and safe dog-owned non-business data. It never cascades, detaches, anonymizes, or rewrites business history. If any blocker exists, the dog remains Archived.
