# **TL;DR**

- This document outlines a new approach to manual testing, shifting focus towards automation.
- Manual testing by the QA team should be avoided for generic checks or minor fixes covered by automated tests.
- Manual testing is still needed for new features, complex integrations, visual QA, and accessibility testing.
- The new QA process prioritizes automation, with developers responsible for self-verification and writing automated tests.
- Clear and detailed acceptance criteria are crucial for determining manual QA needs.
- Effective manual testing methods are described here, including using a dedicated template and exploratory testing.
- We suggest scheduling exploratory testing during feature development, before major releases, and after automated test runs.
- Hosting team-wide bug-bash sessions with clear goals, preparation, and follow-up is recommended.
- User Acceptance Testing (UAT) with external stakeholders is important for ensuring the product meets business needs. Links to sample docs are included here.

---

# Manual Testing: A New Approach

This document outlines a new approach to manual testing, emphasizing a shift toward automation and a more strategic use of manual testing resources.

## When to Avoid Manual Testing by the QA team

Manual testing should not be used as a routine "check the boxes" task. Avoid manual testing when:

- The request is generic, like "Please check and make sure everything is ok".
- The work is a minor fix or change that can be sufficiently covered by automated tests.

## When Manual Testing is Still Needed

Manual testing should be reserved for scenarios that genuinely benefit from a second set of eyes. This includes:

- New features or components
- Complex integrations
- Visual QA\*
- Accessibility testing\*

_\*Note: Visual QA and Accessibility Testing are currently owned by the accessibility consultant and the design team, and the process for these types of testing remains unchanged at this time._

## New QA Process: Key Changes

### Focus on Automation

The QA team is prioritizing automation over manual testing. The goal is to reduce reliance on manual testing and instead focus on comprehensive automated tests. This shift requires the entire development team to critically evaluate the necessity of manual testing for each feature or bug fix.

### Developer Responsibility

#### Developer Self-Verification in QA

Regardless of whether a change requires manual QA or is a minor fix, engineers are expected to double-check their own work in the QA environment. This "spot checking" is a fundamental part of an engineer's due diligence and contributes to a collaborative and high-quality development process. It helps catch issues early and ensures a smoother experience for both the QA team and end-users.

#### Developers Write Automated Tests

Developers should ensure their work is thoroughly covered by unit tests and, when appropriate, Playwright or API integration tests. For minor fixes or changes, developer discretion should be sufficient without requiring a QA team member's approval.

For guidance on our overall approach to automated testing, please refer to our [Automated Testing Strategy](https://docs.google.com/document/d/1ZcIcFLrYx7UJptqEA737b_8gNXljVG23RVv9_q9zp18/edit?usp=sharing).

The responsibility for writing tests isn't strictly divided between Engineers (unit tests) and QA Engineers (Playwright tests). The engineer developing a feature or fixing a bug should write the most appropriate test to ensure their code functions correctly and provides confidence in their work. QA Engineers will then supplement these efforts by identifying and addressing testing gaps, developing additional automated tests based on product requirements, ensuring automated tests are being written as part of the development process, and conducting regular manual testing, as detailed further in this document.

### The "Ready for QA" Column Revisited

Historically, the "Ready for QA" column on Jira boards signified that a QA person needed to review and approve a ticket before it could progress. For many teams, this column became a bottleneck, with tickets lingering and waiting for manual testing. Some teams have since removed this column entirely and instead assign manual testing tickets directly to the QA Engineer. Others still use the column.

Teams should use whatever workflow best supports their needs, but it's important to monitor how many tickets are regularly placed in this column for manual testing and whether it is causing delays in deploying to production. With a greater focus on automation, the number of tickets requiring manual QA should trend downward over time. If the "Ready for QA" column is becoming a bottleneck, consider revisiting your team's process or reducing reliance on manual testing for routine changes.

### Importance of Acceptance Criteria

Clear and detailed acceptance criteria are always necessary for any work going through the development process. These criteria will help determine whether a ticket requires manual QA testing or can be sufficiently covered by automated tests.

## Effective Manual Testing Methods

### Use the Manual Testing Document

Use the Manual Testing Document whenever manual testing is required—such as for new features, components, or complex integrations. This collaborative document brings together Visual QA, Accessibility QA, and functional testing in one place. The template for this document is now an official template in our Google Workspace (see the "VQA/QA/Accessibility Manual Testing Template" in the NYPL tab of the Template Gallery).

As manual testing is completed in this document, QA Engineers should create and prioritize automated testing tickets for any gaps identified (if not already written). This ensures that manual QA directly leads to improved automated test coverage.

Examples of how this document has been used for past projects:

- [Staff Profiles: Accessibility/QA/UAT and Bug Tracking](https://docs.google.com/document/d/1RiK1fOHdrmJjzWlYlpHC697d-5SBlUirpvUU5qBpxJ8/edit?tab=t.0#heading=h.bngjjr7cfh5e)
- [Research Catalog: Collection filter/ advanced search VQA/QA](https://docs.google.com/document/d/1CqQZg5vyHRm-0knUGnX8VBT54i06VLle32j0nyFcLIc/edit?usp=sharing)

### Exploratory testing or _Spend time with your application_

Exploratory testing is basically where a tester learns about the software, figures out what to test, and then actually tests it all at the same time to find bugs. Instead of following a strict script, it's pretty loose and driven by the tester's gut, what they know, and their creative thinking. It's almost always a good idea to just play around with your app. Try to think like a user. Come up with weird scenarios and give them a shot.

#### Key Concepts

**Simultaneous Process:** Think of it like this: you're designing and executing tests at the same time. As you explore the system, you learn more about it, and that helps you come up with new, unscripted tests on the fly. It's all about adapting as you go.

**Tester-Driven:** This method really relies on the tester's smarts and experience to sniff out bugs, especially those sneaky ones hiding in the corners that might not be covered by traditional, written-out test cases.

**Complementary, Not a Replacement:** Exploratory testing isn't meant to be the _only_ way you test. It's a super effective tool to add to your toolbox, helping you find unexpected problems and get a more complete picture of your test coverage alongside your usual scripted tests.

#### Scheduling exploratory testing

- **During Feature Development:** Conduct short, focused exploratory testing sessions (e.g., 30 minutes) on new features as they are being developed. This provides rapid feedback and helps catch bugs early.
- **Before a Major Release:** Dedicate a specific time to run exploratory tests on the entire application. This is a great way to find last-minute, integration-level bugs. It’s often most effective if the entire development team participates.
- **After Automated Test Runs:** Use exploratory testing to investigate areas where automated tests have a low coverage rate.

### Hosting team-wide bug-bash sessions

Bug-bash sessions can be initiated by anyone on the team. QA Engineers, in particular, should be able to organize and run these sessions with their teammates, especially when the situation calls for it. Hosting a successful team-wide bug-bash session requires careful planning, a well-run execution, and a solid follow-up. A bug bash is essentially a period of focused, informal testing where the entire team (QA personnel, developers, designers, product managers, etc.) dedicates time to find as many bugs as possible in a short time frame. Think of it as a "bug-hunting party".

#### 1\. Before the Bug Bash (Planning)

- **Define a Clear Goal:** The most important step. Decide what you're testing. Is it a brand-new feature? An entire user flow? Make the goal and scope very specific (e.g., "Find all bugs related to the new user profile page on iOS and Android").
- **Set the Time:** A bug bash should be a focused effort, not an all-day event. A one hour session works well to maintain energy and focus. Book this time on everyone's calendar.
- **Prepare the Environment:** Ensure the build is stable and deployed to a staging or testing environment. Provide clear instructions on how to access the build, log in, and perform any necessary setup.
- **Create a Centralized Bug-Reporting System:** Use a dedicated channel or a spreadsheet to track bugs in real time. Tools like Jira, or a shared Google Sheet work well. Make the reporting process as simple as possible.

#### 2\. During the Bug Bash (Execution)

- **Kick-off Meeting:** Start the session with a brief meeting. Reiterate the goal, the scope, and how to report bugs. This gets everyone on the same page.
- **Test and Report:** Encourage everyone to test freely and creatively. Remind them not to worry about writing perfect bug reports. Focus on getting the core information down: what the bug is, where they found it, and how to reproduce it. Screenshots and screen recordings are highly encouraged.
- **Foster Communication:** Encourage the team to talk to each other. When someone finds a bug, they should announce it. This prevents multiple people from finding and reporting the same issue. Use a dedicated Slack channel or a Zoom chat for real-time discussion.
- **Make it fun\!** Consider a small prize for the person who finds the most critical bug.

#### 3\. After the Bug Bash (Follow-up)

- **Review and Triage:** Immediately after the session, get the product manager to review the submitted bugs. Help them triage them into severity categories (e.g., high, medium, low) and assign them to the appropriate people.
- **Celebrate the Wins:** Acknowledge the team's effort and celebrate the results. Share a summary of how many bugs were found, the most critical one, and the overall impact of the session.
- **Document and Prioritize:** The bug bash should inform your backlog. Use the findings to create new tickets, enhance your test plans, and update your user stories.

### Asking stakeholders outside of the team to perform user acceptance testing (UAT)

User Acceptance Testing (UAT) with stakeholders outside the immediate development team is generally a process owned and led by Product Managers. Since Product Managers have the relationships with outside stakeholders, they should coordinate and drive this process. QA Engineers are available to assist in whatever way is most useful—such as preparing test plans, supporting test sessions, or helping with documentation—but the Product Manager should take the lead.

UAT is a crucial step for several reasons. It ensures the product meets the business needs from the perspective of real-world users and decision-makers, providing a vital, unbiased check before a release.

The ILS team takes this approach with each Sierra upgrade. They have a long-standing practice of using a multi-tab Google Sheet to collaborate with various library departments. This sheet is used to engage the actual users of Sierra admin tools, who are asked to perform steps simulating their daily tasks. Testers sign-off on each action from the spreadsheet. These testing sessions are typically conducted during off-hours, often on weekends.

**Example UAT working docs from our colleagues:**  
[UAT Example: Regression Tests](https://docs.google.com/spreadsheets/d/1AnrXFBxXU755HVrinnlxMS2FsfrRdnkpWzT_9Cxq4s0/edit?usp=sharing)  
[UAT Test Plan \- October 2025 Release](https://docs.google.com/document/d/1puYm3hxq9WTZ9Cew5Ys-xKqoC3UwrlioeyCOOs-fEuA/edit?usp=sharing)  
[UAT Example: Collaborative Tests](https://docs.google.com/spreadsheets/d/1RYi9DMcbx4v42BIBOrs0n8hiY0plghRODHYNf73_jak/edit?usp=sharing)

### Best Practices for UAT

#### Scheduling Best Practices

- Make sure high-priority bugs are resolved, all core functionality passes integration testing, and the test environment is stable.
- Don't schedule all users at once. Group testers based on how they will use the application (this may not be applicable for Library apps)
- Keep Sessions Short and Focused

#### Test Session Best Practices

- Run tests on a server that is as close to production as possible (or production, if you’re not testing new features, and just want to know how users are using your application.)

## Choosing the Right Manual Testing Approach

Different situations call for different manual testing strategies. Use this guide to determine which approach fits your needs:

### Use Manual Testing Document when:

- Testing a large, complex feature or project where Jira alone is insufficient for tracking
- You need to coordinate testing across multiple team members (developers, QA, designers, accessibility consultants)
- The feature has multiple components that need systematic verification (Visual QA, Accessibility, functional testing)
- You want a visual representation of bug status and testing progress
- You need to track acceptance criteria alongside testing notes in one place
- Example scenarios: Major product releases, multi-team integrations, significant UI overhauls

### Use Exploratory Testing when:

- Testing a new feature during active development (short 30-minute focused sessions for rapid feedback)
- You need to find edge cases and unexpected behaviors that scripted tests might miss
- Before a major release to catch last-minute integration bugs (entire team participates)
- After automated test runs to investigate areas with low coverage
- You want to think like a user and try creative/weird scenarios
- Automated tests are passing but you want human judgment on the experience
- Example scenarios: New user flows, complex business logic, areas prone to subtle bugs

### Use Bug Bash Sessions when:

- You have a specific, scoped area to test (e.g., new user profile page, checkout flow)
- You want to engage the entire team (QA, developers, designers, PMs) in focused testing
- You need many bugs found quickly in a short timeframe (typically 1 hour)
- Testing a brand-new feature before release
- You want to build team energy and collaboration around quality
- The feature is ready for intensive scrutiny but not yet released
- Example scenarios: Feature complete but pre-launch, high-stakes releases, team morale building

### Use UAT (User Acceptance Testing) when:

- You need real-world users or stakeholders to validate the product meets business needs
- The work involves critical business processes that actual users understand better than the dev team
- You need sign-off from decision-makers before release
- Testing requires domain expertise from library staff, researchers, or specific user groups
- The change affects daily workflows of staff or patrons
- Example scenarios: Patron-facing feature changes, staff tools, major workflow modifications

### Combining Approaches

These methods aren't mutually exclusive. For example:

- **Large new feature:** Manual Testing Document (to track) \+ Exploratory Testing during development \+ Bug Bash before release \+ UAT with stakeholders
- **Complex integration:** Manual Testing Document \+ Exploratory Testing in low-coverage areas
- **Minor UI change:** Developer self-verification \+ optional quick Exploratory Testing session
- **Critical business process change:** Exploratory Testing \+ UAT with actual users
