# Dogs and lifecycle

## Three independent classifications

**Work class** describes development and work context: `puppy`, `junior`, `training`, or `standard`. Older values remain readable for compatibility, but new writes use the four canonical classes.

**Lifecycle** describes the record's operational phase: `active`, `retired`, `archived`, or `deceased`.

**Operational status** is date-effective. It combines the persistent availability baseline, temporary status periods, explicit Team Builder exclusion, lifecycle, and relevant operational assignments. It must not be inferred from a badge cached by the client.

Archived and Deceased dogs are historical and operationally unavailable. A stored baseline such as Available may remain as history, but it does not make the dog currently available.

## Status and capabilities

Capabilities (`can_lead`, `can_team`, `can_wheel`) describe possible harness roles. Baseline availability and dated periods cover injury, illness, pregnancy, rest/recovery, treatment, and restriction compatibility. Lifecycle and hard safety blockers always outrank role capability or pairing preference.

## Lifecycle transitions

- Active and Retired are normal managed lifecycle states.
- Archive removes a dog from current operational presentation while preserving history.
- Archived dogs may be restored according to lifecycle rules.
- Archived can transition directly to Deceased while retaining archive outcome metadata.
- Deceased is lifecycle-first and is not treated as an Available operational dog.

See [Archive](archive.md) for fate metadata and deletion policy.

## Dog Detail

Dog Detail is a lifecycle-aware composition rather than one flat record form:

- **Overview** combines identity, role/capabilities, current or last-known housing, co-residents, family/pedigree context, and lifecycle metadata where applicable.
- **Status & availability** projects current operational status and provides baseline, temporary-status, Front Yard, work-class, and Team Builder eligibility controls for current operational dogs.
- **Workload & activity** presents workload/risk context and canonical activity history for a selected reference date.
- **Profile & history** retains profile fields, resolved status records, date-effective housing intervals, and operational-assignment history.

Lifecycle changes the presentation boundary. Archived and Deceased profiles omit current operational controls, show last-known housing and historical summaries, and keep meaningful work collapsed with only the latest ten rows projected when expanded. Active and Retired profiles retain the operational sections allowed by their current semantics.
