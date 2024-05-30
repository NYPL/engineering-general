# Using Amazon Web Services [AWS]

NYPL Digital uses a variety of services provided by AWS, including

- Simple Storage Service [S3] -- used for basic storage of data
- Elastic Container Service [ECS]-- for hosting apps
- Elastic Beanstalk Service [EBS] -- for deploying web services
- CloudWatch -- a logging tool

## Accessing AWS

### Basic Requirements Supplied by DevOps

- A VPN account
- An AWS Identity and Access Management [AIM] account tied to either the `nypl` or `nypl-dev` account ID or both.
- A multifactor account associated with each AWS identity you need to access.

### Log in to AWS Control Panel

1. Meet the above requirements.
2. Connect to VPN.
3. Log into [AWS control panel](https://us-east-2.signin.aws.amazon.com/oauth?client_id=arn%3Aaws%3Asignin%3A%3A%3Aconsole%2Fcanvas&code_challenge=7AjH2gmOALM8AhXV3JyBb_vocS-TA9Q2mJWbubye0q4&code_challenge_method=SHA-256&response_type=code&redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3FhashArgs%3D%2523%26isauthcode%3Dtrue%26state%3DhashArgsFromTB_us-east-2_3ced86ca70ae0768&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEKr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMiJGMEQCIAo2NADe5ruXKINGecfy0JwQCqvI%2F%2BXwoRYY12duaZ5PAiBF8EmBJk54AiyjpwkMYbgUJmkuIBsBprkWnesPsjW%2BsCqKAggzEAEaDDkxNDUzOTE4NzAxMyIMWY0nWuYEq3xEW7AtKucBpb4N93SEC%2B4uorB9fzkydDSBEpphE9tLu6WEsJmYPlJIklEtOePb0irzVu6OM8GqVV3Pgob8GRXHCGlgxw6qCma5yB2GaYPlz3ijImASpS%2BSl1C0usSRX%2BVy4w0yfkdSdiSpTAHoKVHL3bS8hSChuCD7RGBycSRPkIno4Noo8%2BPdBEP8iQXStGXVHFogEzqo1XyTPZkqrdcPo0KDF6%2BZAJw30RbOne2sTJbXGsG1isOPa6o74b9cLtezrzQrwyuQSAtSHxsOz%2Bim7Ihy%2BucJo29ZkpusU8jat85ziUImlL22X5EL8oR9MNGF47IGOpABGsBJfc8Cmy5fjIMYqjZY8Q3MNKLtnIdEqJIF%2F0wjyZHuG3bijdkhSSmuljte4Hy7qrmHhIzOED9WLVuQlsBZUvYivrieXwZchvqv%2BRiid6r36z08%2BDiYKj%2BCRPZEFFwFTH10aqqKxXeVvd4Y1jVc7SvL40P7rj%2FEGZfMTorflNAc7s643usOOZOgz3UIfBJs&X-Amz-Date=20240530T185343Z&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIA5J3WIRNCYDRPNAJX%2F20240530%2Fus-east-2%2Fsignin%2Faws4_request&X-Amz-SignedHeaders=host&X-Amz-Signature=9d44d9c81ed45f9471bafe008e68a66e3d383ab095ed314533887bc37d9e8b23).


### SSH to a Dockerized ECS App

#### Requirement for SSH

- A shared `dgdvteam.pem` file must be located in the `~/.ssh` directory of your local machine. This file can be provided by a colleague or DevOps.
- Set permissions on the local file to `600`

To interact with an app via SSH you must first access the ECS "cluster" that contains the Docker image. Then you must run bash on the container for that image.

1. [Log into the AWS control panel](#log-in-to-aws-control-panel).
2. Select "Elastic Container Service" from the bar at the top of the dashboard.
3. Select the "cluster" you wish to access.
4. Click the "Infrastructure" tab.
5. Under "Container Instances," click any active instance.
6. At the bottom-right of the Container Instance page will be a Private IP number. Copy it.
7. In your terminal type `ssh -i ~/.ssh/dgdvteam.pem ec2-user@[private_IP]`
8. Once logged in, type `docker ps` to get the container ID
9. Type `docker exec -it [container_ID] bash`

