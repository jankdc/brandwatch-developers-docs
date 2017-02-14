---
title: "The manifest.json file"
excerpt: ""
---

To demo a bundle in a local environment, you typically don't need to do more than run it. However, you'll eventually want to create bundles for use in Vizia. Your bundle will be added to Vizia via its `manifest.json` file. Vizia will examine that manifest to see where your runnable bundle code is, as well as any additional information you've supplied. 

A basic `manifest.json` can be very simple:
```
{
    "browserScripts": [],
    "app": "your-new-bundle/bundle.js"
}
```

The following parameters may be used in `manifest.json`, in any order:

## app : `string` (required)
The location of your built and runnable bundle code. Usually this file will be in the top level of your bundle's directory, so the complete string will take the form `your-bundle-name/bundle.js` or similar. the path is short because your bundle is either copied or linked to a directory within Vizia, so all other path information is set elsewhere.

## auths : `array` of `object`s
An auth token or tokens needed to run the bundle.
   ### provider : `string`
   The name of the token provider, e.g. `"salesforce"`.
   ### clientId : `string`
   An ID that identifies the user to this authentication provider.
   ### clientSecret : `string`
   The password, API key, or other authentication mechanism that verifies this user's identity.
   ### scopes : `array`
   Strings representing the various scopes for which this auth token should be used. 
   ### tokenTTLSeconds : `integer`
   The number of seconds the token remains active.

## browserScripts : `array` (required)
Full paths to scripts to be included on the rendered page, as strings. These can be local files or scripts stored on a CDN.

## config : `object`
Key/value pairs to be added to the bundle's config object, as though the `set` method had been used.

## name : `string`
The optional bundle name. If supplied, this should match the name used in the path of the `app` property.

## optionViewConfig : `array` of `object`s
The option views that will be rendered for user input of bundle settings, in the order provided.
   ### name : `string`  
   The name of the option view to render. This can be the filename of any of the [existing option views](https://github.com/BrandwatchLtd/vizia/tree/master/admin2/public/js/views/optionviews) without the `.js` file extension or path. 
   ### settings : `object`  
   Additional properties currently only required for the `generateCustomComponentOptionsView` option view.
      #### allowedValues : `array` of `string`s  
      The options to show in a `select` dropdown. The value supplied will function as both label and value.
      #### label : `string`  
      The label for the input field that should be displayed to the user.
      #### inputType : `string`  
      One of the standard HTML input types, such as `text` or `date`. This can also be used to generate custom non-input types, which are: `select`, `googleAnalyticsViewID`, `location`, and `weatherUnits`.
      #### paramName : `string`  
      What property name should be used to reference the user's input when it's made available to the bundle on the `config.scene.options` object.

