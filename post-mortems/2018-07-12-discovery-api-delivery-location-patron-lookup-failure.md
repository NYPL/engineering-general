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
   - July 12 1:34pm: Rosa Caballero-Li alerted scctechgroup@nypl.org about problem; Twana Fluker subsequently escalated to Stephen Betts & Kevin Friedman
   - July 12 2:00: Stephen Betts & Kevin Friedman examine DiscoveryApi logs for `$.level = "ERROR"` entries and find a number of errors implicating an empty response from the PatronService
   - July 12 2:20: Stephen Betts & Kevin Friedman determine that PatronService appears to be unchanged and functioning
   - July 12 2:30: Stephen Betts & Kevin Friedman notice that the recent deployment of the DiscoveryApi including bumping the version of the `@nypl/data-api-client` module, which no longer modifies api responses before passing them back to the caller (previously `client.get` stripped the root level `data` property if the endpoint response used one; this was a bad choice)
   - July 12 2:40: Paul Beaudoin cut a hotfix branch from `production`, merged it, and pushed it live.
     - https://github.com/NYPL-discovery/discovery-api/pull/119/files#diff-7c24ce55110822757567f71ceef0a1adR20
   - No alarms were raised
   - No tests explicitly checked the result of looking up a patron record. Existing tests mocked around the call to the PatronService, effectively cutting out the parts that parse that result.
   - this error was seen in the dev environment [by more than one person, I believe — STB] but was not taken seriously. So, one root cause is that the dev environment is not trusted
5. Root Cause
   - [nypl data api client](https://github.com/NYPL-discovery/node-nypl-data-api-client) was [bumped to 1.0.0](https://github.com/NYPL-discovery/node-nypl-data-api-client/blob/master/CHANGELOG.md#v100---2017-11-08), which includes a breaking change: Previously, when the returned data included a root-level `data` property, the contents of the `data` property was returned. As of `1.0.0`, the entire response is returned without modification. The previous practice was presumptuous, confusing, and in some cases prevented the integrating app from accessing other necessary root-level sibling properties.
   - The discovery-api [bumped its nypl-data-api-client dependency to 1.0.0 on June 7](https://github.com/NYPL-discovery/discovery-api/commit/c20963f9bfa41ffc37cf98decfd719e0d2053f43) to support the new annotated-marc endpoint. Although the existing test suite continued to pass, a thorough check of the codebase should have been performed to ensure the library was not relied on for anything not tested (or not adequately tested).
   - The discovery-api includes a route for 'request/deliveryLocationsByBarcode?barcodes[]={BARCODE}&patronId={PATRONID}', which returns the delivery locations allowed for a given item, by barcode. If `patronId` is given, the controller uses the PatronService to determine the patron's "Patron Type", which may enable additional delivery locations (i.e. Scholar p-type patrons may request items be sent to special rooms). The existing unit tests [overwrote the `AvailableDeliveryLocationTypes._getPatronTypeO` method](https://github.com/NYPL-discovery/discovery-api/blob/3ab4c994c8bcc942d43e4a3087fd900a7ee8f2df/test/available_delivery_location_types.test.js#L6) to avoid calling the patron service, inadvertantly also skipping code that parses the result. This is a fine test of the method's ability to map "Patron Type" codes to expected internal type names (i.e. "Research", "Scholar"), but effectively cut out the code that interprets Patron Service responses. We had no coverage for the code that parsed patron records, so when handling `undefined` patron records, tests did not fail.
   - Contributing to confusion, the NyplDataApiClient is instantiated twice in `discovery-api`, which may lead one to assume they've adequately assesssd the app's of NyplDataApiClient after reviewing the first instance.
6. Resolution and Recovery
   - Recovery:
     - Librarians could place holds through SCSB, so most patrons should have been able to achieve their needs, just with a bit more friction, or by waiting 24 hours.
   - Resolution:
     - Paul Beaudoin created and deployed hotfix.
     - Paul created new [DiscoveryApiErrorAlarm](https://console.aws.amazon.com/cloudwatch/home?region=us-east-1#alarm:alarmFilter=inInsufficientData;name=DiscoveryApiErrorAlarm)
7. Preventative Measures
   - Code-review all promoted features, particularly those that perform major version bumps on dependencies
   - When doing a major version bump of a dependent module, we should ensure the test suite includes tests against that dependent interface; If the version bump causes something about the interface to change fundamentally, we want a test to fail. To that end:
     - Modified existing patron type tests to use local fixtures representing two primary patron types to confirm 1) Patron Type code maps to correct delivery location class (existing check) and 2) Patron Type is correctly extracted from patron record (new check).
   - Ensure alarms raised when logged.
8. Tracking of Preventative Measures
   - Reviewers of this PR should confirm DiscoveryApiErrorAlarm appears to be correctly set up.
