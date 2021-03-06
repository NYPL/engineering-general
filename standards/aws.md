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
AWS profile name format MUST be in kebab-case/dasherized.

The profile name SHOULD be one of the following:

- `Account ID`

- `Alias`

Examples: `nypl-digital-dev`, `nypl-sandbox`, `nypl`

### Metrics

See [Monitoring & Alarms](../standards/alerting.md)

### Alarms

See [Monitoring & Alarms](../standards/alerting.md)

### SQS

#### Naming

Queues MUST be named in a way that describes:

1.  _What_ is is the queue.
2.  _Where_ the destination is for these records.

The _What_ and the _Where_ SHOULD be separated by the word "for", unless
it's awkward grammatically.   
Finally, the queue name MUST be suffixed with
the environment name.

e.g. `user-profile-updates-for-sierra-development` tells us:

1. The queue contains records that represent a user's profile update.
2. The records will be sent to sierra.
3. It is the `development` environment.

#### Documenting

Queues should be documented in https://github.com/NYPL/aws.

## Repository Names

Repository names MUST be written with `lower snake case` where the delimiter is a hyphen ("-") or an underscore ("\_") character.

## Code

There MAY be language-specific conventions developers will implement.

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