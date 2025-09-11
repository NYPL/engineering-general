# Onboarding

Welcome to NYPL Digital!

This document is intended to help developers become familiar with NYPL digital properties and standards.

## Welcome & First Day

We hope that you'll have a good first day at NYPL Digital! Use this checklist to track your progress through the onboarding process.

---

## Day 1 Checklist

### Getting Started

- [ ] Meet your team and have a lunch or other meet-and-greet
- [ ] Get your laptop and set it up
- [ ] Receive your onboarding packet (first day, week, month and quarter plan)
- [ ] Start meeting with team members and collaborators to plan your work
- [ ] Choose a fun fact about yourself to share with NYPL and introduce yourself in the #introductions channel on Slack

### Essential Account Setup

- [ ] Set up password manager ([Keeper](https://keepersecurity.com) or [MacPass](https://macpassapp.org/))
- [ ] Configure multi-factor authentication (MFA)
- [ ] Request VPN access via [ServiceNow](https://nyplprod.service-now.com/nyplsp?id=sc_cat_item&sys_id=3ae790c0878db9006a42c74d19434d00)
- [ ] Access [Slack](https://nypl.slack.com/) and join relevant channels
- [ ] Set up GitHub account access (personal or NYPL-specific)

---

## Week 1 Checklist

### Learning & Documentation Review

- [ ] Review the [Digital Team Onboarding deck](https://docs.google.com/presentation/d/1LWD2qq5Ru5-1jYpd4HdZbNHym7ChDe-h/edit?usp=sharing&ouid=106215742869003313280&rtpof=true&sd=true)
- [ ] Explore the [Devops Confluence space](https://newyorkpubliclibrary.atlassian.net/wiki/spaces/DOPS/overview?homepageId=5963980)
- [ ] Explore the [Digital Confluence space](https://newyorkpubliclibrary.atlassian.net/wiki/spaces/DIGTL/overview?homepageId=153255944)
- [ ] Review [Peer Review Guidelines](../standards/peer-review.md)
- [ ] Review [Technical Approach Documents](../standards/technical-approach.md)
- [ ] Review the [Contents](../README.md#contents) of this repo
- [ ] Start a questions document for your 1:1s with your manager

### Account Setup Completion

- [ ] Access [JIRA](https://newyorkpubliclibrary.atlassian.net/) for ticket management
- [ ] Request AWS account access via [DevOps FAQ](https://newyorkpubliclibrary.atlassian.net/wiki/spaces/DOPS/pages/138346498/Frequently+Asked+Questions+FAQs#How-do-I-request-AWS-access%3F--How-do-I-rescind-AWS-access%3F)
- [ ] Join GitHub organizations:
  - [ ] [NYPL Main GitHub Organization](https://github.com/NYPL)
  - [ ] Team-specific organizations as needed ([NYPL-discovery](https://github.com/NYPL-discovery), [NYPL-Simplified](https://github.com/NYPL-Simplified))

### Essential Meetings

- [ ] Meet with your Manager
- [ ] Meet with your Project Manager
- [ ] Meet with your Product Manager
- [ ] Meet with engineering team members
- [ ] Meet with key stakeholders and non-Digital NYPL staff (if applicable)

### Repository Exploration

- [ ] Review READMEs/Wikis of repositories your team maintains
- [ ] Set up local dev environments for repositories you'll contribute to
- [ ] Schedule meetings with other engineers to understand current work status

---

## Month 1 Checklist

### AWS Account Access

Complete access setup for relevant AWS accounts (MFA required):

- [ ] [nypl](https://nypl.signin.aws.amazon.com/console) - Main production account
- [ ] [nypl-dev](https://nypl-dev.signin.aws.amazon.com/console) - Main QA/dev account
- [ ] [nypl-digital-dev](https://nypl-digital-dev.signin.aws.amazon.com/console) - Main account for LSP and DRB
- [ ] [nypl-sandbox](https://nypl-sandbox.signin.aws.amazon.com/console) - Dev/testing environment
- [ ] Other team-specific accounts as needed

### Additional Tool Access (As Needed)

- [ ] [NYPL Platform](https://platformdocs.nypl.org) - APIs for NYPL resources
- [ ] [New Relic](https://newrelic.com/) - Telemetry and monitoring
- [ ] [Google Analytics](https://analytics.google.com) - Analytics solution
- [ ] [Stash](https://stash.nypl.org/) - AWS configurations (requires VPN)
- [ ] [NPM Organization](https://www.npmjs.com/org/nypl) - If publishing packages

### Development Contributions

- [ ] Review open PRs to understand code standards
- [ ] Complete initial development tasks assigned by your manager
- [ ] Submit your first PR by end of first sprint
- [ ] Participate in code reviews

---

## Quick Reference

### Important Links

- **Slack**: [nypl.slack.com](https://nypl.slack.com/)
- **JIRA**: [newyorkpubliclibrary.atlassian.net](https://newyorkpubliclibrary.atlassian.net/)
- **VPN Request**: [ServiceNow Link](https://nyplprod.service-now.com/nyplsp?id=sc_cat_item&sys_id=3ae790c0878db9006a42c74d19434d00)
- **Password Sharing**: [PrivateBin](https://privatebin.nypl.org/)

### Key Confluence Spaces

- **DevOps**: [DOPS Space](https://newyorkpubliclibrary.atlassian.net/wiki/spaces/DOPS/overview?homepageId=5963980)
- **Digital**: [DIGTL Space](https://newyorkpubliclibrary.atlassian.net/wiki/spaces/DIGTL/overview?homepageId=153255944)

---

## Detailed Information

### Password Management

We **strongly** encourage team members to use a password manager for their credentials. There will be many passwords you need to track and the dangers of password reuse are real. We recommend one of the following password management tools:

For sharing credentials securely as a time-bound encrypted link (accessible only via VPN or onsite), use NYPL's open-source fork of ZeroBin: [PrivateBin](https://privatebin.nypl.org/)

- [Keeper](https://keepersecurity.com)
  - This is NYPL's approved password manager
  - To create a keeper account attempt to sign in with your `@nypl.org` email address, you should be prompted to request Admin approval.
- [MacPass](https://macpassapp.org/)
  - This is a local, open source, password management solution
  - It is not officially supported, but provides an easy place to track passwords

### Multi-Factor Authentication

Using multi-factor authentication (MFA) is also **strongly** encouraged at NYPL. For some accounts (most importantly AWS) it is **required**. There are several options for MFA:

- NYPL-supplied Yubi key. If you'd prefer a physical authentication key, please request one from your manager.
- MFA Application such as Duo or Microsoft Authenticator. These should be installed on your phone to support authentication.

### VPN Access

Some NYPL resources require VPN access. NYPL uses **OpenVPN Connect** for secure remote access.

- To request VPN access, please use the following ServiceNow link: [Request VPN Access in ServiceNow](https://nyplprod.service-now.com/nyplsp?id=sc_cat_item&sys_id=3ae790c0878db9006a42c74d19434d00)
- Once approved, you will receive instructions for installing and configuring OpenVPN Connect on your device.

If you have any issues with VPN setup, contact IT support or your manager for assistance.

### Learning Resources

There is a lot to learn in Digital, and there is no way to pick everything up in your first month, let alone your first day! So here are some tips for starting the process of learning the whats, wheres, hows and whys of our department.

**Key Documentation to Review:**

- [Digital Team Onboarding deck](https://docs.google.com/presentation/d/1LWD2qq5Ru5-1jYpd4HdZbNHym7ChDe-h/edit?usp=sharing&ouid=106215742869003313280&rtpof=true&sd=true)
- [Devops Confluence space](https://newyorkpubliclibrary.atlassian.net/wiki/spaces/DOPS/overview?homepageId=5963980) for documentation on infrastructure, deployment, and operations
- [Digital Confluence space](https://newyorkpubliclibrary.atlassian.net/wiki/spaces/DIGTL/overview?homepageId=153255944) for documentation on Digital team processes, projects, and resources
- [Peer Review Guidelines](../standards/peer-review.md) and [Technical Approach Documents](../standards/technical-approach.md) for current engineering practices
- [Contents](../README.md#contents) of this repo
- READMEs (or Wikis) of the repositories your team maintains

**Learning Tips:**

- Your manager and onboarding buddy should help give you context for repositories
- A good approach is to spin up local dev environments for any repositories you'll be contributing to
- Set up meetings with other engineers on your team to get a sense for the status of the team's work and where you can help contribute
- Ask questions! Start a document with questions and things that were unclear - this should be an important part of your early 1:1s with your manager
- We want to use these questions to improve our documentation and processes! Fresh eyes often see things that we miss

### Initial Tasks Philosophy

We strive to design an initial set of tickets/tasks for new team members that both allow them to begin exploring codebases as well as making impactful contributions early in their time in Digital. We are not a "deploy to production on Day 1" shop, but aim to have new engineers putting up PRs by the end of their first sprint.

Please discuss your initial set of tasks with your manager and new team. Our goals generally are:

**Codebase Exploration Tasks:**

- Extending unit test coverage
- Refactoring a specific class/module to align with a larger codebase
- Implementing a new linting, CI/CD or other quality-of-life tool

**Standards Understanding Tasks:**

- Reviewing open PRs
- Implementing specific code quality changes on a small codebase
- Refactoring an application to a new version of its current tech stack
- Anything that you and your manager decide!

---

## Less Commonly Used Accounts

The following accounts may be needed depending on your team and role:

- [Docker Hub](https://hub.docker.com/u/nypl/) - Used for publicly distributed images. Internal images are hosted on AWS ECR
- [Adobe Analytics](https://experience.adobe.com) - Largely deprecated in favor of GA
- [Stash](https://stash.nypl.org/) - (NYPL VPN needed) IT and devops keep AWS configurations here
- [Bitbucket](https://bitbucket.org/NYPL) - Host for older git repositories
- [TravisCI](https://travis-ci.com) - Used for some CI/CD Pipelines, largely deprecated in favor of GitHub Actions
- [Bamboo](http://bamboo.nypl.org/) - Used for some CI/CD workflows, largely deprecated in favor of GitHub Actions
- [Loggly](https://nypl.loggly.com) - Largely deprecated in favor of NewRelic and AWS CloudWatch
