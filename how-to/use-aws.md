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

### SSH to a Dockerized ECS App

Using a terminal to access a Dockerized ECS app is only recommended for Dev and QA instances for the purposes of debugging. Accessing a production instance is risky and should be avoided. If accessing logs on a production service is necessary, consider using AWS Cloudwatch or installing New Relic monitoring. 

#### Requirement for SSH

- A shared key file associated with the AWS account you wish to access, e.g. `dgdvteam.pem`, must be located in the `~/.ssh` directory of your local machine. This file can be provided by a colleague or DevOps.
- Set permissions on the local file to `600`

To interact with an app via SSH you must first access the ECS "cluster" that contains the Docker image. Then you must run bash on the container for that image.

1. [Log into the AWS control panel](#log-in-to-aws-control-panel).
2. Select "Elastic Container Service" from the bar at the top of the dashboard.
3. Select the "cluster" you wish to access.
4. Click the "Infrastructure" tab.
5. Under "Container Instances," click any active instance.
6. At the bottom-right of the Container Instance page will be a Private IP number. Copy it.
7. In your terminal type `ssh -i ~/.ssh/[your_shared_ssh_key.pem] ec2-user@[private_IP]`
8. Once logged in, type `docker ps` to get the container ID. Some instances may have multiple containers. Check the name/process to make sure you copy the correct ID.
9. Type `docker exec -it [container_ID] bash`.
10. You are now logged into the container and may issue terminal commands to interact with it.