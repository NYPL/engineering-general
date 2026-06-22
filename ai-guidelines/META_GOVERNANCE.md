# AI Guidelines Meta-Governance Policy
**Version:** 0.1

## Overview

This is a "meta" document — unlike the [AI working policy](./README.md) itself, this does **not** define how NYPL Digital should use AI in day-to-day engineering work. Instead, it answers the following questions:
- Who is responsible for reviewing and maintaining the AI working policy?
- How are changes to the policy proposed and recorded?
- How can we maintain the policy as a living document, and avoid letting it get out of date?

In essence, **this charter outlines the maintenance *behind* the working policy**. As a reminder, the AI working policy only applies to those who write, review, and ship code.

---

## Rotating Stewardship

The AI working policy will be reviewed on a **quarterly basis**. Two engineering pods will be paired up to review and recommend changes to the policy, based on their teams' actual experiences with AI tooling. Not only does this encourage cross-pod collaboration, but it also gives technical leadership a chance to gather how and why tools like Gemini and CoPilot are used by engineers.

After assessing the current policy against their engineers' experiences and against any external or vendor changes (e.g. licensing, pricing, data privacy updates), the pods will propose changes as needed, along with the associated rationale.

Final approval of these recommendations will come from either the technical team leads, the AI pod, or higher leadership. *(TBD)*

### Example Rotation Schedule

| Quarter | Rotating Pod Pair |
| :------ | :---------------- |
| Q1 | Research Catalog + Data Platforms & Access |
| Q2 | UPE + ISW |
| Q3 | Scholarly Research + ILS |
| Q4 | Digital Asset Preservation & Access + SWIS |

### Off-Cycle Reviews

In the event of an "emergency," an off-cycle review can be triggered. Examples of pressing incidents include:
- A new institutional directive arrives from HR, Legal, etc. that could affect our AI use
- Major privacy breaches on one of our approved AI tools
- Major shifts in the AI landscape (e.g. updated regulation)

Off-cycle reviews are ad-hoc and can be carried out by the existing AI working policy group.

---

## Versioning

Because of its transient nature, the AI working policy requires a **"last reviewed" date** and a **version number** to monitor how the document has evolved. This is modeled after our [pre-established versioning guidelines](../standards/versioning.md):

| Change Type | Version Step | Example |
| :---------- | :----------- | :------ |
| Major | x.0 | New tool approved; a substantive rule change |
| Minor | x.y | Clarified wording; added an example; small scope tweak |
| Review, no change | date only | Quarterly review completed; policy reaffirmed as-is |

Alongside its versioning, the AI working policy document should have an associated **decision log** (similar to a [CHANGELOG](../standards/documentation.md#changelog)) to briefly record how and why updates were made.
