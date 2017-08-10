# Monitoring & Alarms

All components MUST have an alarm set up.

Components MAY have multiple alarms.

Owners SHOULD identify and monitor other key success metrics.

## Alarm Triggers

### Log Messages

A service MUST create a metric filter for [log messages](logging.md) of severity `ERROR` and greater. 

The metric filter MUST be named and namespaced consistently:

- The namespace MUST be `Log Message`
- The name MUST be in upper camel case and MUST be prefixed with the component name. For example: `BibServiceLogError`.

The RECOMMENDED search for a metric filter is `{ $.levelCode <= 3 }`.

The metric created from the metric filter MUST be used to trigger an alarm. 
Other Alarms

Additional alarms MAY be set up for other metrics. For example: 

- HTTP errors (5xx, 4xx status codes)
- Lambda errors
- Kinesis errors

### Alarm Configuration

Alarms MUST be named consistently:

- The name MUST be in upper camel case and MUST be prefixed with the component name. For example: `BibServiceLogAlarm`.

Alarms SHOULD notify a SNS topic when triggered.

The SNS topic MUST be named consistently and SHOULD be reused for all the component alarms.

- The name MUST be in upper camel case and MUST be prefixed with the component name. For example: `BibServiceAlarmNotification`.

The SNS topic SHOULD notify the component owner(s) by email or other means.

Alarms SHOULD be added to an alarms dashboard.
