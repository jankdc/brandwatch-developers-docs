---
title: "Retrieving Query Groups"
excerpt: "Listing the Query Groups that you have created."
---
You can create Query Groups to represent a relationship between related Queries. They are stored within Projects. To see the Query Groups that exist in a Project, then use the following call:
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/937893762/querygroups",
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
      "code": "{\n  \"resultsTotal\": -1,\n  \"resultsPage\": -1,\n  \"resultsPageSize\": -1,\n  \"results\": [\n    {\n      \"id\": 165923298,\n      \"name\": \"Competitors\",\n      \"shared\": \"public\",\n      \"sharedProjectIds\": [\n        1494022974\n      ],\n      \"queries\": [\n        {\n          \"id\": 39037892,\n          \"name\": \"Ikea\"\n        },\n        {\n          \"id\": 49482811,\n          \"name\": \"DFS\"\n        }\n      ],\n      \"users\": [\n        {\n          \"id\": 298473382,\n          \"username\": \"example@example.com\",\n          \"firstName\": \"John\",\n          \"lastName\": \"Doe\",\n          \"uiRole\": \"regular\"\n        }\n      ]\n    }\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]
You can then use the `id` of the Query Group to apply a Filter to Mentions data calls, or to create charts with.