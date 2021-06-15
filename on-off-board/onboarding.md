# Onboarding

Welcome to NYPL Digital!

This document is intended to help developers become familiar with NYPL digital properties and standards.

## 1. Learn

- Review the [Contents](../README.md#contents) in the `engineering-general` repo.
  - Contains links to development standards and guidelines at NYPL.
- Review the [Useful Links](../other/README.md) in the `engineering-general` repo.
  - Contains links to documentation for various services, applications, and other products at NYPL.
- Review READMEs (or Wikis) in relevant repos
  - Generally, each repo will contain more app-specific information.

## 2. Set up accounts

### Commonly used accounts

A developer will generally need accounts for the following services:
- Slack
    - [nypl.slack.com](https://nypl.slack.com/)
- Github (Can use a personal account or make a new NYPL specific github account)
    - Github organizations:
        - [NYPL](https://github.com/NYPL)
        - [NYPL-discovery](https://github.com/NYPL-discovery)
        - [NYPL-Simplified](https://github.com/NYPL-Simplified)
    - Old and no-longer used organizations
        - [NYPL-registry](https://github.com/NYPL-registry)
        - [nypl-spacetime](https://github.com/nypl-spacetime)
        - [nypl-open-audio](https://github.com/nypl-openaudio)
        - [nypl-publicdomain](https://github.com/NYPL-publicdomain)
- JIRA*
    - [jira.nypl.org](https://jira.nypl.org/)
- [Docker Hub](https://hub.docker.com/u/nypl/)
- Amazon Web Services (AWS)
    - Primary AWS accounts (MFA Login):
        - [nypl-digital-dev](https://nypl-digital-dev.signin.aws.amazon.com/console)
- Bamboo*: Deployment happens via Bamboo 
    - [http://bamboo.nypl.org/](http://bamboo.nypl.org/)

### Less commonly used accounts

- NYPL Platform
    - [https://platform.nypl.org](https://platform.nypl.org)
- [npm organization](https://www.npmjs.com/org/nypl): You do not need an npm account to publish to npm 
- [Travis CI](https://travis-ci.com): Accounts are OAuthed and synced through Github. Adding/Removing access to Github controls access to Travis.
- Bitbucket: Older apps are on bitbucket
    - [bitbucket.org/NYPL](https://bitbucket.org/NYPL)
- Loggly
    - [https://nypl.loggly.com](https://nypl.loggly.com)
- CI Servers (e.g Jenkins instances)
    - [https://ci-sa.prod.aws.nypl.org](https://ci-sa.prod.aws.nypl.org)
- Optimizely
    - [https://app.optimizely.com](https://app.optimizely.com)
- Google Analytics
    - [https://analytics.google.com](https://analytics.google.com)
- Amazon Web Services (AWS)
    - Secondary AWS accounts (MFA Login):
        - [nypl-sandbox](https://nypl-sandbox.signin.aws.amazon.com/console)
        - [nypl/prod](https://nypl.signin.aws.amazon.com/console)
        - [nypl-dev](https://nypl-dev.signin.aws.amazon.com/console)
        - [nypl-labs](https://nypl-labs.signin.aws.amazon.com/console)
- Data Warehouse DB credential
    - [https://github.com/NYPL/data-warehouse#users](https://github.com/NYPL/data-warehouse#users)
- [New Relic](https://newrelic.com/) (Not currently used, just legacy for off-boarding)

*&#42; uses [NYPL/ServiceNow](https://nyplprod.service-now.com) credentials for authentication*

## 3. Set up keys

* Having public key added/removed to appropriate `.authorized_keys` files on machines
  * If ensuring provisioning scripts that contain this key are updated / run
* Add user's public key to [NYPL/public_keys](https://github.com/NYPL/public_keys)
  * See that repo's README for offboarding instructions
