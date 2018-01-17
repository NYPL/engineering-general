# Version Tagging

All repositories and components that may be dependencies of other entities MUST use [semantic versioning](https://semver.org/) to enable controlled roll-out of new functionality and mitigate breaking changes.

Version numbers SHOULD begin at `1.0.0`.

The following convention MUST be used when incrementing the version number:

 * **Major release**: First digit. Changes that break backwards functionality.
 * **Minor release**: Second digit. Addition of new features that don't break existing features.
 * **Patch release**: Third digit. Bug fixes and other minor changes.

When flagging a given version as **"pre-release"** (i.e. a version made available for testing, but not for general consumption by the unwary), the version number MUST use an alphanumeric suffix. For example, if the current release is `1.0.1` and you would like to publish a candidate for `1.0.2`, you may tag it `1.0.2-alpha`. After review, pre-release versions MUST be followed by proper release (e.g. `1.0.2`) for general consumption. [See semver notes on pre-releases](https://semver.org/#spec-item-9)

## Git Repository versioning

Any repository using semantic versioning MUST reflect those versions in git "annotation" tags, as in:

```
git tag -a "v1.0.3"
git push --tags
```

## NPM versioning

NPMJS uses `package.json` to identify the version of a given deployment. 
For convenience, one can use [npm version](https://docs.npmjs.com/cli/version]). For example, after merging a patch to your deploy branch:

```
# This updates the version in package.json and commits it:
npm version patch -m "Version bump (patch)"

git push --tags
git push origin [npm release branch]
npm publish
```



