---
title: "Tutorial: polling for new Mentions"
excerpt: "How to write a program that continually gets the latest mentions for your query."
---
A common integration use case is to continually populate a display with Mentions from a Brandwatch Query. This, for example, is something that we ourselves do in some of our [Vizia](https://www.brandwatch.com/brandwatch-vizia/) tiles.

The behaviour that we want to achieve is as follows:
1. On application start up, we want to retrieve the latest 100 mentions.
2. At every polling interval, we want to get the latest mentions since the last time that we polled.

In this tutorial we will assume that the application has already [logged in](doc:logging-in) and has a token. 
[block:api-header]
{
  "type": "basic",
  "title": "Getting the latest 100 mentions"
}
[/block]
When our application runs for the first time, we want to get the latest 100 mentions for our query. We use the following parameters to achieve this:
[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Value",
    "h-2": "Reasoning",
    "0-0": "`pageSize`",
    "1-0": "`page`",
    "2-0": "`orderBy`",
    "3-0": "`orderDirection`",
    "0-1": "100",
    "1-1": "0",
    "2-1": "`id`",
    "3-1": "`desc`",
    "0-2": "This returns 100 Mentions per request.",
    "1-2": "This sets the page market to the latest page, which is indexed from 0.",
    "2-2": "This orders the Mentions by their `resourceId`, which is a global counter incremented for every new Mention that we crawl.",
    "3-2": "This changes the sort direction to descending, ensuring that the newest result is returned first."
  },
  "cols": 3,
  "rows": 4
}
[/block]
Here is the request as a cURL command.
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/289733322/data/mentions?queryId=348973733&startDate=2016-05-01&endDate=2016-05-02&pageSize=100&page=0&orderBy=id&orderDirection=desc",
      "language": "curl"
    }
  ]
}
[/block]
This will return a list of Mentions, newest first. The following example response has had the Mentions removed for brevity.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"resultsTotal\": 99,\n  \"resultsPage\": 0,\n  \"resultsPageSize\": 100,\n  \"results\": [...],\n  \"maximumId\": 100057070129,\n  \"maximumIdInResult\": 100057070129,\n  \"startDate\": \"2016-05-01T00:00:00.000+0000\",\n  \"endDate\": \"2016-05-02T00:00:00.000+0000\"\n}",
      "language": "json"
    }
  ]
}
[/block]
Each page of Mentions contains a `maximumIdInResult` field, which is the latest `id` of a Mention in your result. In your application, parse this value and store it. You will then use it in the next call to get all new Mentions from that point onwards.
[block:api-header]
{
  "type": "basic",
  "title": "Polling for new mentions"
}
[/block]
Having parsed the `maximumIdInResult` field, you are now ready to request all of the Mentions that have matched your Query that have an `id` greater than `100057070129`. To do that, we will be using the `sinceId` parameter.
[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Value",
    "h-2": "Reasoning",
    "0-0": "`sinceId`",
    "0-1": "100057070129",
    "0-2": "Retrieve all Mentions that have an `id` greater than 100057070129."
  },
  "cols": 3,
  "rows": 1
}
[/block]
We then add this to our new request:
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/289733322/data/mentions?queryId=348973733&startDate=2016-05-01&endDate=2016-05-02&pageSize=100&page=0&orderBy=id&orderDirection=desc&sinceId=100057070129",
      "language": "curl"
    }
  ]
}
[/block]
This then returns the newest 100 mentions since we last polled. Repeat this process in order to continually poll for new Mentions in your integration.