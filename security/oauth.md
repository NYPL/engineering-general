#  OAuth

## Credentials

Client IDs SHOULD include a namespace. For example, `nypl_holds_service` where `nypl_` is the namespace.

Client IDs SHOULD use snake-case.

Client IDs SHOULD be limited to 16 alphabetical characters.

Client secrets MUST NOT be shared across applications and MUST NOT be committed to source control or exposed publicly (see [security](README.md)).

## Scopes

Scopes are used to specify access on [NYPL platform services](http://platformdocs.nypl.org/).

Scopes let you specify exactly what type of access you need. Scopes limit access for OAuth tokens. They do not grant any additional permission beyond that which the user or application already has.

Clients SHOULD always request the most specific scopes when requesting a token.

### Common Scopes

These scopes are common to all services:

- `openid`: required by [OpenID Connect specification](http://openid.net/specs/openid-connect-core-1_0.html#AuthRequest)
- `offline_access`: issues a refresh token (when applicable)

Additional scopes can be used to define the *role* requested:

- `role:service`: used to indicate request originates from a service

### Service-specific Scopes

#### Hold Requests

- `readwrite:hold_request`
- `read:hold_request`

#### Bibs

- `readwrite:bib`
- `read:bib`

#### Items

- `readwrite:item`
- `read:item`

### User-specific Scopes

#### Patrons

- `read:patron`
