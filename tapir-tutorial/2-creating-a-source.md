---
title: "2. Creating a Source"
excerpt: ""
---
Both apps that we wish to create consume the Monzo api's [`/transactions`](https://monzo.com/docs/#list-transactions) endpoint. Below is the [httpie](https://httpie.org/) command to view this endpoint.

```shell
http "https://api.monzo.com/transactions" \
    "Authorization: Bearer $access_token" \
    "account_id==$account_id"
```
We expect JSON data back in the following format:
```json
{
    "transactions": [
        {
            "account_balance": 13013,
            "amount": -510,
            "created": "2015-08-22T12:20:18Z",
            "currency": "GBP",
            "description": "THE DE BEAUVOIR DELI C LONDON        GBR",
            "id": "tx_00008zIcpb1TB4yeIFXMzx",
            "merchant": "merch_00008zIcpbAKe8shBxXUtl",
            "metadata": {},
            "notes": "Salmon sandwich 🍞",
            "is_load": false,
            "settled": "2015-08-23T12:20:18Z",
            "category": "eating_out"
        },
        {
            "account_balance": 12334,
            "amount": -679,
            "created": "2015-08-23T16:15:03Z",
            "currency": "GBP",
            "description": "VUE BSL LTD            ISLINGTON     GBR",
            "id": "tx_00008zL2INM3xZ41THuRF3",
            "merchant": "merch_00008z6uFVhVBcaZzSQwCX",
            "metadata": {},
            "notes": "",
            "is_load": false,
            "settled": "2015-08-24T16:15:03Z",
            "category": "eating_out"
        },
    ]
}
```
Making a Tapir source that consumes JSON over HTTP is super-easy, as the framework supplies both a `http` source and a `json` transform. Let's look at what the finished source will look like, and then break it down and explain how it fits together.
```javascript
'use strict';

var http = require('@vizia/tapir/sources/http');
var json = require('@vizia/tapir/transforms/json');
var MONDO_API_URL = 'https://api.getmondo.co.uk';

function create(config) {
    // set up a tapir transform that parses the `transaction` property from
    // the response JSON.
    var parse = json('transactions.*');
    var url = MONDO_API_URL + '/transactions?account_id=' + config.accountId;

    // optional config to set an end date for the transactions
    if (config.before) {
        url = url + '&before=' + config.before;
    }

    // optional config to set a start date for the transactions
    if (config.since) {
        url = url + '&since=' + config.since;
    }

    // optional config to hydrate the `merchant` property in each transaction
    if (config.fetchMerchantDetails) {
        url = url + '&expand[]=merchant';
    }

    // set up the oAuth 2.0 Header.
    var options = {
        headers: {
            Authorization: 'Bearer ' + config.accessToken
        }
    };

    // expose a composed method to execute the request and transform
    // the resulted json into a tapir stream of transaction objects
    return parse(http(url, options));
}

exports.create = create;

```
Nice! The code is pretty straightforward, as all the heavy-lifting is done by Tapir. Having said that, there's a couple of things to highlight:

1. We set up the transform for the json (in the `var parse`) *inside* the scope of the `create` function. This is important as the internal buffer for the transform needs to be scoped to the function.

2. By exposing a create property on the exports, the Tapir framework knows that we are expecting it to supply the bundle config to the exported function. This is a convention across Tapir, so bear it in mind whenever you need runtime config in your sources, transforms or destinations.

## Testing our Source

A really nice way to test HTTP sources is using the [`nock`](https://github.com/node-nock/nock) http mocking and expectations library. Nock allows us to set up expectations for the exact format of the outgoing request, as well as specify a dummy response.

In the tests below we're using `tape`, a very lightweight TAP-compliant testing library that we can execute from the command line.

If you're coding along with this tutorial, make sure to:

Let's look at some code that does the initial test suite setup: 
```javascript
'use strict';

const transactions = require('../lib/transactions');
const MONDO_API_URL = 'https://api.getmondo.co.uk:443';

const jsonResponse = require('./fixtures/transactions.json');

const test = require('tape');

const nock = require('nock');
nock.disableNetConnect();

const XMLHttpRequest = require('xhr2').XMLHttpRequest;
global.XMLHttpRequest = XMLHttpRequest;
```

> Note that in the tests above we rely on the `xhr2` module. This is because we're executing our tests in node, and there's no `window` object. Tapir's `http` module uses `window.XMLHttpRequest` under the hood so we use `xhr2` here and hang it off the `global` object whilst the tests run.
> If you're coding along with this tutorial, make sure to `npm install nock tape xhr2 --save-dev` to install these dev dependencies.

Here's our first test:
```javascript
test('creates a function when passed config', assert => {
    const config = {};
    const source = transactions.create(config);

    assert.equal(typeof source, 'function', 'should create function');
    assert.end();
});
```
This is pretty much a self-explanatory smoke test.

Other things we should test in this suite are:

1. Appending the expected request parameters to the Monzo api call, based on the supplied Config
2. Making sure we add in the oAuth header 
3. Checking that we parse the transactions out of the JSON response

Let's look at testing the config's effect on the api call next:
```javascript
test('calls the mondo api transactions endpoint with the account id', assert => {
    const config = {
        accountId: 'accountId'
    };

    const scope = nock(MONDO_API_URL, { encodedQueryParams : true })
        .get('/transactions')
        .query({ account_id: config.accountId })
        .reply(200, jsonResponse);

    const source = transactions.create(config);

    source(null, (end, data) => {
        assert.true(scope.isDone(), 'request made');
        assert.end();
    });
});

test('calls the mondo api transactions endpoint with the before date', assert => {
    const config = {
        accountId: 'accountId',
        before: '2016-08-01T23:00:00Z'
    };

    const scope = nock(MONDO_API_URL, { encodedQueryParams : true })
        .get('/transactions')
        .query({
            account_id: config.accountId,
            before: config.before
        })
        .reply(200, jsonResponse);

    const source = transactions.create(config);

    source(null, (end, data) => {
        assert.true(scope.isDone(), 'request made');
        assert.end();
    });
});

test('calls the mondo api transactions endpoint with the since date', assert => {
    const config = {
        accountId: 'accountId',
        since: '2016-08-01T23:00:00Z'
    };

    const scope = nock(MONDO_API_URL, { encodedQueryParams : true })
        .get('/transactions')
        .query({
            account_id: config.accountId,
            since: config.since
        })
        .reply(200, jsonResponse);

    const source = transactions.create(config);

    source(null, (end, data) => {
        assert.true(scope.isDone(), 'request made');
        assert.end();
    });
});

test('expands merchants if config specifies', assert => {
    const config = {
        accountId: 'accountId',
        since: '2016-08-01T23:00:00Z',
        fetchMerchantDetails: true
    };

    const scope = nock(MONDO_API_URL, { encodedQueryParams : true })
        .get('/transactions')
        .query({
            account_id: config.accountId,
            since: config.since,
            expand: ['merchant']
        })
        .reply(200, jsonResponse);

    const source = transactions.create(config);

    source(null, (end, data) => {
        assert.true(scope.isDone(), 'request made');
        assert.end();
    });
});
```

Next let's test we added the oAuth header from the config:
```javascript
test('calls the mondo api transactions endpoint with the oauth token header', assert => {
    const config = {
        accountId: 'accountId',
        accessToken: 'coole-token'
    };

    const scope = nock(MONDO_API_URL, { encodedQueryParams : true })
        .matchHeader('Authorization', 'Bearer ' + config.accessToken)
        .get('/transactions')
        .query({
            account_id: config.accountId
        })
        .reply(200, jsonResponse);

    const source = transactions.create(config);

    source(null, (end, data) => {
        assert.true(scope.isDone(), 'request made');
        assert.end();
    });
});
```
Finally, lets' add a test to ensure we parsed the transaction objects out of the response JSON:
```javascript
test('returns parsed Monzo transaction objects', assert => {
    const config = {
        accountId: 'accountId'
    };

    const scope = nock(MONDO_API_URL, { encodedQueryParams : true })
        .get('/transactions')
        .query({
            account_id: config.accountId
        })
        .reply(200, jsonResponse);

    const source = transactions.create(config);

    source(null, (end, data) => {
        const expected = jsonResponse.transactions[0];
        const actual = data;

        assert.true(scope.isDone(), 'request made');
        assert.equal(actual, data, 'responded with JSON');

        assert.end();
    });
```
Great! Now we have a completed Tapir Source that's ready to use in our bundles.

> Remember you can clone the tutorial repo at [https://github.com/vizia/monzo-tapir](https://github.com/vizia/monzo-tapir)