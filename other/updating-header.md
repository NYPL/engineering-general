# Changing NYPL Header

The primary NYPL header is maintained as a React component distributed as an NPM module. To support non-React apps, a "header app" ensures the component may also be included via  aa `<script>` or as fully rendered HTML.

The following proposes a safe sequence of deployments for activing changes to the header across our apps. 

## 1. Update React Header Component

The React Component [source is maintained in Github](https://github.com/NYPL/dgx-header-component) and [published to NPMJS](https://www.npmjs.com/package/@nypl/dgx-header-component).

Changes to the component should follow [the instructions in the repo](https://github.com/NYPL/dgx-header-component#contributing-is-fun-and-easy) for review, merging, and tagging. Don't overlook publishing the new version to NPMJS.

## 2. Activate Changes in React Apps

Starting with the lowest traffic [React apps](https://github.com/NYPL/engineering-general/tree/master/other#reactnode) (excluding "Header App"), update the `dgx-header-component` dependency to use the new version. Proposed order:

 * [Get a library card](https://bitbucket.org/NYPL/nypl-library-card-app/src/master/)
 * [New Arrivals](https://bitbucket.org/NYPL/dgx-new-arrivals)
 * [Staff picks](https://github.com/NYPL/staff-picks)
 * [BookLists](https://bitbucket.org/NYPL/dgx-booklists)
 * [SCC](https://github.com/NYPL-discovery/discovery-front-end)
 * [Global Search](https://bitbucket.org/NYPL/dgx-global-search)
 * [Blogs beta](https://bitbucket.org/NYPL/dgx-blogs)
 * [Homepage](https://bitbucket.org/NYPL/dgx-homepage)

Note: You may choose to do QA deployments exclusively for steps two and three, followed by production deployments.

## 3. Activating Changes in Non-React Apps via Header App

Because not all NYPL apps use React, a special Header App exists to provide two different methods of inclusion:

 * [Embeddable Script](https://github.com/NYPL/nypl-dgx-react-header#embeddable-script): Include the header in any app via `<script>` tag.
 * [Fully Rendered HTML](https://github.com/NYPL/nypl-dgx-react-header#drupal-import) (aka "Drupal Import"): Get raw html, JS, and CSS to include in any app server-side.

To incorporate changes made to the React Header Component above, change the `@nypl/dgx-header-component` version to match the latest version of dgx-header-component in NPMJS. For example [this PR bumped the Header App to use Header Component `1.4.19`](https://github.com/NYPL/nypl-dgx-react-header/pull/26/files). Travis will automatically deploy changes merged to `development`, `qa`, and `master` (production).

 * Locations: Locations QA is deployed with `LOCINATOR_ENV` "qa", which causes app to use qa deployments of refinery and header app (i.e. [App will load `https://qa-header.nypl.org/dgx-header.min.js?skipNav=main-content`](https://github.com/NYPL/locations-app/blob/8517c884fe8bc46998077ced735b992875a47b5a/views/index.erb#L65)
 * Staff Profiles: Staff Profiles appears to be [configured identically](https://bitbucket.org/NYPL/dgx-staff-profiles/src/c1ccec275ef7754632c617821a6c1287cfb245a5/views/staff_profiles.erb?at=master#staff_profiles.erb-55), although **it's unclear where/how this is deployed**
 * Research Divisions: This also appears to be [configured identically](https://bitbucket.org/NYPL/research-collections/src/04d8a64e3b140a5751a78974b895c60006c97309/views/research_collections.erb?at=master#research_collections.erb-55), but it's also **unclear where/how this is deployed**.


