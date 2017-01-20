---
title: "6. Testing a complete bundle"
excerpt: ""
---
So far in this tutorial, we've:

1. Created a `source` to pull data from Monzo bank's transactions API
2. Created a `destination` to chart two-dimensional data
3. Created `transforms` to shape the data from the source into the format we want.
4. Weaved everything together into a complete bundle

In this step we'll look at some of the helpers that Tapir provides in order for us to test how our transformation chain works.

Here's the test code for our bundle:
```javascript
'use strict';

const test = require('tape');
const sinon = require('sinon');

const tapir = require('@vizia/tapir/bundle');
const makeDownstream = require('@vizia/tapir/testHelpers/makeDownstream');

const jsdom = require('jsdom').jsdom;
const doc = jsdom(undefined);
global.window = doc.defaultView;
global.document = doc;

test('the transform pipeline works as expected', assert => {
    const bundle = require('../../bundles/cumulative-spend/bundle')(tapir);
    const config = {
        since: '2016-09-01T00:00:00Z',
        before: '2016-09-03T00:00:00Z',
    };
    const transformedOutput = [];
    const replacementDestination = makeDownstream(transformedOutput);

    const dummyData = [{
        id: 'tx_1234',
        created: '2016-09-01T16:53:34.38Z',
        amount: 10000,
        category: 'mondo',
        include_in_spending: false
    }, {
        id: 'tx_1235',
        created: '2016-09-01T20:00:00Z',
        amount: -1000,
        category: 'shopping',
        include_in_spending: true
    }, {
        id: 'tx_1236',
        created: '2016-09-01T20:00:00Z',
        amount: -1000,
        category: 'holidays',
        include_in_spending: true
    }, {
        id: 'tx_1237',
        created: '2016-09-01T21:00:00Z',
        amount: -1500,
        category: 'shopping',
        include_in_spending: true
    }, {
        id: 'tx_1238',
        created: '2016-09-02T09:00:00Z',
        amount: -1000,
        category: 'eating_out',
        include_in_spending: true
    }];

    const expectedOutput = [{
        name: 'total',
        x: [ '2016-09-01', '2016-09-02', '2016-09-03' ],
        y: [ 35, 45, 45 ]
    }];

    bundle.testPipeline(config, dummyData, replacementDestination);

    assert.deepEqual(transformedOutput, [expectedOutput]);
    assert.end();
});
```
Let's look at the most important things to note.
```javascript
const jsdom = require('jsdom').jsdom;
const doc = jsdom(undefined);
global.window = doc.defaultView;
global.document = doc;
```
The above code, at the start of our tests, exists in order to provide a fake DOM environment for our destination. We'll be executing the tests in node, using `tape` so we need to hang a fake window and document off the `global` object. This isn't great, but as we'll see shortly we dont use the DOM in our test anyway.
```javascript
const bundle = require('../../bundles/cumulative-spend/bundle')(tapir);
const config = {
    since: '2016-09-01T00:00:00Z',
    before: '2016-09-03T00:00:00Z',
};
const transformedOutput = [];
const replacementDestination = makeDownstream(transformedOutput);
```
Here we start to set up our test, by requiring in the bundle and setting some dummy config. Then, importantly, we start to use Tapir's test helpers.

We define an empty array, `transformedOutput`, that will ultimately contain the output of our transformation pipeline, and then use the tapir `makeDownstream` module to create a new destination that we'll shortly use to replace the destination in our bundle.
```javascript
const dummyData = [{
    id: 'tx_1234',
    created: '2016-09-01T16:53:34.38Z',
    amount: 10000,
    category: 'mondo',
    include_in_spending: false
}, {
    id: 'tx_1235',
    created: '2016-09-01T20:00:00Z',
    amount: -1000,
    category: 'shopping',
    include_in_spending: true
}, {
    id: 'tx_1236',
    created: '2016-09-01T20:00:00Z',
    amount: -1000,
    category: 'holidays',
    include_in_spending: true
}, {
    id: 'tx_1237',
    created: '2016-09-01T21:00:00Z',
    amount: -1500,
    category: 'shopping',
    include_in_spending: true
}, {
    id: 'tx_1238',
    created: '2016-09-02T09:00:00Z',
    amount: -1000,
    category: 'eating_out',
    include_in_spending: true
}];

const expectedOutput = [{
    name: 'total',
    x: [ '2016-09-01', '2016-09-02', '2016-09-03' ],
    y: [ 35, 45, 45 ]
}];
```
Above we set up some dummy data in `const dummyData` that mirrors the data we expect our source to emit.

Then we define `const expectedOutput` with the data that we expect our transformation pipeline to emit, when supplied with `dummyData`.
```javascript
bundle.testPipeline(config, dummyData, replacementDestination);
```
Above we act on our test setup, using Tapir's `testPipeline` method. This is a non-destructive method call that will execute the transform pipeline defined in `bundle.js` but with the provided dummy data instead of our `source`, and with the `makeDownstream` test destination instead of our bundle's destination.
```javascript
assert.deepEqual(transformedOutput, [expectedOutput]);\nassert.end();
```
Above we simply assert that the bundle took the dummy data and transformed it as expected. Note that expectedOutput should be encapsulated in an array in this case. This is because our destination expects an array of plotly series.

> Remember you can clone the tutorial repo at [https://github.com/vizia/monzo-tapir](https://github.com/vizia/monzo-tapir)