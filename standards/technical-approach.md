# Technical Approach Documents

Technical Approach Documents (TADs) serve to help the engineering team document solutions to feature development, share ideas between teams, and help highlight potential issues with tasks before they are encountered during the development process.

TADs should strive to describe the whats, hows and whys of the technical problem that is trying to be solved. It should strive to understand the problem at hand in a comprehensive way and explore any challenges so that engineers can be confident in their implementations of solutions. In short, writing a TAD should answer any technical questions prior to the start of actual development work, freeing up developers to focus on implementation once the major questions have been resolved.

## Audience

TADs are ultimately technical documents for a technical audience, not for Product or non-technical stakeholders. They do require approval from the Engineering Leadership Team (ELT) as [described below](#review-process).

## Authors

TADs should be assigned to engineers by Technical Leads or Technical Architects. Writing a TAD is a good opportunity to grow as an engineer, to have sanctioned time to research integrating different approaches into an NYPL codebase, and experiment with a new tool or technology.

If it is unknown who will be doing the implementation work for a project, an engineer with previous experience or subject matter knowledge should be assigned the task of writing a TAD.

TADs SHOULD have one author. In instances where a more collaborative approach is desired, consider splitting the TAD up into separate TADs each with their own author. See more in the [length](#length) section below.

## Tone

TADs are persuasive documents grounded in facts and best practices. Writing a TAD is communicating, “This is what I think we should do, and this is why.” Readers SHOULD come away from the TAD understanding why we need the solution that you recommended.

## Length

TADs SHOULD be as concise as possible while including all of the details that have a material impact on your design's acceptability. Generally, we recommend a TAD be no longer than 10 pages.

Long TADs are a sign that the document should be split up into multiple TADs, with priority assigned to the one that is required to start implementation.

## When Necessary

TADs do not have to be created for all development work, but MUST be created in the following cases:

- If a Business Requirements Document (BRD) has been created
- If the scope of work is expected to extend beyond a single sprint
- If multiple developers will be contributing to the new feature
- If the pros and cons of introducing a new tool or technology to a project, team, or the department need to be considered

TADs SHOULD be created in the following situations:

- If multiple approaches to a feature or problem are valid and the engineer assigned the ticket(s) wishes to document the decisions made
- If questions are raised about the appropriateness of an approach and engineer/team wishes to document the decision process
- If a engineer is faced with a decision or choice that they would like to receive feedback on and/or have validated by a more senior member of the engineering team
- If writing the TAD will save engineering team time in the implementation phase. Generally, a TAD should eliminate the kind of pull request that generates feedback in the realm of, "We need to rethink this entire approach."

## Resourcing

The quarterly planning process is a good time for Tech Leads and Architects to look ahead at the upcoming quarter and ensure enough engineering time is allocated to writing TADs for a planned feature or project.

## Timing

The TAD MUST be written before any implementation work begins. However, TADs SHOULD NOT be written _too far_ in advance of implementation. Best practice is to make Jira tickets and start implementation in the sprint immediately following document approval.

## Proof of Concepts

A TAD MAY include a proof of concept as demonstration of feasibility of and confidence in the recommended approach.

A proof of concept should be time-boxed to no longer than one sprint (two weeks). Tech leads and architects SHOULD guide engineers in generating a list of questions that the proof of concept aims to answer or clarify.

A proof of concept MUST NOT go to production. The expectation is that a proof of concept is a rough draft built using mock data and may not include the cleanest or most maintainable code. If possible, it is recommended to implement a solution that _only_ runs locally & in a separate repository with a name that includes `proof of concept` in the title.

## Process

All TADs MUST follow this process to be approved, at which point JIRA tickets can be created and development work can start.

1. An engineer is assigned a ticket to write the TAD and the ticket MUST be tagged with `tech-approach`
2. The assigned developer should collect as much information from the BRD, stakeholders and any other relevant information sources and write the TAD. It is recommended to time box the first draft of the TAD-writing phase to one sprint (2 weeks) so as not to lose context or momentum on the problem at hand. If a [proof of concept](#proof-of-concepts) is deemed necessary, then this may extend the TAD-writing phase by an additional sprint.
3. The TAD MAY be circulated at this point for feedback within a team or stakeholders for further input/feedback. Posting the drafted TAD in a public channel is a good way to start receiving feedback. Scheduling a meeting to review the draft with team members is another option. It is recommended to set clear expectations about how long the TAD will be open for comments and discussion from team members and when that window is considered closed.
4. When ready for review the Engineering Leadership Team (ELT) should be notified, the TAD uploaded to the shared TAD Google Drive (see below), and the associated JIRA ticket moved to the `Under Review` column
5. The TAD MUST be reviewed by at least one ELT member with subject area knowledge, and SHOULD be reviewed by two members (see review process below)
6. If approved, in Step 5 the TAD MUST be sent to Garvita Kapur for final approval. With final approval the associated JIRA ticket is moved to `Done`
7. If approved, specific tickets MUST be created to execute the work as described in the TAD

### Review Process

Step 5 above includes the following steps to be followed by the Tech Lead/Architect who is reviewing the document:

1. After reviewing the document they should add a summary to the end of the TAD including: Potential Risk, Cost and an evaluation of the completion of the TAD
2. If revisions are requested/necessary the document's author should make the necessary changes and record the process in a changelog to be added to the end of the document
3. The above steps should be repeated until the document is approved

### Changes After Approval

During the implementation phase, it is possible that the approved approach is deemed insufficient and the technical team pivots to a different solution. In this case, it is important to update the original TAD in the "Changelog" section at the bottom of the document. Including a changelog with a record of why something didn’t work the way we expected provides helpful context to new and exisitng team members.

## TAD Examples

### TADs that follow the above guidelines

- [Reservoir Design System - Header App AWS Deployment](https://docs.google.com/document/d/1k8tAuQ6OEk23CsGE2p0uqWFmMBRF4Sp8K2r9YRyMkvU/edit#heading=h.kutc298lyner): This document describes the problem and architectural summary in detail without going over the recommended 10 page limit. Each approach includes pros and cons that are grounded in fact and the final recommendation follows technical best practices for maintainability.

### TADs with opportunities for improvement

- [OE Hybrid Mobile TAD](https://docs.google.com/document/d/1OP9vD78IxtP-S3LVwUvFFx-ZHtw8J20MqCUbgwu1GPs/edit#heading=h.kutc298lyner): This document is too long (28 pages) and should have been split up into _multiple_ TADs.

- [Digital Research Books - Expose TOC for Single-Resource PDFs](https://docs.google.com/document/d/1k3RaT24glGBv9cccw2aqiYNSnFgB4SwZxiiNlogSUNM/edit#heading=h.kutc298lyner): This TAD is good, but it sat around for 6 months before implementation started. By the time we started implementing, we realized that we needed to re-think the technical approach and provide a new recommendation. This new approach should be documented in a changelog at the bottom of the document.

## Resources

- [Shared TAD Google Drive](https://drive.google.com/drive/u/0/folders/0AN2RNnk4RBBwUk9PVA): All TADs should be added to this drive in the appropriate portfolio group's directory
- [TAD Reference Doc](https://docs.google.com/document/d/1jL7yxFBmb8Pv9VR-dYNX1VTFaJzIgfVRyzinKk-T200/edit?usp=sharing): A sample TAD document to be used as the basis for future documents
- [Confluence TAD Documentation](https://confluence.nypl.org/display/DIGTL/Technical+Approach+Documents): Similar documentation page in confluence containing list of sample TADs from different projects
