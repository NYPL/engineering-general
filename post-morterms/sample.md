# Sample Post-mortem

1. Incident Date
   - June 20, 2016
2. Incident Summary
   - Website location pages were returning a 404 to the public
3. Authors
   - Kevin Friedman (kevinfriedman@nypl.org)
   - Brett Richter (brettrichter@nypl.org)
4. Timeline
   - At around 2pm on Sunday, Appsdev started receiving New Relic Refinery alerts.
   - Presumably around this time, locations pages (and other pages dependent on the Refinery) were returning a 404 error to the public.
   - Service was fully restored by 8:00am on Monday.
5. Root Cause
   - The Refinery makes connections to https://www.nypl.org (routing through Imperva) for data refreshes. We suspect that the ELB was blocking access to Imperva during the time of this outage because Imperva was using an IP address not granted access in the ELB.
6. Resolution and Recovery
   - Immediately, as a short-term fix, Devops allowed global access to the ELB to allow for the Refinery to rebuild its cache and restore service to the public.
     - Global access was subsequently removed.
   - Devops discovered that not all IP address ranges known to be used by Imperva were granted access on the ELB.
     - These IP access ranges have been granted access in the ELB.
7. Preventative Measures
   - Devops is monitoring the thread that announces IP address ranges used by Imperva and will be more proactive in adding new IP address ranges.
   - Appsdev will be more proactive in responding to New Relic alerts and not dismiss alerts without verifying the suspected cause.
   - Appsdev will work with Devops to install Loggly on Refinery nodes.
8. Tracking of Preventative Measures
   - Tickets have been created and assigned in JIRA.
