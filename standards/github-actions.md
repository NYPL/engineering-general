# Github Actions

Various applications are moving from Travis CI to Github Actions for their CI/CD pipeline. While not a requirement, using Github Actions is preferred for CI/CD.
- It provides seamless integration since it's part of Github and can stay within the site when reviewing pull requests.
- Staying on the Github site allows us to manage permissions and security settings in the repo instead of navigating to a different site.
- DevOps has worked on providing a smooth [Open ID Connect](https://www.microsoft.com/en-us/security/business/security-101/what-is-openid-connect-oidc) (OIDC) auth integration so Travis keys are not rotated every few months.
- There's a large community and marketplace with pre-built action templates that can be add to projects.

Resources:
- Github's [quickstart guide](https://docs.github.com/en/actions/quickstart).

## Deploying to AWS

Applications are moving towards deployment with Docker on AWS Elastic Container Registry (ECR) and Elastic Container Service (ECS). The AWS account that an app deploys to varies per app and per portfolio team. When configuring AWS credentials with DevOps, make sure it's the appropriate credentials for the desired AWS account for the QA and production actions -- typically, the QA and production stacks are on different accounts such as `nypl-dev` and `nypl`, for example.

The following are good examples of Github Action scripts that build a Docker image, push it up to the appropriate ECR repository, and then deploy it to the appropriate ECS cluster.

- [patron-info-poller](https://github.com/NYPL/patron-info-poller/blob/main/.github/workflows/deploy-qa.yml)
- [drb-etl-pipeline](https://github.com/NYPL/drb-etl-pipeline/blob/main/.github/workflows/build-production.yaml)
- [shared-ruby](https://github.com/NYPL/shared-ruby/blob/develop/.github/workflows/build-qa.yml)

While the above examples can serve as a template, there are a few things to note:
- Make sure to have the following before the `jobs` step which is needed for OIDC:

```yml
permissions:
  id-token: write
  contents: read
```

- Every AWS account has a different IAM key. Make sure to update the `role-to-assume` configuration with the proper key obtained from DevOps.

```yml
- name: Configure AWS credentials
  uses: aws-actions/configure-aws-credentials@v2
  with:
    role-to-assume: arn:aws:iam::[REPLACE-THIS]:role/GithubActionsDeployerRole
    aws-region: us-east-1
```

- In the build step, make sure to update the `ECR_REPOSITORY` with the app's ERC repo name.
- In the `aws ecs update-service` command step, update the app's ECS cluster and service name.

## Tests and other actions

Github Actions are also great for running unit tests, creating git tags, publishing to npm, or running any other automated tasks.

Examples of Actions that run unit tests:
- [patron-info-poller](https://github.com/NYPL/patron-info-poller/blob/main/.github/workflows/run-tests.yml) (python)
- [circulation](https://github.com/NYPL-Simplified/circulation/blob/main/.github/workflows/test.yml) (python)
- [research-catalog](https://github.com/NYPL/research-catalog/blob/main/.github/workflows/testing.yml) (node)
- [digital-collections](https://github.com/NYPL/digital-collections/blob/main/.github/workflows/ci.yml) (node)

Other actions include but are not limited to:
- [deploying to Github pages](https://github.com/NYPL/nypl-design-system/blob/development/.github/workflows/gh-pages.yml)
- [creating tags and publishing to npm](https://github.com/NYPL/nypl-design-system/blob/development/.github/workflows/release.yml)
