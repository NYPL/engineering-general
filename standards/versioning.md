# Version Tagging

All repositories and components that may be dependencies of other entities MUST use [semantic versioning](https://semver.org/) to enable controlled roll-out of new functionality and mitigate breaking changes. For a quick reference on bumping a components version, see (Typical Workflow)[#typical-workflow] below.

Version tags SHOULD start with a "v".

Version numbers SHOULD begin at `1.0.0` (i.e. tagged `v1.0.0`).

The following convention MUST be used when incrementing the version number:

 * **Major release**: First digit. Changes that break backwards functionality.
 * **Minor release**: Second digit. Addition of new features that don't break existing features.
 * **Patch release**: Third digit. Bug fixes and other minor changes.

When flagging a given version as **"pre-release"** (i.e. a version made available for testing, but not for general consumption by the unwary), the version number MUST use an alphanumeric suffix. For example, if the current release is `v1.0.1` and you would like to publish a candidate for `v1.0.2`, you may tag it `v1.0.2-alpha`. After review, pre-release versions MUST be followed by proper release (e.g. `v1.0.2`) for general consumption. [See semver notes on pre-releases](https://semver.org/#spec-item-9)

## Git Repository versioning

Any repository using semantic versioning MUST reflect those versions in git "annotation" tags, as in:

```
git tag -a "v1.0.3"
git push --tags
```

## NPM versioning

NPMJS uses `package.json` to identify the version of a given deployment. The version number in `package.json` MUST NOT include the 'v' prefix.

For convenience, one can use [npm version](https://docs.npmjs.com/cli/version]). For example, after merging a patch to your deploy branch:

```
# This updates the version in package.json and commits it:
npm version patch -m "Version bump (patch)"

git push --tags
git push origin [npm release branch]
npm publish
```

## Changelog

Repositories and components that maintain version tags SHOULD include a `CHANGELOG.md` that documents the difference between tags at a high level. This file SHOULD include one section for each tagged version, listed in reverse chronological order, with headings matching the version tags (optionally followed by date of release).

Version sections MAY organize lists of changes under header level 3 subsections labeled "Features", "Bug Fixes", "BREAKING CHANGES", or other topics of interest to a reviewer.

Pre-release versions MAY be excluded.

A sample `CHANGELOG.md` follows:

```
# CHANGELOG

## v2.0.1
 - Add OZ code to locations and recapCustomerCodes

## v2.0.0 - 2018-02-01
 - Rename multiple mappings files for consistency

### BREAKING CHANGES
 - Multiple paths have changed, breaking previous contracts

## v1.1.1
 - Fixed broken CLI loglevel handling
 - Documentation clean-up

## v1.1.0
 - Added CLI

## v1.0.0
 - Initial release
```

## Typical Workflow

The following is the standard workflow for bumping a component version. If a component deviates from this strategy, it MUST be noted in the `README.md` and SHOULD be noted in `CONTRIBUTING.md`.

1. Cut feature branch against the repo's deveopment branch (typically `development` or `master`)
1. Update the app version to the next logical version. This may include updates to:
   - `package.json`/`.gemspec`
   - `README.md`
   - `CHANGELOG.md` (See notes above for updating a CHANGELOG)
1. Commit your changes as part of your feature branch
1. Create a PR to merge your feature branch into the development branch (typically `development` or `master`)
1. After approval, merge the development branch into qa
1. After QC signoff, merge qa into the production branch
1. Git tag the production branch with version number (see [#git-repository-versioning](notes above)

Note that this strategy sometimes creates extra work if multiple features are under review simultaneously (because they will be competing for the next logical version number). When that happens, discuss with collaborator about whether to:
1. merge all approved feature branches at once into development (ensuring both changes are noted correctly in the CHANGELOG), or
1. reward the version number to the first feature merged to production; The other feature will have to be patched with the next logical version number (although it needn't repeat any stage of review).

To see how version bumps are implemented in other Git stategies, see our [./git-workflow.md](Git Workflow doc)
