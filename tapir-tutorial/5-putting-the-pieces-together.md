---
title: "5. Putting the pieces together"
excerpt: ""
---
So far in this tutorial, we've:

1. Created a `source` to pull data from Monzo bank's transactions API
2. Created a `destination` to chart two-dimensional data
3. Created `transforms` to shape the data from the source into the format we want.

The next step is to put all the pieces together and create our finished bundle. The bundle essentially takes each piece we've created, defines some config, and stitches it all together into something Vizia can consume as a `scene`.

Let's look at the main bundle code:
```javascript
'use strict';

var concat = require('@vizia/tapir/transforms/concat');
var monzoTransactions = require('monzo-transactions-source');
var removeCreditsFilter = require('./transforms/removeCreditsFilter');
var toDailyTotals = require('./transforms/toDailyTotals');
var xyChartDestination = require('vizia-plotly-xy-chart-destination');

module.exports = function createBundle(tapir) {
    var bundle = tapir();

    bundle.use(monzoTransactions);
    bundle.use(removeCreditsFilter);
    bundle.use(concat);
    bundle.use(toDailyTotals);

    bundle.use(xyChartDestination);

    return bundle;
};
```
Nice and simple! There's a couple of things to highlight, as ever:

1. We use the dependency injection pattern to pass the `tapir` library in. As we shall see later on, this makes testing much simpler as we can stub/mock tapir.

2. `bundle.use` tells Tapir to add a module to the pipeline. The order is important. The first call will be interpreted as a source.

We also need an entry point for our app, so we can easily run it whilst we develop it:
```javascript
'use strict';

var tapir = require('@vizia/tapir/bundle');
var bundle = require('./bundle')(tapir);

bundle.set('destTarget', '#chart');

var config = {
    accountId: '[our monzo account id]',
    userId: '[our monzo user id]',
    since: '2016-09-01T00:00:00Z', // start date for the visualisation
    before: '2016-09-14T00:00:00Z', // end date for the visualisation
    accessToken: '[our monzo oAuth token]'
};

bundle.load(config);

bundle.start();
```
When we're running inside Vizia, the `config` object will be supplied by Vizia itself, but this is a convenient pattern for development outside of Vizia.

Additionally, when we're running in Vizia, the DOM element will be supplied to our bundle automatically, but here we need to specify an element ourselves with `bundle.set`

Note also that we require `tapir` here instead of in `bundle.js` and inject it as a dependency of `bundle`.

> Remember you can clone the tutorial repo at [https://github.com/vizia/monzo-tapir](https://github.com/vizia/monzo-tapir)