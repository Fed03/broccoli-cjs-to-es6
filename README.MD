# broccoli-cjs-to-es6

The broccoli-watchify plugin bundles your assets with

## Installation

```bash
npm install --save broccoli-cjs-to-es6
```

## Example

```js
"use strict";
const browserifyTree = require("broccoli-cjs-to-es6");

module.exports = {
  name: "ember-pouch",

  treeForVendor(tree) {
    return browserifyTree(tree, {
      modules: [
        {
          module: "pouchdb-browser",
          resolution: "pouchdb"
        },
        "relational-pouch"
      ],
      outputFile: "pouchdb-browserify.js"
    });
  },

  included(app) {
    app.import("vendor/pouchdb-browserify.js");
  }
};
```

