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

#### How to Set up a Metric

1. Log in the [AWS service](https://aws.amazon.com/console/) with your credentials.

2. Go to `CloudWatch` by clicking `Services` dropdown menu from the top navigation and choose `CloudWatch`.

3. Go to `Logs` from the left navigation and find the log you want to build the meric on from the log list.

4. Click the left circle of the log, and then go up to the top of the log list, click `Create Metric Filter`.

5. In `Define Logs Metric Filter` page, enter the filter you like in `Filter Pattern` field, such as `{ $.levelCode <= 3 }`. Then click `Assign Metric`.

6. In `Create Metric Filter and Assign a Metric` page, enter your filter and metic names based on the conventions from the previous paragraph. Also, notice that all the customized metrics should be assigned in the `Metric Namespace` of `LogMetrics`. Click _Create Filter_ it is done.

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

##### How to Set up a SNS Topic

1. Click `Services` dropdown menu from the top navigation and choose `Simple Notification Service` under the category of `Messaging`.

2. Click `Create topic` on the page, and named your topic following the naming conventions from the previous paragraph. And then create the topic.

3. You should be on `Topic details` page now. In `Subscription` section, click `Create subscription`. In the `Protocol` dropdown menu, choose the method you want to recieve the notification, generally we use `Email.` Then, in the `Endpoint` field, enter the email address. Finally, click `Create subscription`.

#### Alarm Setup

Alarms MUST be named consistently:

- The name MUST be in upper camel case and MUST be prefixed with the component name. For example: `BibServiceErrorAlarm`.

Alarms SHOULD generally use the *sum* of a metric to trigger an alarm.
 
Alarms SHOULD notify a SNS topic when triggered.

Alarms SHOULD be added to an alarms dashboard.
