# Winter Team Builder

The Winter automatic solver belongs to Operations. It does not generate Autumn or Carousel Training groups.

## Inputs and safety

The solver works within one departure and one operational side. Vanha and Uusi candidates never mix. It supports canonical 3 km and 10 km programs, checks lifecycle and operational eligibility, projects workload including same-day saved work, enforces temporal feasibility, and applies housing/pairing relationships and dog-specific rules.

Work class is evaluated separately from availability. An Active dog can be Available and still be ineligible for automatic Winter generation:

| Work class | Automatic Winter Operations result |
| --- | --- |
| Puppy | Hard excluded |
| Junior | Hard excluded |
| Training | Hard excluded |
| Standard | Eligible when all other safety and operational requirements pass |

There is no warning override for the three pre-standard classes. Age does not independently hard-block a dog that is already Standard and does not automatically change work class or lifecycle.

Critical projected workload and hard availability/lifecycle blockers exclude automatic selection. High workload may remain selectable with an explicit warning or acknowledgement according to the workflow. Soft pairing preferences never override hard safety.

## Harness geometry

Rows have Lead, Team, and Wheel roles. A row contains one or two dogs; row order, not a left/right semantic, defines the sled layout.

| Team size | Supported row sizes |
| --- | --- |
| 5 | 1-2-2; 2-1-2 where supported |
| 6 | 2-2-2 |
| 8 | 2-2-2-2 |

Persisted `HarnessRows` are authoritative after save. A legacy flat team remains readable but no geometry is inferred from its sequence.

## Exact-home pairing

Exactly two eligible dogs sharing the same housing identity may qualify as an exact-home pair. A pen with three or more residents does **not** create an arbitrary two-dog exact-home subset. Exact-home is a pairing relation/preference, not permission to bypass eligibility.

## Dog-specific rule architecture

Runtime rules can express forced, preferred, allowed, and avoided pairs plus solo-only, lead-only, and big-sled-only constraints. Some rules can prefer a role or team. Rules are intentionally documented without production dog names. Forced structural rules are still subordinate to lifecycle, availability, workload, temporal, side, and geometry safety.

## Temporal occupancy

For supported safaris, occupancy begins at the scheduled customer time and covers briefing/prestart, expected run, and turnaround/recovery:

- briefing: 15 minutes;
- 3 km run: 30 minutes;
- 10 km run: 60 minutes;
- turnaround/recovery: 30 minutes.

Intervals are half-open: an assignment ending exactly when the next starts does not overlap. Unknown or contradictory program/distance timing cannot be treated as safely resolved.
