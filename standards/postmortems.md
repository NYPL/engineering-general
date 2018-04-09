# Post-mortems

After an outage, security incident or other service disruption a post-mortem SHOULD be performed.

The post-mortem SHOULD be done as soon as possible _after_ the incident and SHOULD be done as a collaboration between engineers, managers, and parties affected.

Post-mortems are *blameless*. We're all human and make mistakes. At NYPL we want to encourage an [engineering culture](../culture/values.md#not-shaming-or-blaming) of experimentation, learning, continuous improvement, and making room for mistakes. We celebrate our post-mortems.

Completed post-mortems SHOULD be saved in the [post-mortems](../post-mortems) directory ([sample](../post-mortems/sample.md)) for a historical record and shared with relevant parties.

### More learning about post-mortems ###

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

