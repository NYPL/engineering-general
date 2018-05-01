
_Before running a post-mortem, please see the [post-mortem standards](../standards/postmortems.md)._

# Gap in accession of itesm from ReCAP partners

1. Incident Date
   - April 23rd 2018
2. Incident Summary
   - ReCAP partner items had not been accessioned since February 6th 2018
3. Authors
   - Stephen Betts (stephenbetts@nypl.org)
   - Kevin Friedman
   - Kate Sweeney
4. Timeline
   - HTC send email January 18th, proposing a change of directory structure for partner record data, creating one for full data export files and one for incremental data export files
   - Other partners consented. 
   - Kate Sweeney forwarded email to S Betts, K Friedman, K Kelly, Nicole Ziabakhsh, Heide Miklitz on January 29th. Nobody thought it would have an impact. ADD LINK
   - Kate replied to group saying NYPL consents on January 30th
   - HTC implemented change to UAT on February 5th, production February 6th
   - NYPL stopped accessioning partner items from February 6th onward
   - April 23rd, Kevin Friedman was double checking on logging and noticed there were no logs from ReCAP Harvester, and then checked and saw there were no files in the `processedFiles` directory.
   - K Friedman alerted S Betts & K Sweeney via email
   - K Sweeney sent email mentioning previous thread about path directory change for certain files by HTC
   - K Friedman investigated and determined that would have caused the problem
   - K Friedman moved files from new directory to old directory and restarted Harvester to deal with backlog
   - K Friedman updated config of ReCAP Harvester and confirmed that it was picking up new accessioned items as expected
5. Root Cause
   - Change was approved when it should not have been
   - We did not realise that this would require a change on our side
   - We did not realise the scope of the change ('incremental' was only mentioned later in the email)
   - email was not clear that this was not backward compatible change AND we did not read email carefully enough
     - mitigated by original engineer who wrote Harvester (Jobin Thomas) was no longer working at NYPL

   - No alarms were raised
   - no monitoring on activity threshold (i.e., not based on actual errors)
   
6. Resolution and Recovery
   - Recovery: K Friedman moved files from new directory to old directory and restarted Harvester to deal with backlog
   - Resolution: K Friedman updated config of ReCAP Harvester and confirmed that it was picking up new accessioned items as expected
7. Preventative Measures
   - Better ownership of LSP should help
     - better awareness of orphaned components
   - Avoid miscommunication between HTC & NYPL (& partners)
     - e.g., involve Shelley Dexter in all such sign-offs
   - Recommend more formal change request process for changes to cross-partner functionality
     - include request to highlight breaking changes
   - better monitoring and alerting, i.e., based on activity thresholds
8. Tracking of Preventative Measures
   - K Sweeney will request formal change process from HTC
   - K Sweeney will create Jira ticket in the SCC project for activity monitoring and alerting on activity thresholds
