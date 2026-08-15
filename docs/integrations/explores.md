# Explores integration

Explores is the authoritative external daily schedule source. Kennel Operations reads it; it never writes back to Explores.

## Preview and Apply

1. An authorized user requests Preview for a date.
2. The backend fetches and normalizes the external schedule, stores the proposed items, and returns a preview token.
3. The token is bound to the requesting user and expires.
4. Apply consumes those stored Preview items in a transaction. It performs **no external refetch**.
5. Results report deterministic created, updated, and unchanged counts.

This separation lets the operator review the exact data that Apply will use and prevents the external schedule changing between review and write.

## Accepted schedule semantics

- Offers are excluded.
- Confirmed Orders and Allotments are normalized according to their current contract.
- Departure identity is stable across repeated imports.
- PAX, program, time, and external identifiers remain authoritative where owned by Explores.
- Operational area is resolved from configured departure-point mapping. Unknown or multi-site values remain unresolved rather than being guessed.
- An operator may set a local manual area override; subsequent sync preserves that ownership.
- Saved lineups are protected from destructive external refresh.
- Absence from a later response does not delete a local departure.

Advanced pasted JSON exists only as a complete fallback when the connector is unavailable. It does not weaken the same validation/ownership rules.

## Configuration and privacy

Credentials, tokens, tenant identifiers, and endpoint secrets are environment configuration and are not published. Logs and documentation must not include raw customer order data. See [Configuration](../administration/configuration.md).
