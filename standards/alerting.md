# Monitoring & Alarms

All services, applications, and consumers MUST have a [CloudWatch Alarm](http://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) set up,

Multiple alarms MAY be set up.

Owners SHOULD identify and monitor other key success metrics.

## Alarm Triggers

### Log Messages

All services, applications, and consumers MUST create a metric filter for their [log messages](logging.md) of severity `ERROR` and greater. 

The metric filter MUST be named and namespaced consistently:

- The namespace MUST be `LogMetrics`.
- The name MUST be in upper camel case and MUST be prefixed with the component name. For example: `BibServiceError`.

The RECOMMENDED search for a metric filter is `{ $.levelCode <= 3 }`.

The metric created from the metric filter MUST be used to trigger an alarm. 

### Other Alarms

Additional alarms MAY be set up for other metrics. For example: 

- HTTP errors (5xx, 4xx status codes)
- Lambda errors
- Kinesis errors

### Alarm Configuration

#### SNS Topic

The SNS topic SHOULD be setup before creating an alarm.

The SNS topic MUST be named consistently and SHOULD be reused for all the component alarms.

- The name MUST be in upper camel case and MUST be prefixed with the component name. For example: `BibServiceErrorAlarm`.

The SNS topic SHOULD notify the component owner(s) by email or other method.

#### Alarm Setup

Alarms MUST be named consistently:

- The name MUST be in upper camel case and MUST be prefixed with the component name. For example: `BibServiceErrorAlarm`.

Alarms SHOULD generally use the *sum* of a metric to trigger an alarm.
 
Alarms SHOULD notify a SNS topic when triggered.

Alarms SHOULD be added to an alarms dashboard.
