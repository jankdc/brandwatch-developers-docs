---
title: "Retrieving Metrics"
excerpt: "Finding out which Metrics you can filter your Mentions by."
---
There are global preset metrics that you can filter your Mentions by. 
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/metrics",
      "language": "curl"
    }
  ]
}
[/block]
This returns (at the time of writing):
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"sentiments\": [\n    \"negative\",\n    \"neutral\",\n    \"positive\"\n  ],\n  \"accountTypes\": [\n    \"organisational\",\n    \"individual\"\n  ],\n  \"genders\": [\n    \"female\",\n    \"male\"\n  ],\n  \"pageTypes\": [\n    \"news\",\n    \"forum\",\n    \"general\",\n    \"image\",\n    \"twitter\",\n    \"review\",\n    \"facebook\",\n    \"video\",\n    \"instagram\",\n    \"blog\"\n  ],\n  \"subTypes\": [\n    \"other\",\n    \"question\",\n    \"link\",\n    \"photo\",\n    \"video\",\n    \"status\"\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]
As we add new global metrics, they will turn up here. It's worth mentioning that these change infrequently, often in line with new features being added to Analytics. If you wanted to store these locally and update them in your app infrequently, then you could take that approach and save on your rate limiting.