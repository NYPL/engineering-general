# Technical Approach Documents

Technical Approach Documents (TADs) allow engineers to explore possible solutions to a technical problem before development begins, uncovering potential issues and ultimately landing on a recommended approach through the process.

## Audience

TADs are ultimately technical documents for a technical audience, not for Product or non-technical stakeholders. They do require approval from the Engineering Leadership Team (ELT), which includes Engineering Managers and the Director of Engineering as [described below](#review-process).

Generally, the sections of the TAD that you'll be writing are for:
* Your technical peers, i.e. other engineers who will be reviewing PRs and implementing the feature alongside you
* The Engineering Manager who will be writing the Review Summary section at the end of the review process. The Director of Engineering will be reading the Review Summary section and skimming any other sections of the document that they find helpful.

Since the Engineering Manager might not be intimately familiar with your technical stack or the problem at hand, it is helpful to provide some additional context in the "Problem Definition/Goal" and "Architectural Summary" sections of the template. For example, an iOS engineer might add a brief sentence or two of background information about iOS technologies if the Engineering Manager is not familiar with those technologies.

## Authors

TADs should be assigned to engineers by Technical Leads or Architects. Writing a TAD is a good opportunity to grow as an engineer, to have sanctioned time to research integrating different approaches into an NYPL codebase, and experiment with a new tool or technology.

If it is unknown who will be doing the implementation work for a project, an engineer with previous experience or subject matter knowledge should be assigned the task of writing a TAD.

TADs SHOULD have one author. In instances where a more collaborative approach is desired, consider splitting the TAD up into separate TADs each with their own author. See more in the [length](#length) section below.

## Tone

TADs are persuasive documents grounded in facts and best practices. Writing a TAD is communicating, “This is what I think we should do, and this is why.” Readers SHOULD come away from the TAD understanding why we need the solution that you recommended.

## Length

TADs SHOULD be as concise as possible while including all of the details that have a material impact on your design's acceptability. Generally, we recommend a TAD be no longer than 10-12 pages. You may include supplemental information, code samples, and other asides that aren't essential in an optional "Appendix" section. Items in the Appendix don't count toward the recommended 10-12 page limit.

Long TADs are a sign that the document should be split up into multiple TADs, with priority assigned to the one that is required to start implementation.

## When Necessary

TADs do not have to be created for all development work, but MUST be created in the following cases:

- If a Business Requirements Document (BRD) has been created
- If the pros and cons of introducing a new tool or technology to a project, team, or the department need to be considered
- If developers disagree or are unsure on the entire approach for implementing the new feature. Generally, a TAD should eliminate the kind of pull request that generates feedback in the realm of, "We need to rethink this entire approach."

TADs SHOULD be created in the following situations:

- If the scope of work is expected to extend beyond a single sprint
- If multiple developers will be contributing to the new feature
- If multiple approaches to a feature or problem are valid and the engineer assigned the ticket(s) wishes to document the decisions made
- If questions are raised about the appropriateness of an approach and engineer/team wishes to document the decision process
- If a engineer is faced with a decision or choice that they would like to receive feedback on and/or have validated by a more senior member of the engineering team.
- If writing the TAD will save engineering team time in the implementation phase. Figuring out the hardest challenges in a TAD usually helps saving time down the road.

## Resourcing

The quarterly planning process is a good time for Tech Leads and Architects to look ahead at the upcoming quarter and ensure enough engineering time is allocated to writing TADs for a planned feature or project.

## Timing

The TAD MUST be written before any implementation work begins. However, TADs SHOULD NOT be written _too far_ in advance of implementation. Best practice is to make Jira tickets and start implementation in the sprint immediately following document approval.

## Proof of Concepts

A TAD MAY include a proof of concept as demonstration of feasibility of and confidence in the recommended approach.

A proof of concept should be time-boxed to no longer than one sprint (two weeks). Tech leads and architects SHOULD guide engineers in generating a list of questions that the proof of concept aims to answer or clarify.

A proof of concept MUST NOT go to production. The expectation is that a proof of concept is a rough draft built using mock data and may not include the cleanest or most maintainable code. If possible, it is recommended to implement a solution that _only_ runs locally & in a separate repository with a name that includes `proof of concept` in the title OR in a feature branch that is left unmerged.

## TAD Template

The TAD template can be found in the Google Drive NYPL template gallery. Select it in Google Docs using `File > New > From template gallery` and make sure you're on the `NYPL` tab. Navigate to the `NYPL` section header and the TAD template will be in the list.

The TAD template includes several sections that serve as a guide for getting started. Feel free to add or reformat sections as you see fit. Take a look at the [examples](#tad-examples) below for inspiration.

Writers should start by stating the problem and goals in a couple of sentences or paragraphs and then add an architectural summary of the problem at hand as it relates to the existing code base or infrastructure. For features that involve deep understanding of the underlying infrastructure and/or changes to an architectural pattern, this section can be quite long and include many sub-sections. See the [DAM — Virtual Reading Room, Phase 1A TAD](https://docs.google.com/document/d/1c9f2lxb8-ANWdMxcLIej_bN87muSfP7WkLs7zS3BWOc/edit#heading=h.kutc298lyner) as an example.

If there are multiple options to weigh before proposing a final recommendation, each option should include a description and a list of pros and cons.

Writers should consider multiple layers of the technical stack in the TAD: backend, frontend, APIs, infrastructure (devops), and security concerns, for example. If you're unsure about any of these sections, reach out for help from your Tech Lead or engineering peers for help. Talking with other teams, i.e. devops, frontend, or backend, is also encouraged throughout the writing process.

The recommendations section should clearly state the final recommended approach alongside a summary or list of any other recommendations discussed throughout the TAD.

The next steps section can be a short summary or list of next steps that need to be taken. This section does not need to include links to Jira tickets.

## Process

All TADs MUST follow this process to be approved, at which point JIRA tickets can be created and development work can start.

1. An engineer is assigned a ticket to write the TAD and the ticket MUST be tagged with `tech-approach`. Assigning points to a TAD-writing ticket can be challenging. Generally a TAD is given 5, 8, or 13 points, depending on the complexity of the feature, how much research is needed, time for edits, and if a [proof of concept](#proof-of-concepts) is necessary.
2. The assigned developer should collect as much information from the BRD, stakeholders and any other relevant information sources and write the TAD. It is recommended to time box the TAD-writing process to one sprint (2 weeks) so as not to lose context or momentum on the problem at hand. To make this happen, it is recommended to complete a _first_ draft within one week in order to get peer feedback sooner, especially on major challenges and avoid wasting 2 weeks writing about an insufficient approach. Oftentimes the various iterations, including format fixes, corrections, expansions, and summaries, can take longer than expected. If a [proof of concept](#proof-of-concepts) is deemed necessary, then this may extend the TAD-writing phase by an additional week or sprint, depending on the feature or project.
3. The TAD MAY be circulated at this point for further feedback within a team or stakeholders for further input/feedback. Posting the drafted TAD in a public channel is a good way to start receiving feedback. Scheduling a meeting to review the draft with team members is another option. It is recommended to set clear expectations about how long the TAD will be open for comments and discussion from team members and when that window is considered closed.
4. When ready for review the Engineering Leadership Team (ELT) should be notified, the TAD uploaded to the shared TAD Google Drive (see below), and the associated JIRA ticket moved to the `Under Review` column
5. The TAD MUST be reviewed by at least one ELT member with subject area knowledge, and SHOULD be reviewed by two members (see review process below)
6. If approved, the TAD MUST be sent to the Director of Engineering for final approval.
7. With final approval the associated JIRA ticket is moved to `Done`. Specific tickets MUST be created to execute the work as described in the TAD.

### Sample TAD Timeline

- __Day 1-2__ Research & information gathering
- __Day 3-4__ Complete research & begin drafting
- __Day 5__ Complete initial draft
- __Day 6__ Refine draft & circulate internally for feedback
- __Day 7-8__ Refine draft & finalize recommendations
- __Day 9__ Finalize draft
- __Day 10__ Submit TAD for review

### Review Process

Step 5 above includes the following steps to be followed by the Tech Lead/Architect who is reviewing the document:

1. After reviewing the document they should add a summary to the end of the TAD including: Potential Risk, Cost and an evaluation of the completion of the TAD
2. If revisions are requested/necessary the document's author should make the necessary changes and record the process in a changelog to be added to the end of the document
3. The above steps should be repeated until the document is approved

### Changes After Approval

During the implementation phase, it is possible that the approved approach is deemed insufficient and the technical team pivots to a different solution. In this case, it is important to update the original TAD in the "Changelog" section at the bottom of the document. Including a changelog with a record of why something didn’t work the way we expected provides helpful context to new and existing team members. You should also tell your Tech Lead/Architect/Manager about these updates so they can be communicated up the chain if necessary.

## TAD Examples

### TADs that follow the above guidelines

- [Reservoir Design System — Header App AWS Deployment](https://docs.google.com/document/d/1k8tAuQ6OEk23CsGE2p0uqWFmMBRF4Sp8K2r9YRyMkvU/edit#heading=h.kutc298lyner): This document describes the problem and architectural summary in detail without going over the recommended 10 page limit. Each approach includes pros and cons that are grounded in fact and the final recommendation follows technical best practices for maintainability.

- [DAM — Virtual Reading Room, Phase 1A](https://docs.google.com/document/d/1c9f2lxb8-ANWdMxcLIej_bN87muSfP7WkLs7zS3BWOc/edit#heading=h.kutc298lyner): 7 pages long and explains a complex new system very clearly

- [LSP — Research Catalog My Account](https://docs.google.com/document/d/12Tcr4b9z-_icH5COr_pWUtUBFFBWo2mOH2T65_zF0tQ/edit#heading=h.kutc298lyner): Clearly defines the problem and why the current solution is bad, and also breaks the suggested approach into two implementation phases to build out the feature incrementally.

- [Digital Research Books — Adding New Relic Instrumentation](https://docs.google.com/document/d/1mklgUj2rQyh8vpjBDw44aeVFX1-_v92KEeaPDmnqCOc/edit#heading=h.k9mn1t9nmu98): This is a good example of a TAD being used as an architecture and planning document. A TAD doesn't always need to weigh different options; it can be used to clarify the team's understanding of a new architectural pattern or third-party library.

### TADs with opportunities for improvement

- [Open eBooks — Hybrid Mobile TAD](https://docs.google.com/document/d/1OP9vD78IxtP-S3LVwUvFFx-ZHtw8J20MqCUbgwu1GPs/edit#heading=h.kutc298lyner): This document is too long (28 pages) and should have been split up into _multiple_ TADs.

- [Digital Research Books — Expose TOC for Single-Resource PDFs](https://docs.google.com/document/d/1k3RaT24glGBv9cccw2aqiYNSnFgB4SwZxiiNlogSUNM/edit#heading=h.kutc298lyner): This TAD is good, but it sat around for 6 months before implementation started. By the time we started implementing, we realized that we needed to re-think the technical approach and provide a new recommendation. This new approach should be documented in a changelog at the bottom of the document.

## Resources

- [Shared TAD Google Drive](https://drive.google.com/drive/u/0/folders/0AN2RNnk4RBBwUk9PVA): All TADs should be added to this drive in the appropriate portfolio group's directory
- The TAD Template can be found in the Google Drive NYPL template gallery. Select it in Google Docs using `File > New > From template gallery` and make sure you're on the `NYPL` tab. Navigate to the `NYPL` section header and the TAD template will be in the list.
- [Confluence TAD Documentation](https://confluence.nypl.org/display/DIGTL/Technical+Approach+Documents): Similar documentation page in confluence containing list of sample TADs from different projects
