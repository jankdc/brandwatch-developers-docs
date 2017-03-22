---
title: "Welcome to Vizia for Developers"
---
Vizia allows you to display Brandwatch data in a variety of ways, but you can extend it by adding other data sources, displays, and ways of transforming that data. The tiles you see in Vizia are all examples of bundles, and using the Vizia for Developers (V4D) Tapir framework, you can create your own custom bundles. These can be simple reconfigurations of the [modules](./tapir-modules/) that already exist in the V4D toolkit, or entirely new data or displays that you write for your own use.

A bundle is usually composed of a source and a destination, possibly with one or more transforms between them that reorganize the data from the source into the format expected by the destination which displays it. These individual modules are composed into a pipeline by the V4D Tapir framework.

Within Vizia, bundles may be supplied with addition configuration information specific to the installation or display where they'll be shown. V4D also allows you to define the [configuration options](./integrating-with-vizia/option-views.md) administrators will see when using your bundle as a tile.



[What is Tapir?](./tapir-api/tapir-overview.md)

[Quickstart Guides](./quickstarts/)

[Learn to use Tapir](./tapir-tutorial/1-introduction.md)
