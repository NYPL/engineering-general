# Naming Conventions

As part of the NYPL Engineering team, proper naming delivers clarity and consistency amongst our code, applications, services, consumers and more. The following sections will detail examples on how we (NYPL Engineering), agree on a standard for naming.

Establishing proper naming will help each developer by:
- Reducing the effort needed to read and understand source code

- Enabling code reviews to focus on more important issues than arguing over syntax and naming standards

- Enabling code quality review tools to focus their reporting mainly on significant issues other than syntax and style preferences

## Table of Contents

- [Naming Conventions](#naming-conventions)
  * Identifiers
    + [Readability](#readability)
    + [Multiple Words versus Single Word](#multiple-words-versus-single-word)
    + [Length of Identifiers](#length-of-identifiers)
  * AWS
    + [Lambdas](#lambdas)
    + [Metrics](#metrics)
    + [Alarms](#alarms)
  * [Repository Names](#repository-names)
  * [Code](#code)
    + [Camel Case](#camel-case)
    + [Snake Case](#snake-case)

## Identifiers

### Readability

Developers MUST make their naming declarations readable.

Well-chosen identifiers make it significantly easier for developers to understand what the codebase is doing or extend the source code to apply for new needs.

### Multiple Words versus Single Word

Developers MUST use "meaningful identifiers". A single word may not be as meaningful, or specific, as multiple words.

### Length of Identifiers

Developers SHOULD avoid the following issues that may arise by:

- declaring extremely short identifiers. For example, using 'i' or 'j' make it very difficult to uniquely distinguish using automated search and replace tools
- declaring longer identifiers may be preferred because short identifiers cannot encode enough information or appear too cryptic
- extremely long identifiers may be disfavored because of visual clutter

Developers SHOULD find the right balance as long as readability, clarity and meaning is accomplished.

## AWS

### Lambdas

AWS Lambda functions MUST be in upper camel case and MUST be suffixed with the development environment string to include a `-` (dash) separator.

A correct example would be `BibService-development` or `HoldRequestResultConsumer-qa` or `HoldService-production`.

An incorrect example would be `ItemService-dev`. Although it uses upper camel case format for the service name, it fails to establish the correct development environment suffix.

All development environment strings MUST adhere to one of three allowable types:

- `-development`

- `-qa`

- `-production`

### Profile Names
AWS profile name format MUST be in lower snake case, delimited by a hyphen ("-").

The profile name SHOULD be one of the following:

- `Account ID`

- `Alias`

Examples: `nypl-digital-dev`, `nypl-sandbox`, `nypl`

### Metrics

See [Monitoring & Alarms](../standards/alerting.md)

### Alarms

See [Monitoring & Alarms](../standards/alerting.md)

## Repository Names

Repository names MUST be written with `lower snake case` where the delimiter is a hyphen ("-") or an underscore ("\_") character.

## Code

There MAY be language specific conventions developers will implement.

Each team/developer MUST adhere to one of the allowable formats:

### Camel Case

Letter-case separated words will create boundaries using medial capitalization.

- UpperCamelCase
  - ex: `SearchResultsController`

- lowerCamelCase
  - ex: `getPatronId`

### Snake Case

Delimit separate words with a non-alphanumeric character.

The two characters commonly used for this purpose are the hyphen ("-") and the underscore ("\_").

- lower_snake_case
  - ex: `get_job_id`

- Upper_Snake_Case
  - ex: `Get_Hold_Request_Id`

- ALL_UPPER_SNAKE_CASE
  - ex: `SERVICE_API_URL`

As long as the team/developer is consistent across their codebase, the selection of what format relies on the team/developer.
