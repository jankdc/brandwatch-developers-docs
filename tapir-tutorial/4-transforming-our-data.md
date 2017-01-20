---
title: "4. Transforming our Data"
excerpt: ""
---
So far in this tutorial, we've:

1. Created a `source` to pull data from Monzo bank's transactions API
2. Created a `destination` to chart two-dimensional data

In this part of the tutorial we'll look at creating transforms, which are small modules that reshape the data as it travels from the source to the destination.

Let's concentrate on the transforms we need for our first app, the app that displays cumulative daily spending.

We know that our source simply lists any transactions between two specific points in time, and we know that our destination expects data in a specific format. So, we can deduce that we need to transform the data as follows:

1. Filter the data so that we only show spending (ie remove account credits)
2. Group the data by day, and reduce over each day to calculate the sum of spending for that day, added to the previous day.
3. Transform the final aggregated data into the format required by the destination

We can do this with three transforms chained together:

1. A custom `filter` transform that removes items that are credits
2. A `concat` transform from the tapir library that collapses the stream of transactions into one large array
3. A final custom transform that performs the aggregation and massages the data into the format our destination requires.

Let's have a look at the two custom transforms:
```javascript
'use strict';

var filter = require('@vizia/tapir/transforms/filter');

module.exports = filter(function (item) {
    return item.amount < 0;
});
```
That's a very simple transform! All we need to do is use Tapir's [filter](https://github.com/vizia/tapir#viziatapirtransformsfilter) module, and specify the function to filter the data. In our case, we're interested in data where `amount` is less than zero, as positive amounts in Monzo's api indicate an account credit.

Next up let's look at the final transform to aggregate the data:
```javascript
'use strict';

var createDatesArray = require('make-dates-array');

exports.create = function (config) {
    return function (data) {
        // createDatesArray just creates an array of dates between since and            // before in YYYY-MM-DD format
        var dates = createDatesArray(config.since, config.before);
  
        // transaction.created is an ISO date string
        // so truncate it to YYYY-MM-DD
        var totalsByDay = data.reduce(function (memo, transaction) {
            
            var dateStr = transaction.created.slice(0,10);
            var amount = Math.abs(transaction.amount / 100);

            memo[dateStr] = (memo[dateStr] || 0) + amount;

            return memo;
        }, {});

        return [{
            name: 'total',
            x: dates,
            y: dates.reduce(function(memo, date, idx){
                var dateStr = getDateKey(date);
                var total = totalsByDay[dateStr] || 0;

                memo[idx] = total += (idx === 0 ? 0 : memo[idx - 1]);
                return memo;
            }, [])
        }];
    };
};
```
There's a bit more going on here. The code is pretty self explanatory, but there's a couple of things we should highlight:

1. This transform exports an object with a `create` property. As we saw in the initial part of this tutorial when we created the `source` module, exposing a create property from a module lets Tapir know that this module needs bundle-level config. We use this config here to understand the date range that we're working with.

2. We want to `reduce` over all of the data supplied from the source in one go in order to perform our aggregation, so we can't chain this transform right off the back of the `removeCreditsFilter` transform. We need to use a Tapir `concat` transform to collapse the stream from the source. We can discuss this further in the next part of this tutorial series.

> Remember you can clone the tutorial repo at [https://github.com/vizia/monzo-tapir](https://github.com/vizia/monzo-tapir)