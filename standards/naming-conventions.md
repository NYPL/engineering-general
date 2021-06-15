# Naming Conventions

As part of the NYPL Engineering team, proper naming delivers clarity and consistency amongst our code, applications, services, consumers and more. The following sections will detail examples on how we (NYPL Engineering), agree on a standard for naming.

Establishing proper naming will help each developer by:
- Reducing the effort needed to read and understand source code

- Enabling code reviews to focus on more important issues than arguing over syntax and naming standards

- Enabling code quality review tools to focus their reporting mainly on significant issues other than syntax and style preferences

## Table of Contents

- [Naming Conventions](#naming-conventions)
  - [Table of Contents](#table-of-contents)
  - [Identifiers](#identifiers)
    - [Readability](#readability)
    - [Multiple Words versus Single Word](#multiple-words-versus-single-word)
    - [Length of Identifiers](#length-of-identifiers)
  - [Version Tagging](#version-tagging)

## Identifiers

### Readability

Developers MUST make their naming declarations readable.

Well-chosen identifiers make it significantly easier for developers to understand what the codebase is doing or extend the source code to apply for new needs.

### Multiple Words versus Single Word

Developers MUST use "meaningful identifiers". A single word may not be as meaningful, or specific, as multiple words.

### Length of Identifiers

Developers SHOULD avoid the following issues that may arise by:

- declaring extremely short identifiers. For example, using 'i' or 'j' make it very difficult to uniquely distinguish using automated search and replace tools
- declaring longer identifiers may be preferred because short identifiers cannot encode enough information or appear too cryptic
- extremely long identifiers may be disfavored because of visual clutter

Developers SHOULD find the right balance as long as readability, clarity and meaning is accomplished.



## Version Tagging

See our [Versioning standard](../standards/versioning.md) for guidance creating version tags.
