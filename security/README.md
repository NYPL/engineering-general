# Security

## Services

Services SHOULD ensure their API documentation has proper [OAuth scope](../security/oauth.md) requirements in their documentation.

Services SHOULD be on a private network inaccessible from the Internet whenever possible.

Publicly exposed services SHOULD be behind an API Gateway and use the API Gateway for authentication, DoS protection, and rate limiting.

Services SHOULD use HTTPS for connections.

## Applications

Applications MUST NOT expose private credentials to users or in source control (e.g. OAuth credentials, tokens, API keys, etc.).

Applications SHOULD use environment variables to store private credentials and SHOULD be encrypted using [AWS KMS](http://docs.aws.amazon.com/kms/latest/APIReference/API_Decrypt.html) or other encryption service.

- If storing or sharing secrets, they MUST be stored or shared according to the [Secret Management](secrets.md) guidelines.

Front-end applications MUST NOT store any private credentials in browser cache or cookies.

Applications SHOULD protect against [XSS and CSRF](http://www.redotheweb.com/2015/11/09/api-security.html) attacks.

Applications SHOULD use HTTPS for connections.

Applications SHOULD sanitize all user inputs, URL parameters or any input parameters exposed to the user to prevent attacks (e.g. XSS, SQL injection).

When storing passwords, `bcrypt` SHOULD be used.

## General Guidelines

Two-factor authentication (2FA) MUST be enabled for AWS accounts and SHOULD be enabled for other accounts (e.g. Github, Optimizely, etc.)

Network resources (e.g. instances, databases, etc.) are RECOMMENDED to be installed on private networks and, otherwise, MUST have IP address filtering and as few open ports as possible.
