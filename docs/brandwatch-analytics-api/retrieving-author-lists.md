---
title: "Retrieving Author Lists"
excerpt: "Showing lists of Authors that have been saved in Brandwatch Analytics."
---
Author Lists are stored within Projects. You can access them with the associated Project ID:
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/398748937/group/author/summary",
      "language": "curl"
    }
  ]
}
[/block]
The response will be like the following:
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"resultsTotal\": 1,\n  \"resultsPage\": -1,\n  \"resultsPageSize\": -1,\n  \"results\": [\n    {\n      \"id\": 165923563,\n      \"name\": \"Influencers\",\n      \"shared\": \"public\",\n      \"sharedProjectIds\": [\n        398748937\n      ],\n      \"authors\": [\n        \"John Doe\"\n      ],\n      \"userId\": 2748873,\n      \"userName\": \"example@example.com\"\n    }\n  ],\n  \"projects\": [\n    {\n      \"id\": 398748937,\n      \"name\": \"Shopping trends\",\n      \"description\": \"\",\n      \"billableClientId\": 324398,\n      \"billableClientName\": null,\n      \"timezone\": null,\n      \"billableClientIsPitch\": false\n    }\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]