# Delivery locations failed to display in Shared Collection Catalog

## 1. Incident Date
 - Discovered: Sept 3, 2019
 - Thought to have occurred: Aug 31, 2019

## 2. Incident Summary
 - On Saturday, Aug 31 at 10:27am Eastern all indexes in the discovery-api production ES domain disappeared. Following disappearance, the DiscoveryApiIndexer proceeded to write to the configured index "resources-2018-04-09", meaning documents accumulated in a new index without any mappings. When the issue was discovered, the new index had acquired a little over 100k documents.

## 3. Authors
 - Paul Beaudoin

## 4. Timeline
 - Aug 31 8:49am: Environmental health on discovery-api-production jumps from Ok to Degraded. It bounces between Degraded, Warning, and Ok dramatically dozens of times over the next couple hours.
 - Some time before Aug 31 10:27am: All indexes deleted. We know they were deleted at this point because that's the creation timestamp on the 'resources-2018-04-09' index
 - Aug 31 10:27am: 'resources-2018-04-09' is created due to an item/bib update triggering an event in the `IndexDocument-production` stream
 - Sept 3, 4:26pm: Melanie Locay via Mellisa Gasparato report SCC isn't working
 - Sept 3, 10:18pm: Paul Beaudoin builds a new index with correct mappings and uses logstash to copy 300k documents into it as new temporary index backing DiscoveryApi. Also disables the `IndexDocument-production` trigger on the `DiscoveryIndexPoster-production` lambda because it wasn't writing useful documents anyway due to missing field mapping.
 - Sept 3 10:41:56pm: Paul configures discover-api EB to use newly created 'resources-2019-09-03' because it now has the correct field mapping and *more* data than 'resources-2018-04-09'
 - Sept 3, 11:11pm: Paul Beaudoin restores 'resources-2018-04-09' from an automated backup (which takes ~5mins)
 - Sept 3 11:19: Paul configures discover-api EB to use restored 'resources-2019-04-09'

## 5. Root Cause

It's unclear what exactly deleted the indexes..

One explanation is that someone or some process found our [rather public ES domains](https://github.com/NYPL-discovery/discovery-api/blob/88159e60212fb96b9494695c5462722b75d89466/config/production.env#L3) and issued a `DELETE` on `/_all` from an allowed IP. At the time of the incident, the production ES domain was [protected by an access policy](https://github.com/NYPL/aws/blob/b5c0af0ec8357af9a645d8b47a5dbb0090966071/common/elasticsearch.md#2-make-the-domain-public-restrict-by-ip) that restricted access to `[NAT Gateway IP]` and `[SASB IP Block]/24` (actual IPs redacted) . The former is the NAT Gateway IP for all resources launched inside the production vpc, effectively allowing access to the DiscoveryIndexPoster-production lambda and discovery-api-production EB deployment. The latter matches all traffic in SASB (and perhaps beyond). Use of `[SASB IP Block]/24` to enable direct access was reckless because it covers wired connections at SASB as well as computers connecting over the public "NYPL" wifi. Although the building was closed at the time the incident is thought to have occurred, the broadcast range may have allowed one access from the front steps of the building and/or parts of Bryant Park.

Another possible cause may be an hardware or software issue. The domain uses two nodes. Under Instance Health, there are six Data Instances:
   * Elasticsearch-EjrqmHyDS-qK0MJvH9A2Mg: went quiet on Aug 31 at/after 9:00am
   * Elasticsearch-u3AewBjlSD2rwrPdRbI_yg: went quiet on Aug 31 at/after 8:00am
   * Elasticsearch-xWtfBlWnQiG3kYR1b5qYUw: live from Aug 31 10am to 9.03 8pm
   * Elasticsearch--67y18NIR8SGpGfWFzgcPQ: [ditto above]
   * Elasticsearch-zigD5d_8SbmTKCvN9bPozA: live from 9.03 8pm to current
   * Elasticsearch-7ticgp4RRgiJBirouz8fFA: [ditto above]

I don't know what causes data nodes to be retired and replaced. It's suspect that two new nodes were activated about an hour before the outage. It seems possible that a routine process to swap in new nodes simply failed to initialize them with the right data. It's also curious that two new nodes were activated at 8pm on 9.03. I believe this coincides with [enabling](https://console.aws.amazon.com/es/home?region=us-east-1#domain:resource=discovery-api-production;action=dashboard) the [error logs](https://console.aws.amazon.com/cloudwatch/home?region=us-east-1#logEventViewer:group=/aws/aes/domains/discovery-api-production/application-logs) for the domain. Shortly after that was enabled, I see log entries containing "failed to connect to node {-67y18N}" and "failed to connect to node {xWtfBlW}{xWtfBlWnQiG3kYR1b5qYUw..." suggesting those nodes' health degraded, causing them to be swapped. The reason for the degradation could have been the shere number of failed queries hitting the index (due to absense of a field mapping) or could be a side effect of enabling logging. In any case, the nodes created on 9.03 at 8pm to replace the failed nodes have remained without being swapped out (including during the brief period on Sep 3 from about 8pm to 10:41pm when the DiscoveryApi EB continued to send failing queries to the old index, which troubles the theory that it was the queries themselves that destabalized the nodes).

No existing alarm was triggered until work began to fix it. Our "DiscoveryApiErrorAlarm" monitors metric filter [DiscoveryApiError](https://console.aws.amazon.com/cloudwatch/home?region=us-east-1#metricFilter:group=/aws/elasticbeanstalk/discovery-api-production/var/app/current/log/discovery-api.log), which looks for `{ $.level = "ERROR" }` in cloudwatch log `/aws/elasticbeanstalk/discovery-api-production/var/app/current/log/discovery-api.log`. It was not thrown, suggesting the app itself is not throwing enough error-level logs when it encounters issues (or perhaps doesn't adequately identify issues as such).

## 6. Resolution and Recovery
 - The 'resources-2018-04-09' index was restored by following [AWS instructions](https://docs.aws.amazon.com/elasticsearch-service/latest/developerguide/es-managedomains-snapshots.html). Specifically:
   - A `GET` was sent to `/_snapshot/cs-automated/_all?pretty` to retrieve a listing of all available automated backups. (`cs-auomated` is the S3 bucket for automated backups.)
   - The list of backups was reviewed to find the instance taken immediately before the outage.
   - A `POST` was sent to `/_snapshot/cs-automated/2019-08-31t12-30-51.02246626-37bc-4c84-92d9-705cd34f85e7/_restore` with body `{"indices": "resources-2018-04-09"}` and `Content-Type: application/json` via Postman
   - The immediate response was `{ "accepted": true }`
   - If the task was trackable in `/_tasks?` I didn't see it. It completed in about 5 minutes.
 - Once the backup restore was confirmed, I re-enabled the DiscoveryApi EB to use the 'resources-2018-04-09' index and reenabled the `DiscoveryIndexPoster-production` lambda.
 - Removed `[SASB IP Block]/24` from list of allowed IPs on the production domain's access policy, effectively limiting traffic to resources inside the VPC.

## 7. Preventative Measures
 - Added [DiscoveryApiHealthDegraded](https://console.aws.amazon.com/cloudwatch/home?region=us-east-1#alarmsV2:alarm/DiscoveryApiProductionHealthDegraded) alarm, which notifies "DiscoveryApiErrorAlarm" topic when health transitions to "Degraded" or worse (and back again). It seems important to leverage EB's monitoring to detect issues *as well as* monitor app error logging (which depends on the app having traffic and logging errors)
 - Drafted [documentation about how ES permissions are managed](https://github.com/NYPL/aws/pull/14)
