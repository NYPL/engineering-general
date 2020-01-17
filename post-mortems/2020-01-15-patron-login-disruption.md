_Before running a post-mortem, please see the [post-mortem standards](../standards/postmortems.md)._

# Patron Login Disruption Post-mortem

1. Incident Date
   - January 15, 2020
2. Incident Summary
   - Patron login disrupted when attempting to login through the header or either catalog interface (Encore <browse.nypl.org>, WebPac <catalog.nypl.org>).
3. Authors
   - Gregory Kallenberg
   - Ho-Ling Poon
4. Timeline
   - Between 3AM and 4AM on Wednesday, January 15, 2020, using login links produced an 'invalid-identity-auth' error from the oauth-server-prod application.
   - Catalog users were unable to login to the catalog (Encore or WebPac) when using the header links, or sign in links from the catalogs themselves.
   - Service was partially restored by 2:00 PM on Wednesday.
   - Service was fully restored by 9:00 AM on Friday.
5. Root Cause
   - A change was made January 14, 2020, to the catalog.nypl.org domain which hosts the CAS server for the ILS. This is used by the oauth-server and oauth-app applications which interact with the ILS on behalf of patrons to log them in from the header, browse.nypl.org or catalog.nypl.org. This is our universal login solution for allowing patrons to login once for both catalogs. The server that hosts the catalog.nypl.org WebPac application was retired from service and replaced with the ilsstaff.nypl.org WebPac server.
6. Resolution and Recovery
   - DNS was flushed by Brett to pick up the change to the catalog.nypl.org domain and redirected to ilsstaff.nypl.org
     - This removed the error, but created an issue where one had to login again on the ilsstaff.nypl.org domain to finalize the login procedure.
     - The cookie used by the header was not set properly to relay the logged in staus to users.
   - The oauth-server and oauth-app applications were found to have catalog.nypl.org defined as the CAS host, and it was determined that value needed to change to remove the double login and fix the cookie setting issue.
     - No test environment exists for these applications so changes were made to production directly.
     - Changes were made to environment parameters to use the ilsstaff.nypl.org domain as the CAS host, and the applications were deployed on January 16, 2020, around 8:30 AM.
7. Preventative Measures
   - TravisCI should be introduced to handled secure environment variables, run tests, run composer commands, and deploy to AWS.
   - Test environments should be created for both applications for testing changes and for use by QA.
8. Tracking of Preventative Measures
   - A configuration drift analysis is needed. The code deployments for oauth-server and oauth-app essentially are configuration adjustments, which has little effect on code logic changes.
   - A chaos session should be performed to test out what would be broken with or without configuration changes to identify what can potentially be broken.
   - If tools such as Optimizely is available, a more gradual deployment should be used with a rollback plan, de-risking the deployment.
9. Additional Issues Found
   - When logging in NYPL.org, the following security concern occurs
     - ilsstaff.nypl.org redirects to browse.nypl.org
     - going to catalog.nypl.org directly on address bar would go to classic catalog, but user would be asked to sign in again. Meanwhile, the header still reads cookies and remembers the user is logged in.
     - Clicking on sign in on classic catalog link would restart sign in process on ilsstaff.nypl.org.
     - The user at the same time is still logged in on browse.nypl.org. This is a red-flag for security. User would think that they are logged out when in reality that didn't happen, and subsequent users at can harm that user account if this is happening on public computers.
     
