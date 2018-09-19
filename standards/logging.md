# Logging

## Format

The message format MUST be JSON.

The message MUST contain the top-level keys:

| key            | type                 | note
| :------------- | :-------------       | :-------------
| level          | case-sensitive string| MUST follow this order of severity (from least to greatest): `VERBOSE`, `DEBUG`, `INFO`, `NOTICE`, `WARNING`, `ERROR`, `CRITICAL`, `ALERT`, or `EMERGENCY`
| message        | string               |SHOULD contain a message useful for debugging/error reporting.
| timestamp      | string               |MUST be formatted as [iso8601](https://en.wikipedia.org/wiki/ISO_8601), (e.g. "2017-08-01T18:41:09.707Z")

The message MAY also contain the following top-level keys:

- `levelCode` MUST be a **integer** and correspond to the log `level`:

| levelCode      | Level          |
| :------------- | :------------- |
| 8              | VERBOSE        |
| 7              | DEBUG          |
| 6              | INFO           |
| 5              | NOTICE         |
| 4              | WARNING        |
| 3              | ERROR          |
| 2              | CRITICAL       |
| 1              | ALERT          |
| 0              | EMERGENCY      |

Additional key/values of any type MAY be included and MUST NOT break functionality.

Developers SHOULD be aware of message size limits to prevent malformed JSON. For example, CloudWatch [truncates log messages](http://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/cloudwatch_limits_cwl.html) to 256 KB.

## Aggregation

Any logging MUST be sent to CloudWatch.

Services built prior to this standard, MAY send logs to another aggregation service like Loggly.

## Metrics & Exception Notification

We SHOULD use log parsing for generating metrics & exception notification.  
**A severity of `ERROR` & above means human beings MUST be [notified](alerting.md).**

## Rotation

If an app writes logs to disk, those files MUST be rotated.
If the logging library doesn't support this natively - than it should use [logrotate](https://linux.die.net/man/8/logrotate).
