# No Bib/Item Platform Updates For 3 Days

1. Incident Date
   - March 30, 2018
2. Incident Summary
   - On March 27, 2018 at ~2:55pm, bib/item updates from Sierra stopped propagating to our Platform.
   - It was discovered on March 30, 2018 at ~11:00am (almost 3 days later) that the primary Sierra API key used by our Platform services was accidently deleted.
3. Author(s)
   - Kevin Friedman
4. Timeline
   - On March 30, 2018 at ~11:00am, it was noticed that there were no bib/item updates reported on our dashboard (:+1: for dashboards!).
   - Upon checking CloudWatch, it was discovered that were virtually no updates posted since March 27, 2018 at ~2:55pm.
   - After checking the CloudWatch logs from the bib/item pollers (which were logging great :smile:), it was discovered that there was an authentication error retrieving an access token from the Sierra API.
   - It was confirmed that the Sierra API key used by our Platform services was deleted.
   - A new Sierra API key was issued and installed on appropriate services.
   - Normal service resumed by March 30, 2018 at ~12:30pm.
5. Root Causes
   - The Sierra API key used by our Platform was accidentally deleted.
   - Alarms were improperly configured.
        - The metric filter was being generated from the wrong log group `web-1.error.log`.
        - It _should_ have been generated from `web-1.log`.
6. Resolution and Recovery
   - A new Sierra API Key was issued and saved in Parameter Store.
   - Alarms were re-configured based off the correct metric filter.
7. Preventative Measures
   - When used by services, Sierra API keys should be generated and documented as for _services/applications_ and not _people_.
   - Communicate that metric filters should be configured to watch the correct log group.
   - Test Alarms as part of the [Production Readiness](../standards/production-readiness.md) process.
   - Consider tracking usage of Sierra API keys (i.e. what services use a Sierra API key) so they can changed more easily.
8. Tracking of Preventative Measures
   - This post-mortem will shared with relevant staff and asked to take appropriate actions.
   - [Monitoring & Alarms](../standards/alerting.md) standard will be updated appropriately.
