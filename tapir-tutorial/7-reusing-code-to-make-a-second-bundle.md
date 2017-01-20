---
title: "7. Reusing code to make a second bundle"
excerpt: ""
---
In the previous steps of the tutorial we completed our app bundle to show the cumulative daily spend from our Monzo bank account. In this step we'll look at how easy it is to re-use some of the modules in order to create a second app, this time breaking down spending by category.

Let's look at the completed bundle, then what's changed.
```javascript
'use strict';

var concat = require('@vizia/tapir/transforms/concat');
var monzoTransactions = require('../../sources/transactions');
var removeCreditsFilter = require('../../transforms/removeCreditsFilter');
var groupByCategory = require('../../transforms/groupByCategory');
var toPlotlySeries = require('../../transforms/groupedTransactionstoPlotlyXy');
var xyChartDestination = require('../../destinations/plotlyXyChartDestination');

module.exports = function createBundle(tapir) {
    var bundle = tapir();

    bundle.use(monzoTransactions);
    bundle.use(removeCreditsFilter);
    bundle.use(concat);
    bundle.use(groupByCategory);
    bundle.use(toPlotlySeries);

    bundle.set('destTarget', '#chart');
    bundle.set('layout', {barmode: 'stack'});
    bundle.set('seriesType', 'bar');

    bundle.use(xyChartDestination);

    return bundle;
};
```
Nice, there's a whole bunch of modules that we're going to reuse:

1. The `monzoTransactions` source
2. The `removeCreditsFilter` transform
3. The `xyChartDestination` destination

We introduce two new transforms, `groupByCategory` and `groupedTransactionstoPlotlyXy` to transform our data into the new format plotly needs in order to display the stacked bar:
```javascript
'use strict';

module.exports = function groupByCategory(data) {
    return data.reduce(function (memo, transaction) {
        var category = transaction.category;

        if (!memo[category]) {
            memo[category] = [];
        }

        memo[category].push(transaction);

        return memo;
    }, {});
};
```
The `groupByCategory` transform does exactly what its name implies - reduces over the array of transactions and returns an object keyed by each transaction's `category` property.
```javascript
'use strict';

var createDatesArray = require('../util/makeDatesArray');

function getDailyTotals(transactions, dates) {
    var keyedByDate = dates.reduce(function (catMemo, date) {
        catMemo[date] = 0; // fill each day with zeroes - we can overwrite later if need be.
        return catMemo;
    }, {});

    transactions.reduce(function (memo, transaction) {
        var dateStr = transaction.created.slice(0, 10);

        memo[dateStr] += Math.abs(transaction.amount / 100);
        return memo;
    }, keyedByDate);

    return Object.keys(keyedByDate).map(function (date) {
        return keyedByDate[date];
    });
}

function createColumns(transactionDataByCategory, dates) {
    var categoryNames = Object.keys(transactionDataByCategory);
    return categoryNames.map(function (category) {
        var categoryTransactions = transactionDataByCategory[category];

        return {
            name: category,
            x: dates,
            y: getDailyTotals(categoryTransactions, dates)
        };
    });
}

exports.create = function (config) {
    return function (data) {
        var dates = createDatesArray(config.since, config.before);
        return createColumns(data, dates);
    };
};
```
The `groupedTransactionstoPlotlyXy` transaction takes the object keyed by transaction and turns it into the format plotly expects, an array of series of XY data, with X as the transaction day, and the Y the total amount for transactions of a given category.
```javascript
bundle.set('layout', {barmode: 'stack'});
bundle.set('seriesType', 'bar');
```
The final change we make is to instruct the `plotlyXyChartDestination` to display a stacked bar. We do this by specifying the properties above.

That's it! In ~100 lines of JS we've made a second bundle by reusing a bunch of code from the first.

Happy coding!

> Remember you can clone the tutorial repo at [https://github.com/vizia/monzo-tapir](https://github.com/vizia/monzo-tapir)