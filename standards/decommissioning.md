# Decommissioning and Deprecating Apps

NYPL maintains various applications for user interfaces, data pipeline flow, APIs, and more. To align with product and department strategy and needs, it's possible that applications need to be decommissioned. This can happen for various reasons:

- there's a need to combine different APIs or services into a single product or codebase,
- the app need to be replatformed into Javascript/Typescript or Python,
- the tool, package versions, or service it's running on is outdated.

When this happens, the developer(s) working on the new iteration of an application MUST let others know that the older version will be deprecated. This can reduce confusion on whether an app or codebase is in use.

Developer(s) MUST:
* let the team know that an app/codebase is deprecated or will be deprecated on a specific date.
  * Examples of commmunication include sending a message in NYPL's `#dev` or the team-specific Slack channel or emailing `digitaldev@nypl.org`.
* update related documentation where the app or codebase's name is referenced. The app's name SHOULD be searched in NYPL's Confluence site and the `NYPL`, `NYPL-Simplified`, and `NYPL-Discovery` Github organizations.
* update the codebase's README and submit a PR.
  * This MUST include a "Deprecated" heading at the top, a "no longer supported" note, and the date of decommission.
  * If the repository has moved to a different source control location, the link MUST be included.
* archive the repo on Github.
* work with DevOps make sure that all the AWS EBS, ECS, or Lambda servers are shutdown. This includes the QA and Production servers in their relevant AWS accounts.

## Team-specific Processes

The above serves as a general guideline for decommissioning and deprecating products, services, and codebases. In addition to the above, teams can have their own processes that are more detailed and specific to the products they work on. Regardless of the steps involved, it's important to communicate them and maintain documentation.

The LSP team has to decommission certain endpoints and services, and this process was captured in their `lsp_workflows` [Deprecating a Service](https://github.com/NYPL/lsp_workflows/pull/24/files) document.

## Examples

### Application Restructure

In 2020, the Staff Picks React application was decommissioned and moved to a Drupal-based application. The following is on the [Staff Picks README](https://github.com/nypl/staff-picks).

```md
# Deprecated
As of February 2020, this app is no longer in use at NYPL, and the current implementation is Drupal-based. Please contact the DXP/RENO team in Digital for more information. For NYPL developers, please see documentation on the update on [Confluence](https://confluence.nypl.org/pages/viewpage.action?pageId=24150584).
```

### Lambda Replatform

#### BarcodeService

The [BarcodeService](https://github.com/NYPL/barcode-service) app was a Node-wrapped PHP AWS Lambda that served the Platform API `/api/v0.1/patron/{id}/barcode` endpoint. The codebase and lambda had not been updated since 2017, and it was verified that the lambda had no invocations in the previous 12 months.
