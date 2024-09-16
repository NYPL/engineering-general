# Using Amazon Web Services [AWS]

NYPL Digital uses a variety of services provided by AWS, including

- Simple Storage Service [S3] -- used for basic storage of data
- Elastic Container Service [ECS]-- for hosting apps
- Elastic Beanstalk Service [EBS] -- for deploying web services
- CloudWatch -- a logging tool

## Accessing AWS

### Basic Requirements Supplied by DevOps

- A VPN account
- An AWS Identity and Access Management [IAM] account tied to one or more NYPL Digital account IDs, e.g. `nypl` or `nypl-dev`, depending on what infrastructure you need to access. See [Commonly Used Accounts](../on-off-board/onboarding.md/#commonly-used-accounts) for a list of Digital account IDs.
- A multifactor account associated with each AWS identity you need to access.

### Log in to AWS Control Panel

1. Meet the above requirements.
2. Connect to VPN.
3. Log into [AWS control panel](https://console.aws.amazon.com).

## How-tos

### [How to SSH to a Dockerized ECS App](aws-ecs-ssh.md)