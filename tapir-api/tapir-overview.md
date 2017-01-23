---
title: "Tapir Overview"
excerpt: "What is Tapir?"
---
Before diving into coding with Tapir, it's helpful to understand what the framework is meant to help you do. A bundle/app allows you to combine a data source or sources, transformations, and/or a destination where the data will be output. The bundle itself is a kind of controller overseeing the composition of those pieces and packaging the whole process up to be used within Vizia. Tapir itself includes a number of off the shelf utilities from each of the three areas of concern (sources, transforms, and destinations), but it also includes more abstract modules you can use as the basis for custom code. To see what a bundle looks like with a bare minimum of custom code, have a look at [the CSV example in Tapir](https://github.com/vizia/tapir/tree/master/examples/csv).

To do something more powerful, you can use custom components in combination with the tools already available in Vizia, or to combine existing tools in a custom configuration. All three types of components are written as separate modules which will be dependencies of your main bundle module. For a bundle with custom modules you've written for each area of concern, a file structure might look like this:
```
/custom-bundle
 |-/destination
    |-/templates
       |-template.hbs
    |-destination-module.js
    |-destination.css
 |-/transforms
    |-date-transform-module.js
    |-text-transform-module.js
 |-bundle.js
 |-source-module.js
 ```
 
Dependency management is even more straight-forward than that. As mentioned, bundles require the other pieces as dependencies. For most of the individual components, it's likely that you'll get some advantage from requiring the Tapir modules and extending their functionality. However, because functionality is piped together, those dependencies shouldn't need to go more than one level deep for most scenarios and modules can remain lightweight. Sources and transforms can easily be stand-alone modules because their work is fairly specific (fetching data from one place or transforming it in a single way, respectively). Destinations are more likely to be composed of other code in addition to the destination module itself if they require display resources such as HTML or CSS.

Tapir is relatively light on convention, but there are a few important things to note about each of these modules to make them work together. One thing that applies to all of them is the way they're composed; they're chained together in the bundle in the order source → transform[s] → destination. The bundle pulls all the pieces together with a series of calls to its `use` method, which it inherits as an instance of a Tapir bundle. It might look like this:
```
var custom_bundle = tapir();
custom_bundle.use( source_module )
  .use( split() )
  .use( date_transform() )
  .use( text_transform() )
  .use( destination_module );
module.exports = custom_bundle;
```

Whether `use` is passed a variable name or function call depends on the structure of the module being called. If the module exports a function named `create` you can reference it with `.use( module_name )` and the framework will do the rest. You'd use `create` if you wanted to pass in the config object when the module was used. Otherwise, you can name your functions anything you like, export what you like, and pass in whatever arguments you need directly from the bundle.

Although data sources can be anything you like, Tapir contains utilities for the most common, arrays and XHRs. Using the array or http sources, you can create a data source with relatively little code. If your data needs further transformation (for example, extracting it from a response object), you can handle that within your source or further down the chain. 

Transform modules are perhaps the most portable piece of a bundle, so they're slightly more likely to exist as functions that act on any data they receive in an agnostic way, not looking for certain external config properties. Because of how bundles are chained together, they're likely to contain something resembling the following pattern (which will quickly become familiar): 
```
module.exports = function() { return transform( function(data) {...} )};
``` 
When the framework calls your transform it will pass its data as it currently exists (so any previous transforms will have been applied).

Because they're the end of our chain of functionality, destinations can be more complicated. If you require the destination utility module as a dependency, you can call that to get a reference to its `fetchData` method. Calling `fetchData` allows you to backtrack all the way to the beginning of the chain with requesting code–beginning with your rendering code in the destination–calling back to the previous step once it's ready to process it. Separating your code into callbacks will work differently depending on what you'd like your destination to do, so it's best to start with tutorial code and then begin to experiment. 

Once you begin to explore [coding a more complex bundle](../tapir-tutorial/1-introduction.html) you may begin to wonder about one more important Tapir convention, the pattern of returning function calls mentioned above. You might have expected that functions would return variables or a framework object. Those latter conventions would work well for creating a tidy chain with static data, but passing callbacks is something we do to support working with streaming data. This way, if we receive additional data from our source it's piped through all the same functionality as the data we had already and then added to our destination. 

Adding your bundle/app to Vizia will require changes to outside configurations; it can't all be done via your own code. However, there are a few things you will do in your bundle directory and/or repo to make it usable. If you don't have one already, you'll need to create a built version of your code, and you'll need to add the location of the built JavaScript to a `manifest.json` file as the `app` property. The rest of the work will need to be done in Vizia itself. Once you have your bundle ready, you can read the [details of how to add it](https://docs.google.com/document/d/1BFhFzcvKBUjPH9Hnp8eHj_AwMSS_9wVRMgwtVQgwtIo/edit).