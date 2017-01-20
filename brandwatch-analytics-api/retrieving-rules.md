---
title: "Retrieving Rules"
excerpt: "Listing the Rules within your Project."
---
Tags are stored within Projects. You can access them with the associated Project ID:
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/398748937/rules",
      "language": "curl"
    }
  ]
}
[/block]
The response will look like this. It has been edited for brevity by excluding Filters that are not affected by the Rule.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"resultsTotal\": 1,\n  \"resultsPage\": -1,\n  \"resultsPageSize\": -1,\n  \"results\": [\n    {\n      \"id\": 1998324680,\n      \"projectId\": 1494022974,\n      \"name\": \"Dropped calls\",\n      \"filter\": {\n        \"queryId\": [\n          1501738808\n        ],\n        \"search\": \"\\\"dropped call\\\"\",\n      },\n      \"scope\": \"query\",\n      \"enabled\": true,\n      \"ruleAction\": {\n        \"sentiment\": \"negative\",\n      },\n      \"queryName\": \"Mobile phones\",\n      \"projectName\": \"Telecoms\"\n    }\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]
This particular example shows a Rule that applies negative sentiment whenever the term "dropped call" is found in the text of a Mention.