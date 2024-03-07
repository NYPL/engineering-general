# GitHub Organization Management

1. All new repositories and Teams should be created within the existing [NYPL](https://github.com/NYPL) Org, unless specifically called out in the Product Brief, BRD, or TAD. There should not be a need to create additional organizations outside of the NYPL Org or to add repositories within any of the other NYPL organizations, such as NYPL-Simplified. We are aiming to consolidate all extranneous orgs under the NYPL org.
2. All active NYPL employees, this includes both FTEs and Contractors, who need Read, Write, or Admin access to NYPL repositories must be invited as a Member to the NYPL Org. They should _not_ be added to any repository as an Outside Collaborator.
3. NYPL employees can use an existing GitHub account created with a non-NYPL email address or create a new GitHub account using their NYPL email address.
4. It is recommended, but not required, that their [profile](https://github.com/settings/profile) include an easily recognizable name. This allows us to manage Members more easily.
5. Anyone who is part of the NYPL GitHub Org must enable two-factor authentication (2FA).
6. Use GitHub [Teams](https://github.com/orgs/NYPL/teams)
   - Each portfolio group will have a Team. There will also be additional teams for Design System and Data Engineering, which operate outside of a traditional portfolio group structure. The manager or tech lead/architect who manages that team should be listed in that team's About section.
   - Within each Team, there will be two or three child Teams: (1) Read access for people who don’t push code, (2) Write access for people who push code, and (3) Admin access for tech leads, architects, and managers.
   - Add Teams to repositories. Don’t add contributors individually. Unless…
     - Non-NYPL employee contributors should be added to the individual repo as an Outside Collaborator. This makes it easy for us to see who is an Outside Collaborator with access to repositories, since all Outside Collaborators are grouped into their own tab.
     - Non-portfolio Teams or Teams outside Digital may be necessary. The Preservation & Collections Processing Team is an example of this. These Teams should have a designated “owner” with an email address in the “About” section.
   - Do not create “Secret” Teams, which is discouraged by GitHub, unless there is a sensitive situation that requires their use.
   - [Onboarding](./onboarding.md) should include adding contributors to the NYPL Org and the appropriate portfolio Team(s).
   - [Offboarding](./offboarding.md) should include removing Members and Outside Collaborators from the NYPL Org.

## How to add a user to a repo:

_Note: Only GitHub Admins/Owners have the ability to add and remove members from the GitHub Org. If you don't have access and need to add or remove someone, contact an Engineering Manager or Tech Lead._

1. If the person you're adding is an NYPL FTE or Contractor, [invite them](https://github.com/orgs/NYPL/people) to the NYPL Organization. They will need to accept this invite via email. Then make sure they have 2FA enabled (required) & ask them to add a recognizable name to their [profile](https://github.com/settings/profile) (optional).
2. Once the first step is complete, add them to the appropriate portfolio team(s). This should automatically grant them access to any repositories they need. Avoid adding individuals to repositories, unless they're an Outside Collaborator.
3. If they are not an NYPL employee or Contractor, add them to the repo they need access to as an Outside Collaborator.
