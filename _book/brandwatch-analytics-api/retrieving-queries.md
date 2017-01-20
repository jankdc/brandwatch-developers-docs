---
title: "Retrieving Queries"
excerpt: "Listing the Queries that contain your data."
---
Queries are where your Mentions are stored. In order to access your Mentions, you'll need to be able to provide the Query that they are stored in. The following call will list the Queries in the Project with ID `398748937`:
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/398748937/queries/summary",
      "language": "curl"
    }
  ]
}
[/block]
The response will look like the following:
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"resultsTotal\": 2,\n  \"resultsPage\": -1,\n  \"resultsPageSize\": -1,\n  \"results\": [\n    {\n      \"id\": 387238732,\n      \"name\": \"@brandwatchsocial\",\n      \"type\": \"instagram\",\n      \"creationDate\": \"2016-06-20T19:58:47.675+0000\",\n      \"lastModificationDate\": \"2016-06-20T19:58:47.682+0000\",\n      \"lastModifiedUsername\": \"example@example.com\",\n      \"lockedQuery\": false,\n      \"lockedByUsername\": null,\n      \"createdByWizard\": false\n    },\n    {\n      \"id\": 209381723,\n      \"name\": \"Mentions of Pepsi\",\n      \"type\": \"search string\",\n      \"creationDate\": \"2016-06-07T20:02:07.420+0000\",\n      \"lastModificationDate\": \"2016-06-07T20:02:53.717+0000\",\n      \"lastModifiedUsername\": \"example@example.com\",\n      \"lockedQuery\": false,\n      \"lockedByUsername\": null,\n      \"createdByWizard\": false\n    }\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]
You can determine whether a Query is a standard Brandwatch Query or a Channel by the `type` field:

* `search string` - A Brandwatch query created by the Query Wizard, or by Boolean search string.
* `twitter` - A Twitter Channel.
* `facebook` - A Facebook Channel.
* `instagram` - An Instagram Channel.

If you wish to only retrieve a particular type of Query, then you can pass the `type` as a parameter:
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/398748937/queries/summary&type=instagram",
      "language": "curl"
    }
  ]
}
[/block]