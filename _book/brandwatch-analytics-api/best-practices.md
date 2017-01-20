---
title: "Best practices"
excerpt: "Some hints and tips on how to use the Analytics API."
---
Our clients have been using Brandwatch for a multitude of different use cases. Here are some pointers for how to get the best performance when integrating the Analytics API with your application.
[block:api-header]
{
  "type": "basic",
  "title": "Rate limits"
}
[/block]
API Clients are limited to make 30 calls every 10 minutes. Limits are applied at a Client rather than User level. If you have a use case that doesn't fit within these rate limits, then please get in touch with your account manager to discuss your needs.
[block:api-header]
{
  "type": "basic",
  "title": "Choosing polling times"
}
[/block]
If you are building an integration that uses polling in order to keep a dataset continually up to date, think about the type of data that you are displaying in order to choose appropriate polling times. 

For example, if you were populating a stream of Mentions, then it would make sense to poll fairly frequently (e.g. once every 30 seconds) as new data will be arriving continually. However, if you were populating a chart which breaks down volume by week, then choosing a longer polling time would be more appropriate as the data will not change as significantly.
[block:api-header]
{
  "type": "basic",
  "title": "Concurrency"
}
[/block]
We recommend queuing requests at the client side and executing them linearly, rather than in parallel. Multiple parallel requests may be throttled and take longer to return than a sequence of linearly executed requests.
[block:api-header]
{
  "type": "basic",
  "title": "Experimenting with our API"
}
[/block]
If you're looking to quickly get started with experimenting with our API, there is a [Python utility library](https://github.com/BrandwatchLtd/api_sdk) that has is developed and maintained by our Professional Services team. It's a continual work-in-progress, so please submit pull requests if you have any improvements.