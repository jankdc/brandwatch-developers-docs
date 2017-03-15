---
title: "Quickstart: consuming a public API"
---

To understand how to quickly build a bundle, it helps to have simple requirements. If the data your bundle will consume comes from a publicly-accessible API, API keys are one less thing you need to worry about. If a destination module already exists for the way you want to display your data, the only work you'll need to do is transforming the data into the format the destination requires.

In this example we'll create a bundle that outputs its data the to [Big Number destination](https://github.com/vizia/destination-big-number), but the code you write can be the basis for any other destination you want to use in combination with a public API.

To start, create a new directory for your module and add a [package.json](../tapir-api/package-json.html) file. If you know all your dependencies, you can specify those in `package.json` and save time just running `npm install` to install everything at once. For this example, we'll need to add one more dependency not covered in the `package.json` linked above, so it's also necessary to run `npm install --save vizia/destination-big-number`.

Now we can begin to write code in a new file, `bundle.js`.

The first thing we'll add are our dependencies. Bundles are meant to be small files that pull in small modules they chain together to provide their logic. So the dependencies we define at the top are really a quick summary of what logic our bundle is going to perform. For our example, we'll need to use Tapir (which takes care of combining the bundle logic), a generic helper to [get JSON from an XHR](https://github.com/vizia/tapir/tree/master/sources/json-http), and the destination that will provide the display, `destination-big-number`.

```
var tapir = require("@vizia/tapir/bundle"),
    json = require("@vizia/tapir/sources/json-http"),
    bignumber = require("@vizia/destination-big-number");
```

Next we can create an instance of a bundle. While we're at it, we may as well define a settings object to provide to our data source, too. Since it's passed in when the source is added to the bundle and not used by any other modules in our chain, it's fine to just declare it locally. If we wanted to pass it around, however, we could add it to the bundle's config object using `bundle.set`.

```
var bundle = tapir(),
    sourceOptions = {
        throttle: 60000
    };
```

Once all our variables are set up we can compose our chain. Calls to `bundle.use` are run in the order given, so data sources are always used first, and destinations are always used last. The `json-http` module handles creating the actual XHR for us, informed by the options we pass it, so the only other thing we need to supply is the URL of the API we want to call.

```
bundle.use(json("http://api.fixer.io/latest?base=USD&symbols=GBP", sourceOptions));
```

The API we passed in will provide us some information about the value of the British Pound against the US Dollar. We can't use it directly, though. First, we need to get the property containing the actual exchange rate from the JSON we've been provided and return it with the correct key. Next, since `destination-big-number` is biased toward integers, we'll multiply by 100 to show the number of pence in a dollar instead of a decimal. This transformation is specific to this combination of API data and destination, so instead of getting it from a module we'll create it inline with a new function.

```
bundle.use(function getNumber(row) {
    return {
        value: (row.rates.GBP * 100)
    };
});
```

Finally, we'll end our chain of functionality by using our destination. Since it's the last thing we'll do, it's also a good place to remember to export our bundle.

```
bundle.use(bignumber);

module.exports = bundle;
```

And there we have it, a functional bundle using real data. Because bundles are meant to run in the browser, you can test them very easily with a script defined in `package.json`. A bare bones test could be the following `demo.js`, which just calls `load` and `start` on our bundle, passing it a minimal config object:

```
var bundle = require("./bundle");
bundle.load({
    destTarget: "body" // the DOM element where the output will be attached
});
bundle.start();
```

To check that it works, you can run `npm run start` from the terminal in your directory and go to the local IP address it provides in your browser.

Here's what the full example `bundle.js` we wrote looks like:
```
var tapir = require("@vizia/tapir/bundle"),
    json = require("@vizia/tapir/sources/json-http"),
    bignumber = require("@vizia/destination-big-number");

var bundle = tapir(),
    sourceOptions = {
        throttle: 60000
    };

bundle.use(json("http://api.fixer.io/latest?base=USD&symbols=GBP", sourceOptions));
bundle.use(function getNumber(row) {
    return {
        value: (row.rates.GBP * 100)
    };
});
bundle.use(bignumber);

module.exports = bundle;
```

If this were a real bundle we wanted to add to Vizia, the only thing left to do would be [integrate it with the platform](../integrating-with-vizia/). If you want to try a more complicated bundle first, continue on to the [full tutorial](../tapir-tutorial/1-introduction.html).
