# NYPL Header Update Process

- [NYPL Header App Github Repo](https://github.com/NYPL/nypl-header-app)
- [Header Production Preview](https://ds-header.nypl.org/header)
- [Footer Production Preview](https://ds-header.nypl.org/footer)

The NYPL Header is maintained through the NYPL Header App. The Header App is used
to support sites and applications made with any framework. The Header App itself
is a React application that provides endpoints for applications to implement
through an embeddable HTML script tag.

This approach allows for visual updates to be made to the Header and deployed
once to the primary app. All applications that implement the Header App will
receive the update(s) automatically.

## Legacy Header App

The first version of the NYPL Header App was built with Express.js and imported
a separate npm package for the Header component. This version of the Header App
is no longer maintained and should not be used for new implementations. Its
current site is hosted on https://header.nypl.org but SHOULD NOT be used.

- [Legacy Header App Github Repo](https://github.com/NYPL/nypl-dgx-react-header)
- [Legacy Header npm component Github Repo](https://github.com/NYPL/dgx-header-component)

## Support

Any questions, concerns, or feedback should be directed to the Reservoir Design
System team.

## Header App Implementations

Not all NYPL Digital apps are created with React and the embeddable Javascript
approach allows ease of implementation for those apps.

The following script can be used to render the NYPL Header in any app. Because
apps can be implemented in different ways, _where_ the script goes depends on
the app.

```jsx
<style>
   #Header-Placeholder {
      min-height: 62px;
   }
   @media screen and (min-width: 832px) {
      #Header-Placeholder {
         min-height: 130px;
      }
   }
</style>

<!-- .... -->

<div id="Header-Placeholder">
   <div id="nypl-header"></div>
   <script
      src="https://ds-header.nypl.org/header.min.js?containerId=nypl-header"
      async
   ></script>
</div>
```

When working in a Next.js app, the script should be placed in the `_document.js` file.

```jsx
<style>{`
   #Header-Placeholder {
      min-height: 62px;
   }
   @media screen and (min-width: 832px) {
      #Header-Placeholder {
         min-height: 130px;
      }
   }
`}</style>
// ...
<div id="Header-Placeholder">
   <div id="nypl-header"></div>
   <script
      src="https://ds-header.nypl.org/header.min.js?containerId=nypl-header"
      async
   ></script>
</div>
```

## NYPL Footer Component

The NYPL Header App also provides a Footer component that can be used in any app.
Just like the NYPL Header, the Footer is implemented through a script tag. Note
that this script does need placeholder CSS or HTML because it's render on the
bottom of the page. When it loads and render, the user will not see any content
jump on the page.

```jsx
<div id="nypl-footer"></div>
<script src="https://ds-header.nypl.org/footer.min.js?containerId=nypl-footer" async></script>
```
