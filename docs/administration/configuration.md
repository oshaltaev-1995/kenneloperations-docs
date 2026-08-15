# Configuration

Configuration is supplied through `.env` files derived from checked-in templates. Production values are never committed.

## Configuration groups

| Area | Examples of names/concepts |
| --- | --- |
| Database | PostgreSQL database, user, password, and application URL |
| Application | environment mode, debug flag, allowed origins/hosts, session signing and cookie policy |
| Email | SMTP host, port, transport security, sender, username, and password |
| Account actions | public frontend base URL and token/session expiry |
| Explores | base URL, authentication credentials, tenant/location identifiers, timeout, preview expiry, departure-point mapping |
| Media | dog-photo and raw-data storage roots |
| Compose | local published backend/frontend/PostgreSQL ports |
| Backup | compose file, backup destination, and media path list |

Use placeholders such as `change-me` only in local templates. Never copy production values, cookies, tokens, private keys, raw customer data, or staff email addresses into documentation or issue logs.

## Validation

- Backend settings validate required production values at startup.
- Email readiness is observable to authorized administrators without returning credentials.
- Explores Preview should fail safely when connector configuration is absent or invalid.
- Production must use secure cookies/TLS and non-debug mode.
- Changes to environment, email, Explores mapping, or backup roots are operational changes and require an explicit runbook review.
