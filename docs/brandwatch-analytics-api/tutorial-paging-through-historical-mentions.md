---
title: "Tutorial: paging through historical Mentions"
excerpt: "Downloading data from your query by paging through it."
---
Another common integration use case is to request pages of Mentions within a date range and then page through them all. You may want to use this approach if you want to download a substantial dataset from your Query into your own integration.

In this tutorial, we'll take the following approach:
1. We will request for a batch of Mentions across a specified date range.
2. We will then use the paging functionality to access historical data.

In this tutorial we will assume that the application has already logged in and has a token.
[block:api-header]
{
  "type": "basic",
  "title": "Requesting Mentions for a given date range"
}
[/block]
In a similar manner to the other tutorial on [polling for new Mentions](doc:tutorial-polling-for-new-mentions), we'll begin by requesting the newest page of Mentions within a date range. 

We'll use the following parameters to achieve this:
[block:parameters]
{
  "data": {
    "h-0": "Parameter",
    "h-1": "Value",
    "h-2": "Reasoning",
    "0-0": "`pageSize`",
    "0-1": "100",
    "0-2": "This returns 100 Mentions per request. You can change this to a value that suits you. We do not recommend getting more than 5000 at a time.",
    "1-0": "`page`",
    "1-1": "0",
    "1-2": "This sets the page market to the latest page, which is indexed from 0.",
    "2-0": "`orderBy`",
    "2-1": "`id`",
    "2-2": "This orders the Mentions by their `resourceId`, which is a global counter incremented for every new Mention that we crawl.",
    "3-0": "`orderDirection`",
    "3-1": "`desc`",
    "3-2": "This changes the sort direction to descending, ensuring that the newest result is returned first."
  },
  "cols": 3,
  "rows": 4
}
[/block]
Here is the request as a cURL command:
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
      "code": "{\n  \"resultsTotal\": 9982,\n  \"resultsPage\": 0,\n  \"resultsPageSize\": 100,\n  \"results\": [...],\n  \"maximumId\": 100057070129,\n  \"maximumIdInResult\": 100057070129,\n  \"startDate\": \"2016-05-01T00:00:00.000+0000\",\n  \"endDate\": \"2016-05-02T00:00:00.000+0000\"\n}",
      "language": "json"
    }
  ]
}
[/block]
We can see from the result that there were a total of 9982 returned for that date range, and we are beginning on `resultsPage` 0, with a `resultsPageSize` of 100 as per our request.
[block:api-header]
{
  "type": "basic",
  "title": "Iterating through all available pages"
}
[/block]
After the first response, the client should store:
* The current page (identified by `resultsPageSize`: 0)
* The number of results returned across the whole date range (identified by `resultsTotal`: 99382)

Then, you can compute the number of pages that you have to iterate through by applying the following calculation:

```
pagesToIterate = ceiling(resultsTotal/resultsPageSize)
```

In this particular case, the `pagesToIterate` will be 100.

Then, iterate through each page by requesting for Mentions and explicitly passing the page. For example, in order to get the next page we pass the parameter `page` as 1:
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/289733322/data/mentions?queryId=348973733&startDate=2016-05-01&endDate=2016-05-02&pageSize=100&page=1&orderBy=id&orderDirection=desc",
      "language": "curl"
    }
  ]
}
[/block]
Continue iterating over the page numbers until you have retrieved all pages of Mentions data.