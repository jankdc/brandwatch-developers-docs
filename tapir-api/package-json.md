---
title: "Example package.json"
excerpt: ""
---

For your first bundle, it may be easier to start by adding a `package.json` file and running `npm init`, rather than installing all the dependencies you may need manually. You can save this JSON and use it mostly as-is, editing the information in all caps:

```json
{
  "name": "YOUR-BUNDLE-NAME",
  "version": "1.0.0",
  "description": "DESCRIPTION OF YOUR BUNDLE",
  "main": "demo.js",
  "scripts": {
    "start": "wzrd demo.js",
    "build": "browserify -e ./bundle.js -s bundle -o build.js"
  },
  "author": "YOUR NAME",
  "license": "ISC",
  "devDependencies": {
    "browserify": "^13.3.0",
    "wzrd": "^1.5.0"
  },
  "dependencies": {
    "@vizia/tapir": "github:vizia/tapir#v3.x",
    "browserify-css": "^0.9.2",
    "handlebars": "^4.0.6",
    "hbsfy": "^2.7.0",
    "vizia": "github:brandwatchltd/vizia",
    "vizia-css": "github:vizia/vizia-css"
  }
}
```

> Feel free to modify the versions as necessary for your code, those above are simply the versions as of this writing.

The basic dependencies serve one of three functions:
  1. development (build the front-end code and run a test server)
  2. Tapir and Vizia
  3. display (templating and CSS)

For a simple test bundle, you can use the sources, transforms, and destinations that are part of Tapir itself. To do something more complex, you'll need to add other modules. You can write these yourself and keep them with your bundle, or you can install a generic source or destination from NPM to build upon. 
