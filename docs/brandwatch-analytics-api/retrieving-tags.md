---
title: "Retrieving Tags"
excerpt: "Listing the Tags within your Project."
---
Tags are stored within Projects.

If you are building an application, we recommend caching the Tags that are applied to your project locally, so that you do not have to retrieve them every time that you do a Mentions data call.

You can access them with the associated Project ID:
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/398748937/tags",
      "language": "curl"
    }
  ]
}
[/block]
The response will look like this:
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"resultsTotal\": -1,\n  \"resultsPage\": -1,\n  \"resultsPageSize\": -1,\n  \"results\": [\n    {\n      \"id\": 3897282,\n      \"name\": \"Celebrities\"\n    },\n    {\n      \"id\": 3472876,\n      \"name\": \"Journalists\"\n    },\n    {\n      \"id\": 9879833,\n      \"name\": \"Bloggers\"\n    },\n    {\n      \"id\": 7673322,\n      \"name\": \"Members of the public\"\n    }\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]
You can then use these Tag IDs when filtering or breaking down Mention calls.