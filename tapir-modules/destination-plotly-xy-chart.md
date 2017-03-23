# destination-plotly-xy-chart
A Vizia Tapir wrapped [Plotly.js chart](https://plot.ly/javascript/), suitable for simple charts with non-streaming data.

## Demo
To run the demo run `npm start` and point your browser to the suggested url.

## Usage
```
var bundle = tapir();
var destination = require('@vizia/destination-plotly-xy-chart');

destination = chart.create({
    layout: layoutOpts //options passed to the [Plotly.newPlot method](https://plot.ly/javascript/plotlyjs-function-reference/#plotlynewplot)
});

// bundle source and transformation setup

bundle.use(destination);

```
