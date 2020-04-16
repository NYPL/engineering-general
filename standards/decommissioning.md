# Decommissioning and Deprecating Apps

NYPL creates different applications for user interfaces, data pipeline flow, APIs, and more. While we maintain these applications, sometimes it's better to move from one platform to another for many reasons.

When this happens, the developer(s) working on the new iteration of an application MUST let others know that the older version will be deprecated. This can reduce confusion on whether packages need to be updated for an app or codebase.

The above also applies to codebases that will no longer be used, such as moving code from one codebase to another, or upgrading to a different tool.

Developer(s) MUST:
* update the codebase's README. This MUST include a "Deprecaated" heading at the top and a "no longer supported" note, including the date of decommission if possible. If the repository has moved to a different source control location, the link MUST be included.
* let the team know that an app/codebase is deprecated. A message SHOULD be sent in the #dev channel in NYPL's Slack or also email digitaldev@nypl.org.
* update related documentation where the app/codebase's name comes up. The app's name can be searched in NYPL's Confluence wiki or by asking a teammate in Digital.
* archive the repo on Github.
* make sure that all the application servers are shutdown. This includes the development, qa, and production servers on AWS Elastic Beanstalk and any that NYPL IT hosts.

## Example

The Staff Picks react application was recently decommissioned and moved to a Drupal-based application. The following is on the [Staff Picks README](https://github.com/nypl/staff-picks).

```
# Deprecated
As of February 2020, this app is no longer in use at NYPL, and the current implementation is Drupal-based. Please contact the DXP/RENO team in Digital for more information. For NYPL developers, please see documentation on the update on [Confluence](https://confluence.nypl.org/pages/viewpage.action?pageId=24150584).
```
