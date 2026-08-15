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
