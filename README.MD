# broccoli-cjs-to-es6

This plugin transform your CommonJS deps making them usable like ES6 modules in Ember.
Many thanks to the [Ember Browserify](https://github.com/ef4/ember-browserify) addon for the idea.

**⚠️ NOTE ⚠️: This project has been quick hacked so it's far from perfect. I assume no responsibilities.**

## Installation

```bash
npm install --save broccoli-cjs-to-es6
```

## Example

Suppose you have 2 cjs packages in `node_modules` called `very-long-package-name` and `simple-pkg`. In a standard node env you would use them like this:

```js
// node env
const veryLongPackageName = require("very-long-package-name");
const simplePkg = require("simple-pkg");
```

If you want to use them in ember just you can do something like this:

```js
const browserifyTree = require("broccoli-cjs-to-es6");

module.exports = {
  name: "awesome-addon",

  treeForVendor(tree) {
    return browserifyTree(tree, {
      modules: [
        {
          module: "very-long-package-name",
          resolution: "short-name"
        },
        "simple-pkg"
      ],
      outputFile: "whatever-file-name.js"
    });
  },

  included(app) {
    app.import("vendor/whatever-file-name.js");
  }
};
```

Then in your Ember app you can access them like this:

```js
import veryLongPackageName from "short-name";
import simplePkg from "simple-pkg";
```
