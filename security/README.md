# Security

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt).

# Services

Services SHOULD check [OAuth scopes](../security/oauth.md) and [OpenID Connect claims](http://openid.net/specs/openid-connect-core-1_0.html#StandardClaims) (e.g. `sub` ) for proper authorization.

Services SHOULD be on a private network inaccessible from the Internet whenever possible.

Services that are publicly exposed SHOULD be behind an API Gateway and use the API Gateway for authentication, DoS protection, and rate limiting.

Services SHOULD use HTTPS for connections.

# Applications

Applications MUST NOT expose private credentials to users or in source control (e.g. OAuth credentials, tokens, API keys, etc.).

Applications SHOULD use ENVIRONMENT variables to store private credentials (e.g. OAuth credentials, tokens, API keys, etc.).

Front-end Applications MUST NOT store any private credentials in browser cache or cookies (e.g. OAuth credentials, tokens, API keys, etc.).

Applications SHOULD protect against [XSS and CSRF](http://www.redotheweb.com/2015/11/09/api-security.html) attacks.

Applications SHOULD use HTTPS for connections.

Applications SHOULD sanitize all user inputs, url parameters or any input parameters exposed to the user to prevent attacks (e.g. XSS, SQL injection).

When storing passwords, `bcrypt` SHOULD be used.

# General Guidelines

Two-factor authentication (2FA) SHOULD be enabled for account logins (e.g. AWS, Github, etc.)

Network resources (e.g. instances, databases, etc.) are RECOMMENDED to be installed on private networks and, otherwise, MUST have IP address filtering and as few open ports as possible.
