# Secrets Management

Secrets and credentials (e.g. API keys, database logins, or other credentials) SHOULD be stored so they are not lost and can be shared appropriately. 

If secrets are to be stored or shared, they MUST be stored or shared using [AWS Parameter Store](http://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-paramstore.html).

## Parameter Store

### Name conventions

Parameter names MUST use a hierarchy and list the environment name and other descriptors:

```
environment/{service or application name}/{other descriptors}
```

For example:

```
production/bibservice/database-credentials/admin
```

### Value conventions

Values MUST be stored as the `SecureString` type.

Values SHOULD be encrypted using the KMS Key ID `d1a6a910-1455-4d62-b789-f9910bd2df68`. 

A description SHOULD be provided (using the `--description` flag).

Values MUST be in JSON. For example:

```
{"username":"admin","password":"password123"}
```

### Limits

Developers SHOULD be aware of the following limits with Parameter Store:

- Name hierarchy has a maximum of 5 levels.
- Maximum length of `name` is 2,048 characters.
- Maximum length of `value` is 4,096 characters.

See the [API Reference](http://docs.aws.amazon.com/systems-manager/latest/APIReference/API_Parameter.html) for current limits.

### Sample AWS command line commands

Adding a parameter:

```
aws ssm put-parameter --name '/development/testservice/credentials/admin' --type 'SecureString' --key-id alias/secrets-key --description 'This describes this key' --value '{"username":"admin","password":"password123"}' --profile nypl-digital-dev
```

Getting a parameter:

```
aws ssm get-parameter --name '/development/testservice/credentials/admin' --with-decryption --profile nypl-digital-dev
```