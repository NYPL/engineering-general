# Logging

## Format

The message format MUST be JSON.

The message MUST contain the following top-level keys: `level`, `message`:

- `level` MUST be a **case-sensitive string** of one of the following values & MUST follow this order of severity (from least to greatest): `DEBUG`, `INFO`, `NOTICE`, `WARNING`, `ERROR`, `CRITICAL`, `ALERT`, or `EMERGENCY`.

- `message` MUST be a **string** and SHOULD contain a message useful for debugging/error reporting.

The message MAY also contain the following top-level keys:

- `levelCode` MUST be a **integer** and correspond to the log `level`:

| levelCode      | Level          |
| :------------- | :------------- |
| 7              | DEBUG          |
| 6              | INFO           |
| 5              | NOTICE         |
| 4              | WARNING        |
| 3              | ERROR          |
| 2              | CRITICAL       |
| 1              | ALERT          |
| 0              | EMERGENCY      |

Additional key/values of any type MAY be included and MUST NOT break functionality.

## Aggregation

Any logging MUST be sent to CloudWatch.

Services built prior to this standard, MAY send logs to another aggregation service like Loggly.

## Metrics & Exception Notification

We SHOULD use log parsing for generating metrics & exception notification.  
**A severity of `ERROR` & above means human beings MUST be [notified](alerting.md).**

## Rotation

If an app writes logs to disk, those files MUST be rotated.
If the logging library doesn't support this natively - than it should use [logrotate](https://linux.die.net/man/8/logrotate).
