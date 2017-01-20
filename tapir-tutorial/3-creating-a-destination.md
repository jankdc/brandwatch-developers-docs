---
title: "3. Creating a Destination"
excerpt: ""
---
Vizia's Tapir framework comes with a whole bunch of destinations out of the box, but for the purposes of this tutorial we'll roll our own.

Our two apps both require two-dimensional charts:

1. The cumulative spend app requires a line chart
2. The categories spending app requires stacked bars

Both charts have fairly similar requirements in that they're displaying typical two dimensional data. With this in mind we'll use [Plotly.js](https://plot.ly/javascript/) to do the heavy lifting.

So, let's dive in and create a Tapir Destination with Plotly. As is customary in this tutorial series, we'll start by looking at the complete finished code:
```javascript
'use strict';

var dom = require('@vizia/tapir/destinations/dom');
var Plotly = require('plotly.js');

var backgroundGrey = '#36363B';
var axisGrey = '#545459';
var offWhite = '#E5E5EA';

function getFontScale(viewport) {
    var vw = viewport.width / 100;
    var vh = viewport.height / 100;
    var vmin = Math.min(vw, vh);

    return vmin * 2;
}

function xyChartDestination(config) {
    var opts = config || {};
    var fontSize = getFontScale(config.viewportUnits || {
        width: window.innerWidth,
        height: window.innerHeight
    });
    var axisLayout = {
        gridcolor: axisGrey,
        linecolor: axisGrey
    };
    var layoutDefaults = {
        paper_bgcolor: backgroundGrey,
        plot_bgcolor: backgroundGrey,
        xaxis: Object.assign({}, axisLayout),
        yaxis: Object.assign({}, axisLayout),
        font: {
            size: fontSize,
            color: offWhite
        },
        legend: {
            font: {
                size: fontSize,
                color: offWhite
            }
        }
    };

    return dom(opts.destTarget, {
        init: function init() {
            this.layout = Object.assign({}, opts.layout, layoutDefaults);
        },
        onData: function onData(data, done) {
            var seriesType = opts.seriesType || 'line';
            var series = data.map(function (d) {
                return Object.assign(d, {type: seriesType});
            });
            var plotlyOPtions = {
                showLink: false,
                displayModeBar: false,
                staticPlot: true // remove the toolbar etc
            };

            Plotly.newPlot(this.element, series, this.layout, plotlyOptions);

            return done();
        }
    });
}

exports.create = xyChartDestination;
```
Pretty straightforward! Let's break down what's happening.

Firstly, we want to display our data in the DOM, so we choose to extend [Tapir's DOM destination](https://github.com/vizia/tapir#dom), overriding its `init` and `onData` methods.

In the `init` method, we set `this.layout`, based on some sensible defaults (defined in `layoutDefaults`), merged with any options passed in to the destination as config.

In the `onData` method things are a touch more complicated. The module has been designed so that the data it uses is typical plotly XY data, as shown below:
```javascript
[{
  name: 'series name',
  x: ['2016-09-01', '2016-09-02', '2016-09-03']
  y: [1, 20, 10]
},{
  ...
}]
```
We can assume that consumers of the destination we're building can use transforms to massage the data into this format (in fact we'll do this later in this tutorial sequence), but it seems reasonable to keep the Plotly-specific work inside this module, so we need to `map` over the incoming data here:
```javascript
var seriesType = opts.seriesType || 'line';
var series = data.map(function (d) {
    return Object.assign(d, {type: seriesType});
});
```
Here we add the `seriesType` property required by Plotly to each provided series that we need to display. We default to the line type, but the bundle config can override this.

Finally, as per the Tapir docs, we need to call `done()` in the onData method to signal that we're ready.

That's it! We've built a very simple destination using Plotly.js

> Remember you can clone the tutorial repo at [https://github.com/vizia/monzo-tapir](https://github.com/vizia/monzo-tapir)