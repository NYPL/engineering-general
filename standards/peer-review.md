## Pull Request Workflow

- All Pull Requests to NYPL repositories MUST be reviewed prior to merging (caveat below).
  - PRs MUST NOT be merged if a reviewed requests changes
  - Teams MAY agree to specific written policies as to conditions when reviews are not required. Such a policy MUST be approved by a Tech Lead or Engineering Manager.
  
- Engineers MUST mark at least one (1) developer as a reviewer and SHOULD request reviews from all relevant engineers
  - Reviewers MAY come from any team within NYPL Digital
  - Teams MAY create [CODEOWNERS](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners) files to establish a default group of reviewers
  - Experience SHOULD NOT be taken into account when requesting review
  - Requests for specific feedback MAY be requested by tagging specific engineers in PR comments

- Engineers marked as reviewers SHOULD complete the review in a timely manner
  - This period SHOULD be agreed upon within individual development teams, 24-48 hours has proven to be a reasonable starting place
  - Code review SHOULD take some time (more than a quick LGTM) but should not take more than 1-2 hours
  - If a code review is very lengthy or complex, reviewers MAY request that the PR be broken up into smaller pieces and/or request a walkthrough/live review session
 
- If changes are requested (or made in response to questions) the requesting engineer SHOULD re-request review when ready
  - This helps reviewers track the current status of open PRs and plan time for review work
  - Additional rounds of review SHOULD be completed until the PR can be either merged or closed

- Engineers SHOULD utilize the Draft PR status to socialize work in progress and to solicit feedback
  - Reviewers SHOULD NOT use the "request changes" option on draft PR reviews
  - When a draft PR is ready for full review the requesting engineer MUST update its status and request (or re-request) review from relevant team members

# Peer Review

- All peer review MUST comply with our [Engineering Values](../culture/values.md)

- All work SHOULD go through the process of peer review. It is a form of collaboration and it strengthens quality.

- It SHOULD involve at least one (1) more experienced developer evaluating whether best practices are followed.

- It MAY consist of at least one (1) session of one-on-one peer review.

  - Example: One team member would make an appointment with another team member to chat about coding progress, followed by walk-through of code-in-review.

- It MAY involve a team member who is less experienced with the tech stack.

  - Example: A team member who is familiar with PHP can sit down with a team member familiar with Ruby on Rails, walking through the idea behind the PHP code, followed by a list concrete tests showing the code works.