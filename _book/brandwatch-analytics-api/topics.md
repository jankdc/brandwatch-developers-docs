---
title: "Topics"
excerpt: "Finding topics of conversation in your Mentions."
---
You can also use the Brandwatch topics functionality via the API.

The topics data call has the same three required parameters as the Mentions call:

* `queryId` - The ID of the Query that contains the Mentions.
* `startDate` - The beginning of the date range that contains the Mentions.
* `endDate` - The end of the date range that contains the Mentions.

Some additional parameters that will be useful:

* `orderBy` - Choose between `volume` (the number of Mentions the topic appears in) and `burst` (the amount by which it is trending).
* `limit` - Limit the number of results that come back.
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/397263282/data/volume/topics/queries?queryId=389734742&startDate=2016-05-01&endDate=2016-05-07&orderBy=burst&limit=2",
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
      "code": "{\n  \"topics\": [\n    {\n      \"id\": \"1998640329__Lipstick\",\n      \"label\": \"Lipstick\",\n      \"volume\": 3,\n      \"type\": \"topic\",\n      \"sentiment\": {\n        \"neutral\": 1,\n        \"positive\": 2\n      },\n      \"sentimentScore\": 116,\n      \"burst\": 100,\n      \"days\": [\n        {\n          \"date\": \"2016-05-05T00:00:00.000+0000\",\n          \"volume\": 1\n        },\n        {\n          \"date\": \"2016-05-04T00:00:00.000+0000\",\n          \"volume\": 2\n        },\n        {\n          \"date\": \"2016-05-02T00:00:00.000+0000\",\n          \"volume\": 0\n        },\n        {\n          \"date\": \"2016-05-01T00:00:00.000+0000\",\n          \"volume\": 0\n        },\n        {\n          \"date\": \"2016-05-06T00:00:00.000+0000\",\n          \"volume\": 0\n        },\n        {\n          \"date\": \"2016-05-03T00:00:00.000+0000\",\n          \"volume\": 0\n        }\n      ],\n      \"pageType\": {\n        \"blog\": 0,\n        \"facebook\": 2,\n        \"forum\": 1,\n        \"general\": 0,\n        \"image\": 0,\n        \"instagram\": 0,\n        \"news\": 0,\n        \"review\": 0,\n        \"twitter\": 0,\n        \"video\": 0\n      },\n      \"queries\": [\n        {\n          \"id\": 1998640329,\n          \"name\": \"Makeup\",\n          \"volume\": 3\n        }\n      ]\n    },\n    {\n      \"id\": \"1998640329__Rashes\",\n      \"label\": \"Rashes\",\n      \"volume\": 5,\n      \"type\": \"topic\",\n      \"sentiment\": {\n        \"neutral\": 5\n      },\n      \"sentimentScore\": 50,\n      \"burst\": 100,\n      \"days\": [\n        {\n          \"date\": \"2016-05-05T00:00:00.000+0000\",\n          \"volume\": 2\n        },\n        {\n          \"date\": \"2016-05-04T00:00:00.000+0000\",\n          \"volume\": 0\n        },\n        {\n          \"date\": \"2016-05-02T00:00:00.000+0000\",\n          \"volume\": 0\n        },\n        {\n          \"date\": \"2016-05-06T00:00:00.000+0000\",\n          \"volume\": 2\n        },\n        {\n          \"date\": \"2016-05-01T00:00:00.000+0000\",\n          \"volume\": 0\n        },\n        {\n          \"date\": \"2016-05-03T00:00:00.000+0000\",\n          \"volume\": 0\n        }\n      ],\n      \"pageType\": {\n        \"blog\": 0,\n        \"facebook\": 5,\n        \"forum\": 0,\n        \"general\": 0,\n        \"image\": 0,\n        \"instagram\": 0,\n        \"news\": 0,\n        \"review\": 0,\n        \"twitter\": 0,\n        \"video\": 0\n      },\n      \"queries\": [\n        {\n          \"id\": 389734742,\n          \"name\": \"Makeup\",\n          \"volume\": 5\n        }\n      ]\n    }\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]