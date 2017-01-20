---
title: "Retrieving Location Lists"
excerpt: "Getting lists of Locations that have been saved in Brandwatch Analytics."
---
Location Lists are stored within Projects. You can access them with the associated Project ID:
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/398748937/group/location/summary",
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
      "code": "{\n  \"resultsTotal\": 1,\n  \"resultsPage\": -1,\n  \"resultsPageSize\": -1,\n  \"results\": [\n    {\n      \"id\": 179865741,\n      \"name\": \"Top locations\",\n      \"shared\": \"public\",\n      \"sharedProjectIds\": [\n        398748937\n      ],\n      \"locations\": [\n        {\n          \"id\": \"cn\",\n          \"name\": \"People's Republic of China\",\n          \"type\": \"country\",\n          \"fullName\": \"People's Republic of China, Asia\"\n        },\n        {\n          \"id\": \"jp\",\n          \"name\": \"Japan\",\n          \"type\": \"country\",\n          \"fullName\": \"Japan, Asia\"\n        },\n        {\n          \"id\": \"kr\",\n          \"name\": \"Republic of Korea\",\n          \"type\": \"country\",\n          \"fullName\": \"Republic of Korea, Asia\"\n        },\n        {\n          \"id\": \"tw\",\n          \"name\": \"Republic of China (Taiwan)\",\n          \"type\": \"country\",\n          \"fullName\": \"Republic of China (Taiwan), Asia\"\n        }\n      ],\n      \"userName\": \"curtis@brandwatch.com\",\n      \"userId\": 179428706\n    }\n  ],\n  \"projects\": [\n    {\n      \"id\": 398748937,\n      \"name\": \"Shopping trends\",\n      \"description\": \"\",\n      \"billableClientId\": 39837783,\n      \"billableClientName\": null,\n      \"timezone\": \"America/New_York\",\n      \"billableClientIsPitch\": false\n    }\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]