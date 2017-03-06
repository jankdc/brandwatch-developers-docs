---
title: "Integrating with Vizia"
excerpt: "Once your bundle is built it can be added to Vizia."
---

Eventually, you will want to add your bundle to Vizia. To do that, you'll need two files at minimum: the built JavaScript output when you run [`npm run build`](../tapi-api/package-json.html), and [your `manifest.json` file](../tapir-api/manifest-json.html). A Vizia engineer can take those and add them to the Vizia platform, after which you and others in your organization will have access to a new scene or tile that implements the bundle you created.

That means that, in terms of integration, there isn't much to think about. One thing not covered by your bundle code that may be important, though, are the user options for display. These are the settings on the left-hand side of the preview when you add a scene or tile to your display in Vizia. Some bundles will not require any configuration for use, but others, particularly those using Brandwatch data, will need some additional input to run. Vizia contains a library of these [option views](./option-views.html), which you can add by simply naming them in your `manifest.json` file.

If you need to replace your bundle in Vizia at any point, you can just send your built JavaScript file. You'll only need to send the `manifest.json` or any other assets (e.g. images) if they've changed.
