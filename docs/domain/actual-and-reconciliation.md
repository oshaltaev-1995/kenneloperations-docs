# Actual and reconciliation

Actual converts a plan into completed operational history without rewriting what was originally planned.

For each departure, the operator can confirm an unchanged roster or record replacements, role corrections, distance corrections, did-not-start dogs, removed dogs, or a cancelled team/departure. Confirmed participants create the canonical activity session and per-dog activity records. Cancelled, removed, and did-not-start dogs receive no completed-run work.

Corrections use expected revisions, a reason, and audit/history records. The persisted Actual snapshot keeps the effective planned roster so later plan-row history cannot silently alter who the Actual represented. Retry behavior is idempotent where the API contract permits it.

Distance is validated against the operational program. A correction may change completed distance explicitly; a missing or unsafe distance is not guessed. Workload and analytics consume the corrected authoritative result rather than summing compatibility mirrors.
