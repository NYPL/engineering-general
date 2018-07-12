# Delivery locations failed to display in Shared Collection Catalog

1. Incident Date
   - July 12 2018
2. Incident Summary
   - Following 'Hold' button for any item in SCC, visitor presented with "Delivery options for this item are currently unavailable..." due to DiscoveryApi failing to look up patron record, which is required to determine visibility of some locations.
3. Authors
   - Paul Beaudoin
   - Stephen Betts
   - Kevin Friedman 
4. Timeline
   - July 11 mid-day: DiscoveryApi deployed to production
   - July 12 1:51pm: Stephen Betts notes widespread delivery location lookup failures
   - July 12 2:00: Stephen Betts & Kevin Friedman examine DiscoveryApi logs for `$.level = "ERROR"` entries and find a number of errors implicating an empty response from the PatronService
   - July 12 2:20: Stephen Betts & Kevin Friedman determine that PatronService appears to be unchanged and functioning
   - July 12 2:30: Stephen Betts & Kevin Friedman notice that the recent deployment of the DiscoveryApi including bumping the version of the `@nypl/data-api-client` module, which no longer modifies api responses before passing them back to the caller (previously `client.get` stripped the root level `data` property if the endpoint response used one; this was a bad choice)
   - July 12 2:40: Paul Beaudoin cut a hotfix branchfrom `production`, merged it, and pushed it live.
     - https://github.com/NYPL-discovery/discovery-api/pull/119/files#diff-7c24ce55110822757567f71ceef0a1adR20
   - No alarms were raised
   - No tests explicitly checked the result of looking up a patron record. Existing tests mocked around the call to the PatronService, effectively cutting out the parts that parse that result.
6. Resolution and Recovery
   - Recovery: [Extent of impact and recovery path unclear.]
   - Resolution:
     - Paul Beaudoin created and deployed hotfix.
     - Paul created new [DiscoveryApiErrorAlarm](https://console.aws.amazon.com/cloudwatch/home?region=us-east-1#alarm:alarmFilter=inInsufficientData;name=DiscoveryApiErrorAlarm)
7. Preventative Measures
   - Code-review all promoted features, particularly those that perform major version bumps on dependencies
   - Test suite should include expectations against dependent component interfaces
     - Modified existing patron type tests to use local fixtures representing two primary patron types to confirm 1) Patron Type code maps to correct delivery location class (existing check) and 2) Patron Type is correctly extracted from patron record (new check).
   - Ensure alarms raised when logged.
8. Tracking of Preventative Measures
   - Reviewers of this PR should confirm DiscoveryApiErrorAlarm appears to be correctly set up.
