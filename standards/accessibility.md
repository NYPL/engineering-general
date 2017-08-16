# Accessibility Standards

The Library provides resources that should be accessible to all patrons. When building front-end applications that patrons interact with, we MUST build the applications with the accessibility-first approach. The Library uses [WCAG 2.0, level AA](https://nypl.github.io/design-toolkit/resources/glossary.html#wcag-20) as their conformance guideline for web accessibility.

This is a general overview and the Design Toolkit's [Developer Checklist](https://nypl.github.io/design-toolkit/resources/development-checklist.html) MUST be followed to set a strong foundation for an accessible application. Checking off items from the Developer Checklist does not guarantee that an application is fully accessible.

### Implementation

Applications MUST be fully keyboard navigable.

Applications MUST be built as progressive web applications.

Applications MUST support working with Javascript turned off. This includes making navigation and form submissions work as intended. Enhancements to the applications SHOULD be built afterwards.

Developers SHOULD have a working knowledge of the basics of HTML and CSS. This will go a long way to building applications the correct way from the beginning. This alone covers writing valid HTML, creating valid forms with valid `label`s and `input`s, creating page landmarks, creating valid `img` elements, and so on.

Developers SHOULD build user interfaces (UIs) using the native HTML elements intended for their behavior. For example, a dropdown SHOULD be built using the native `<select>` and `<option>` elements instead of a `<button>` with a list `<ul>` dropdown. Unless it is absolutely necessary, UIs behavior can be built with other HTML, but they MUST work as intended in different browsers.

Developers MUST build applications for users with slow connections in mind. This means having the 'above the fold' CSS and HTML be delivered quickly.

Developers SHOULD write components that provide valid HTML over a framework's implementation. For example, when building a definition list `dl`, the only valid HTML allowed as children are `dt` and `dd`. React cannot return a component in the form of

    <dt>Term</dt>
    <dd>Definition</dd>

and require the developer to wrap those elements in a `div` or `span`. Since this creates invalid HTML, it is preferable to not create a smaller component for that HTML and instead allow it to be part of a bigger component. It is better to write a big and accessible React component than smaller and inaccessible React components.

### Tools

Developers MUST run their applications through web accessibility tools.

Developers SHOULD have repo tools or IDE tools installed to help fix accessibility issues as they code. For example, the [eslint-plugin-jsx-a11y](https://github.com/evcohen/eslint-plugin-jsx-a11y) is an ESLint plugin that can be added to check for errors when running the app's code through ESLint. Some IDEs (Atom, for example), can pick up the configuration and tell you the errors as you code.

A more comprehensive list of tools can be found in the Design Toolkit's [Resources](https://nypl.github.io/design-toolkit/resources/resources.html) section.
