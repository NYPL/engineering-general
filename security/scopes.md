# Platform OAuth Scopes

Scopes are used to specify access on [NYPL platform services](http://platformdocs.nypl.org/).

Scopes let you specify exactly what type of access you need. Scopes limit access for OAuth tokens. They do not grant any additional permission beyond that which the user already has.

## Common Scopes

These scopes are common to all services:

- `openid`: required by [OpenID Connect specification](http://openid.net/specs/openid-connect-core-1_0.html#AuthRequest)
- `offline_access`: issues a refresh token (when applicable)

## Service-specific Scopes

### Hold Requests

- `readwrite:hold_request`
- `read:hold_request`

### Patrons

- `read:patron`

### Bibs

- `readwrite:bib`
- `read:bib`

### Items

- `readwrite:item`
- `read:item`
