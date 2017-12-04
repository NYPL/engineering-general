# Post-mortem

After an outage, security incident or other service disruption a post-mortem SHOULD be performed.

The post-mortem SHOULD be done as soon as possible _after_ the incident and SHOULD be done as a collaboration between engineers, managers, and parties affected.

Post-mortems are *blameless*. We're all human and make mistakes. At NYPL we want to encourage an [engineering culture](../culture/values.md#not-shaming-or-blaming) of experimentation, learning, continuous improvement, and make room for mistakes. We celebrate our post-mortems.

More learning about post-mortems:
- [Google SRE - Postmortem Culture: Learning from Failure](https://landing.google.com/sre/book/chapters/postmortem-culture.html)
- [How to Write Great Outage Post-Mortems](http://artsy.github.io/blog/2014/11/19/how-to-write-great-outage-post-mortems/)
- [What is an Incident Post-Mortem?](https://www.pagerduty.com/resources/learn/post-mortem-incident-report/)
- [Blameless PostMortems and a Just Culture](https://codeascraft.com/2012/05/22/blameless-postmortems/)


## Sample Post-mortem Template

Here is the information that SHOULD be included in a post-mortem. The complexity and length of each answer MAY be determined by the severity of the incident.

1. Incident Date
   - The date/time that the incident started.
2. Incident Summary
   - A few sentences to describe the incident.
3. Authors
   - Contributors to the post-portem.
4. Timeline
   - What was the timeline of the service disruption? When it was first reported, what actions were taken, and when it was resolved?
5. Root Cause
   - What was the root cause of outage/interruption? What actions contributed to this disruption?
6. Resolution and Recovery
   - How was the problem resolved? Were short-term fixes used?
7. Preventative Measures
   - What specific measures can we do to prevent this problem (and similar problems) from occurring?
8. Tracking of Preventative Measures
   - How have implementing the preventative measures been tracked?

### Sample Completed Post-mortem Template

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
