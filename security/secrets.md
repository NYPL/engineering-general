# Secrets Management

If secrets (e.g. API keys, database logins, or other credentials) are to be stored or shared, they MUST be stored or shared in one secure place, to signify one source of truth and to make resources easier to find.

[AWS Parameter Store](http://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-paramstore.html) SHOULD be used to store secrets.

## Parameter Store

### Name conventions

Parameter names MUST use a hierarchy and list the environment name and other descriptors.

The name MUST include the following:

- The first segment of the parameter name MUST be environment/stage/tier if applicable.
- The service that this is a parameter for.
- The app that uses this secret. This could be omitted if it's a resource shared by multiple apps.
- A description of what this is.

Examples may be:

- `/production/mms/rds/password-for-mms_productions-root-user`
- `/production/elasticcache/my-cluser-name/password`
- `/loggly/my-loggly-user-name/api-key` (environment/stage/tier isn't applicable)

### Value conventions

Values MUST be stored as the `SecureString` type.

Values SHOULD be encrypted using the KMS Key ID `alias/secrets-key`. 

A description SHOULD be provided (e.g. using the `--description` flag).

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

## Encrypting/Decrypting

### Using the AWS Command Line

To encrypt a secret using the AWS command line:

```
aws kms encrypt --key-id alias/lambda-default --profile nypl-digital-dev --query CiphertextBlob --output text --plaintext "THIS IS A SECRET"
```

returns:

`AQECAHh7ea2tyZ6phZgT4B9BDKwguhlFtRC6hgt+7HbmeFsrsgAAAGkwZwYJKoZIhvcNAQcGoFowWAIBADBTBgkqhkiG9w0BBwEwHgYJYIZIAWUDBAEuMBEEDHM+CBbD63yvLYX7YAIBEIAmPAZ1EOrQMd5GRao2MTOyY16JZmMhOgDNJWvy1V3eWr1xHIWIuRo=`

To decrypt a secret using the AWS command line:

```
aws kms decrypt --profile nypl-digital-dev --query Plaintext --output text --ciphertext-blob fileb://<(echo "AQECAHh7ea2tyZ6phZgT4B9BDKwguhlFtRC6hgt+7HbmeFsrsgAAAGkwZwYJKoZIhvcNAQcGoFowWAIBADBTBgkqhkiG9w0BBwEwHgYJYIZIAWUDBAEuMBEEDK5NDY0/rIiVt3rp4AIBEIAm5tjVxfouymAm2+UDCc6aYesUxlAXvU5lgI9VlQBYIrl7LozlQ2o=" | base64 --decode) | base64 --decode
```

returns:

`THIS IS A SECRET`