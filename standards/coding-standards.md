# Coding Standards

Apps MAY enforce a rigorous coding style.  
Different languages have different opinions about uniformity.

If a project wants to enforce a style - it SHOULD be called
out in a conspicious way (e.g. its README) **and** enforced
via the project's test suite.

**Example:**

A JavaScript application is meant to conform to [standardjs](https://standardjs.com/), its test suite SHOULD
fail if `standard` fails.

One way of doing this is by using something like this in `package.json`:  

```javascript
// ...snip
"scripts": {
    "test": "./node_modules/.bin/standard && ./node_modules/.bin/mocha test",
    "start": "node app.js"
  },
// ...snip
```
