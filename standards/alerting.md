# Monitoring & Alarms

All services, applications, and consumers MUST have a [CloudWatch Alarm](http://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) set up,

Multiple alarms MAY be set up.

Owners SHOULD identify and monitor other key success metrics.

Alarms SHOULD be tested as part of the [Production Readiness](production-readiness.md) process.

## Alarm Triggers

### Log Messages

All services, applications, and consumers MUST create a metric filter for their [log messages](logging.md) of severity `ERROR` and greater. 

The metric filter MUST be named and namespaced consistently:

- The namespace MUST be `LogMetrics`.
- The name MUST be in upper camel case and MUST be prefixed with the component name. For example: `BibServiceError`.

The RECOMMENDED search for a metric filter is `{ $.levelCode <= 3 }`.

The metric created from the metric filter MUST be used to trigger an alarm.

#### How to Set up a Metric

1. Log in the [AWS Service](https://aws.amazon.com/console/) with your credentials.

2. Go to `CloudWatch` by clicking `Services` dropdown menu from the top navigation and choose `CloudWatch`.

3. Go to `Logs` from the left navigation and find the log you want to build the meric on from the `Log Groups` list.

4. Click the left circle of the log, and then go up to the top of the list, click `Create Metric Filter`.

5. In `Define Logs Metric Filter` page, enter the filter you like in `Filter Pattern` field, such as `{ $.levelCode <= 3 }`. More details for `Filter Pattern`, see [here](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/FilterAndPatternSyntax.html). Then click `Assign Metric`.

6. In `Create Metric Filter and Assign a Metric` page, enter your filter name and metric name based on the conventions from the previous paragraph. Also, notice that all the customized metrics SHOULD be assigned in the `Metric Namespace` of `LogMetrics`. Click _Create Filter_ to finish creating the metric.

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

2. Click `Create topic` on the page, and name your topic following the naming conventions from the previous paragraph. And then create the topic.

3. You should be on `Topic details` page now. In `Subscription` section, click `Create subscription`. In the `Protocol` dropdown menu, choose the method you want to recieve the notifications. Generally we use `Email.` Then, in the `Endpoint` field, enter your email address. Finally, click `Create subscription`.

#### Alarm

Alarms MUST be named consistently:

- The name MUST be in upper camel case and MUST be prefixed with the component name. For example: `BibServiceErrorAlarm`.

Alarms SHOULD generally use the *sum* of a metric to trigger an alarm.
 
Alarms SHOULD notify a SNS topic when triggered.

Alarms SHOULD be added to an alarms dashboard.

##### How to Set up an Alarm

1. You SHOULD set up a SNS Topic before you set up the alarm, so the alarm will have the place to go.

2. Go to `CloudWatch` by clicking `Services` dropdown menu from the top navigation and choose `CloudWatch`.

3. If it is your first alarm of the metric, a big chance you might not have any logs in the metric yet, thus you will not be able to see the metric by searching it. To set up the alarm on it, go to `Logs` from the left navigation. And find the log that has your metric from `Log Groups`.

4. On the log, you will find that it indicates how many filters it has on `Metric Filters` column. Click the link such as `1 filter`.

5. Now you will be on the page that has all the filters the log has. On the filter you want, you can find a link to `Create Alarm` on the top right corner of the filter block.

6. In the pop-up `Create Alarm` window, first enter the name and the threshold of the alarm under `Alarm Threshold` section. The name SHOULD follow the naming conventions. In `Whenever` section, `is:` is usually set up to greater and equal to 1.

7. In `Additional settings` section, set `Treat missing data as:` as good.

8. In `Actions` section, set `Whenever this alarm:` as `State is ALARM`, and `Send notification to:` as the SNS Topic you have already created.

9. In `Alarm Preview` section, choose your preferred period yet the Statistic SHOULD be `Standard` and `Sum`.

10. Click `Create Alarm` to finish it.
