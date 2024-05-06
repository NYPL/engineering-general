# Onboarding

Welcome to NYPL Digital!

This document is intended to help developers become familiar with NYPL digital properties and standards.

## Welcome & First Day

We hope that you'll have a good first at NYPL Digital! Generally 4 things should happen your first day:

1. You'll meet your team and have a lunch or other meet-and-greet
2. You'll get your laptop and have some time to set it up
3. You'll be given an onboarding packet that lays out your first day, week, month and quarter
4. You'll start meeting with your team members and collaborators to start planning your work

After that your intro will vary depending on your team and role, but it should focus at least in these areas

## 1. Learning

There is a lot to learn in Digital, and there is no way to pick everything up in your first month, let alone your first day! So here are some tips for starting the process of learning the whats, wheres, hows and whys of our department.

- Review the [Contents](../README.md#contents) of this repo.
- Review READMEs (or Wikis) of the repositories your team maintains
  - Your manager and onboarding buddy should help give you context for them
  - A good approach is to spin up local dev environments for any repositories you'll be contributing to.
- Set up meetings with other engineers on your team to get a sense for the status of the team's work and where you can help contribute!
- Review the documents and initial tasks outlined in the specific onboarding documents provided to you on your first day (Which is probably how you ended up here!)
- Ask questions. If your manager did not ask you to do this already: start a document with questions and things that were unclear!
  - This document should be an important part of your early 1:1s with your manager
  - We want to use these questions to improve our documentation and processes! Fresh eyes often see things that we miss

## 2. Account Setup

### Password Management

We __strongly__ encourage team members to use a password manager for their credentials. There will be many passwords you need to track and the dangers of password reuse are real. We recommend one of the following password management tools:

- [Keeper](https://keepersecurity.com)
  - This is NYPL's approved password manager
  - To create a keeper account attempt to sign in with your `@nypl.org` email address, you should be prompted to request Admin approval.
- [MacPass](https://macpassapp.org/)
  - This is a local, open source, password management solution
  - It is not officially supported, but provides an easy place to track passwords

### Commonly used accounts

A developer will generally need accounts for the following services. Most of these accounts will be configured for you during onboarding, please request access for any systems you do not have access to.

- [Slack](https://nypl.slack.com/) Preferred method of communication
- GitHub (Can use a personal account or make a new NYPL specific GitHub account)
  - [NYPL Main GitHub Organization](https://github.com/NYPL)
  - See [GitHub Organization Management](./github-org-management.md) for onboarding steps.
  - We ask that all members have a username that contains their name somewhere. If you do not want to update your personal Github account, we encourage you to make an NYPL-specific account!
  - Team-specific organizations
    - [NYPL-discovery](https://github.com/NYPL-discovery)
    - [NYPL-Simplified](https://github.com/NYPL-Simplified)
  - Old and/or unused organizations
    - [NYPL-registry](https://github.com/NYPL-registry)
    - [nypl-spacetime](https://github.com/nypl-spacetime)
    - [nypl-open-audio](https://github.com/nypl-openaudio)
    - [nypl-publicdomain](https://github.com/NYPL-publicdomain)
- [JIRA](https://jira.nypl.org/) Ticket Management & Tracking
- Amazon Web Services (AWS) Accounts (MFA login required)
  - [nypl](https://nypl.signin.aws.amazon.com/console) Main production account
  - [nypl-dev](https://nypl-dev.signin.aws.amazon.com/console) Main QA/dev account
  - [nypl-digital-dev](https://nypl-digital-dev.signin.aws.amazon.com/console) Main account for LSP and DRB
  - [nypl-sandbox](https://nypl-sandbox.signin.aws.amazon.com/console) Dev/testing environment
  - [nypl-labs](https://nypl-labs.signin.aws.amazon.com/console) Hosting old projects
  - Other accounts are in use by different teams. Speak with team leadership for details

### Less commonly used accounts

- [NYPL Platform](https://platformdocs.nypl.org) Assorted APIs for interacting with NYPL resources
- [NPM Organization](https://www.npmjs.com/org/nypl) (NOTE: You do not need an npm account to publish to npm)
- [New Relic](https://newrelic.com/) Telemetry, metrics and monitoring
- [Docker Hub](https://hub.docker.com/u/nypl/) Used for publically distributed images. Internal images are hosted on AWS ECR
- Analytics
  - [Adobe Analytics](https://experience.adobe.com) NYPL's main analytics solution
  - [Google Analytics](https://analytics.google.com) Largely deprecated in favor of AA, with specific exceptions 
- Repository Management
  - [Stash](https://stash.nypl.org/) (NYPL VPN needed) IT and devops keep AWS configurations, among other things, here.
  - [Bitbucket](https://bitbucket.org/NYPL) Host for older git repositories
- CI/CD
  - [TravisCI](https://travis-ci.com) Used for some CI/CD Pipelines, largely deprecated in favor of GitHub Actions
  - [Bamboo](http://bamboo.nypl.org/) Used for some CI/CD workflows, largely deprecated in favor of GitHub Actions
- [Loggly](https://nypl.loggly.com) Largely deprecated in favor of NewRelic and AWS CloudWatch

## 3. Initial Meetings

Your manager should set up an initial set of meetings with both team members and other Digital members you will be working with. If, at the end of your first or second week, some of these meetings haven't happened, you should reach out and schedule them! Or ask your manager to do so. You should at least have met with these people:

- Your Manager
- Your Project Manager
- Your Product Manager
- Various members of your engineering team
- Key stakeholders and non-Digital NYPL staff (if applicable)

## 4. Initial Tasks

We strive to design an initial set of tickets/tasks for new team members that both allow them to begin exploring codebases tktk
