# Using AWS Tags

[Amazon's documentation](https://aws.amazon.com/answers/account-management/aws-tagging-strategies/) describes tags as:

 >...a simple label consisting of a customer-defined key and an optional value that can make it easier to manage, search for, and filter resources. Although there are no inherent types of tags, they enable customers to categorize resources by purpose, owner, environment, or other criteria.

Using tags helps us identify stakeholders as well as track critical financial metrics
about our AWS usage. You MUST add Amazon tags to services when they are available.

## Required Tags

| Key           | Description                                                                 |
|:--------------|:----------------------------------------------------------------------------|
| Project       | The primary project this resource is being used for, or "UnknownProject".   |
| OtherProjects | Any other projects that rely on the resource being up ('/'-separated list). |
| Environment   | `production`, `qa`, `UnknownEnvironment`, `development`                     |


### Project Tags In Use

Every effort SHOULD be made to maintain uniform capitalization when creating new
tags using existing values;

* DAM
* DXP
* LSP
* NA
* Shared
* SimplyE

## Resources / More Reading

-   [Use Tagging to Organize Your Environment and Drive Accountability](https://docs.aws.amazon.com/whitepapers/latest/cost-optimization-laying-the-foundation/tagging.html)

-   [Manage Tags](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tagging-resources.html)
