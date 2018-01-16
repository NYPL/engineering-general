# Onboarding

Welcome to NYPL Digital!

This document is intended to help developers become familiar with NYPL digital properties and standards.

## 1. Learn

- Review the [Contents](../README.md#contents) in the `engineering-general` repo.
  - Contains links to development standards and guidelines at NYPL.
- Review the [Master Links](../other/README.md) in the `engineering-general` repo.
  - Contains links to documentation for various services, applications, and other products at NYPL.
- Review READMEs (or Wikis) in relevant repos
  - Generally, each repo will contain more app-specific information.

## 2. Set up accounts

### Commonly used accounts

A developer will generally need accounts for the following services:
- [npm organization](https://www.npmjs.com/org/nypl)
- Slack
    - [nypl.slack.com](https://nypl.slack.com/)
- Github
    - Github organizations:
        - [NYPL](https://github.com/NYPL)
        - [NYPL-discovery](https://github.com/NYPL-discovery)
        - [NYPL-registry](https://github.com/NYPL-registry)
        - [NYPL-Simplified](https://github.com/NYPL-Simplified)
        - [nypl-spacetime](https://github.com/nypl-spacetime)
        - [nypl-open-audio](https://github.com/nypl-openaudio) (this hasn't been used in a while)
- [Docker Hub](https://hub.docker.com/u/nypl/)
- JIRA*
    - [jira.nypl.org](https://jira.nypl.org/)
- Bitbucket
    - [bitbucket.org/NYPL](https://bitbucket.org/NYPL)
- Amazon Web Services (AWS)
    - Primary AWS accounts:
        - [nypl-digital-dev](https://nypl-digital-dev.signin.aws.amazon.com/console)
        - [nypl-sandbox](https://nypl-sandbox.signin.aws.amazon.com/console)

### Less commonly used accounts

- NYPL Platform
    - [https://platform.nypl.org](https://platform.nypl.org)
- Loggly
    - [https://nypl.loggly.com](https://nypl.loggly.com)
- Bamboo*
    - [http://bamboo.nypl.org/](http://bamboo.nypl.org/)
- CI Servers (e.g Jenkins instances)
    - [https://ci-sa.prod.aws.nypl.org](https://ci-sa.prod.aws.nypl.org)
- Optimizely
    - [https://app.optimizely.com](https://app.optimizely.com)
- Google Analytics
    - [https://analytics.google.com](https://analytics.google.com)
- Amazon Web Services (AWS)
    - Secondary AWS accounts:
        - [nypl/prod](https://nypl.signin.aws.amazon.com/console)
        - [nypl-dev](https://nypl-dev.signin.aws.amazon.com/console)
        - [nypl-labs](https://nypl-labs.signin.aws.amazon.com/console)
- Data Warehouse DB credential
    - [https://github.com/NYPL/data-warehouse#users](https://github.com/NYPL/data-warehouse#users)

*&#42; uses [NYPL/ServiceNow](https://nyplprod.service-now.com) credentials for authentication*

## 3. Set up keys

* Having public key added/removed to appropriate `.authorized_keys` files on machines
  * If ensuring provisioning scripts that contain this key are updated / run
* Add user's public key to [NYPL/public_keys](https://github.com/NYPL/public_keys)
  * See that repo's README for offboarding instructions
