# Documentation Standards

All coding projects MUST include and maintain minimum documentation standards.

## Minimum Standards

Applications MUST include a README

## README Standards

README documents MUST be written in a format accepted by the code
repository supported with the application.

README documents MUST contain the following sections:

- Name
- Summary/Purpose
- Requirements
    - Version numbers MUST be included for all software requirements
- Dependencies
    - Version numbers MUST be included for all software dependencies
- Installation information MUST be provided
- Usage examples are RECOMMENDED
- Testing instructions MUST be provided as specified [here](test-coverage.md).

### Optional README sections/additions

- SHOULD include current, stable version information
- SHOULD describe git workflow, including if branches map to certain environments.  
  As an example, see [NYPL/scsb_item_updater's 'Git Workflow & Deployment Section'](https://github.com/NYPL-discovery/scsb_item_updater#git-workflow--deployment)
- SHOULD include instructions about deployment.
- SHOULD include any configuration information, if necessary
- MAY include example usage
- MAY include contributing guidelines
- MAY include badges for:
    - tests/build
    - code coverage
    - stable/unstable version
    - standards compliance (CSS, HTML, etc.)
    - license type
- MAY include ASCII art

### API Documentation

- APIs MUST provide Swagger v2 documentation
- It is RECOMMENDED that APIs provide wiki-style (or similar) additional
documentation.


### CHANGELOG

- Applications SHOULD provide a CHANGELOG for all versioned code.

### Architectural Diagrams

- Applications MAY provide architectural diagrams

### Workflow

- Applications MAY provide workflow documents in formats such as
[Unified Modeling Language (UML)](http://www.uml.org).


## Commit Messages
To tie a GitHub commit message to a Jira ticket, use the 
    git commit -m 'ABC-123 #comment Your comment goes here'
format, where ABC-123 points to the Jira issue your code commit is addressing.  For this to work, the email address you use for your GitHub commits needs to be the same as the address you use for Jira.



