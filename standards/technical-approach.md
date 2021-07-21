# Technical Approach Documents

Technical Approach Documents (TADs) serve to help the engineering team document solutions to feature development, share ideas between teams and help highlight potential issues with tasks before they are encountered during the development process.

TADs should strive to describe the whats, hows and whys of the technical problem that is trying to be solved. It should strive to understand the problem at hand in a comprehensive way and explore any challenges so that engineers can be confident in their implementations of solutions. In short writing a TAD should answer any technical questions prior to the start of actual development work, freeing up developers to focus on implementation once the major questions have been resolved.

## Authors

TADs should be written by the most senior engineer who is or will be working on a project/feature/fix. If it is unknown who will be doing the implementation work for a project an engineer with previous experience or subject matter knowledge should be assigned the task of writing a TAD.

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

## Process

All TADs MUST follow this process to be approved, at which point JIRA tickets can be created and development work can start.

1. The most senior developer on the feature/task/story is assigned a ticket to write the TAD and the ticket MUST be tagged with `tech-approach`
2. The assigned developer should collect as much information from the BRD, stakeholders and any other relevant information sources and write the TAD
3. The TAD MAY be circulated at this point for feedback within a team or stakeholders for further input/feedback
4. When ready for review the Engineering Leadership Team (ELT) should be notified, the TAD uploaded to the shared TAD Google Drive (see below), and the associated JIRA ticket moved to the `Under Review` column
5. The TAD MUST be reviewed by at least one ELT member with subject area knowledge, and SHOULD be reviewed by two members (see review process below)
6. If approved in Step 5 the TAD should be sent to Garvita Kapur for final approval. With final approval the associated JIRA ticket is moved to `Done`
7. If approved specific tickets should be created to execute the work as described in the TAD

### Review Process

Step 5 above includes the following steps to be followed by the Tech Lead/Architect who is reviewing the document:

1. After reviewing the document they should add a summary to the end of the TAD including: Potential Risk, Cost and an evaluation of the completion of the TAD
2. If revisions are requested/necessary the document's author should make the necessary changes and record the process in a changelog to be added to the end of the document
3. The above steps should be repeated until the document is approved

## Resources

- [Shared TAD Google Drive](https://drive.google.com/drive/u/0/folders/0AN2RNnk4RBBwUk9PVA): All TADs should be added to this drive in the appropriate portfolio group's directory
- [TAD Reference Doc](https://docs.google.com/document/d/1jL7yxFBmb8Pv9VR-dYNX1VTFaJzIgfVRyzinKk-T200/edit?usp=sharing): A sample TAD document to be used as the basis for future documents
- [Confluence TAD Documentation](https://confluence.nypl.org/display/DIGTL/Technical+Approach+Documents): Similar documentation page in confluence containing list of sample TADs from different projects