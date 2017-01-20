---
title: "Basic charts"
excerpt: "Creating a chart out of your Mentions."
---
As well as retrieving pages of Mentions, you can also create charts out of them. The charts data call is in the following format:

```
/data/{aggregate}/{dimension1}/{dimension2}
```
The *aggregate* is. Some example aggregates are:

* `volume` - The number of Mentions found.
* `sentiment` - The sentiment of the Mentions.
* `pageType` - The page type of the Mentions.
* `authors` - The distinct authors who posted.

The two *dimensions* are your *x* and *y* axes on the chart. Some example dimensions are:

* `days` - The days over which the Mentions were found.
* `queries` - The Queries that the Mentions are located in.
* `gender` - The gender of the authors.
* `location` - The locations the Mentions were posted from.

For full details on the available aggregates and dimensions, see the Aggregates and Dimensions page of the documentation.

The charts data call has the same three required parameters as the Mentions call:

* `queryId` - The ID of the Query that contains the Mentions.
* `startDate` - The beginning of the date range that contains the Mentions.
* `endDate` - The end of the date range that contains the Mentions.

An example call is below, which charts the volume of Mentions (the *aggregate*) in the given Query (the first *dimension*) by their sentiment (the second *dimension*):
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/397263282/data/volume/sentiment/days?queryId=9226732&startDate=2016-05-01&endDate=2016-05-07",
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
      "code": "{\n  \"aggregate\": \"volume\",\n  \"dimension1\": \"sentiment\",\n  \"dimension2\": \"days\",\n  \"results\": [\n    {\n      \"id\": \"negative\",\n      \"name\": \"negative\",\n      \"data\": {},\n      \"values\": [\n        {\n          \"id\": \"2016-05-05T00:00:00.000+0000\",\n          \"name\": \"2016-05-05 00:00:00.0\",\n          \"value\": 12,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-05-04T00:00:00.000+0000\",\n          \"name\": \"2016-05-04 00:00:00.0\",\n          \"value\": 10,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-05-02T00:00:00.000+0000\",\n          \"name\": \"2016-05-02 00:00:00.0\",\n          \"value\": 10,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-05-01T00:00:00.000+0000\",\n          \"name\": \"2016-05-01 00:00:00.0\",\n          \"value\": 5,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-05-06T00:00:00.000+0000\",\n          \"name\": \"2016-05-06 00:00:00.0\",\n          \"value\": 10,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-05-03T00:00:00.000+0000\",\n          \"name\": \"2016-05-03 00:00:00.0\",\n          \"value\": 8,\n          \"data\": {}\n        }\n      ]\n    },\n    {\n      \"id\": \"neutral\",\n      \"name\": \"neutral\",\n      \"data\": {},\n      \"values\": [\n        {\n          \"id\": \"2016-05-05T00:00:00.000+0000\",\n          \"name\": \"2016-05-05 00:00:00.0\",\n          \"value\": 104,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-05-04T00:00:00.000+0000\",\n          \"name\": \"2016-05-04 00:00:00.0\",\n          \"value\": 110,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-05-02T00:00:00.000+0000\",\n          \"name\": \"2016-05-02 00:00:00.0\",\n          \"value\": 111,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-05-01T00:00:00.000+0000\",\n          \"name\": \"2016-05-01 00:00:00.0\",\n          \"value\": 78,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-05-06T00:00:00.000+0000\",\n          \"name\": \"2016-05-06 00:00:00.0\",\n          \"value\": 93,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-05-03T00:00:00.000+0000\",\n          \"name\": \"2016-05-03 00:00:00.0\",\n          \"value\": 103,\n          \"data\": {}\n        }\n      ]\n    },\n    {\n      \"id\": \"positive\",\n      \"name\": \"positive\",\n      \"data\": {},\n      \"values\": [\n        {\n          \"id\": \"2016-05-05T00:00:00.000+0000\",\n          \"name\": \"2016-05-05 00:00:00.0\",\n          \"value\": 16,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-05-04T00:00:00.000+0000\",\n          \"name\": \"2016-05-04 00:00:00.0\",\n          \"value\": 19,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-05-02T00:00:00.000+0000\",\n          \"name\": \"2016-05-02 00:00:00.0\",\n          \"value\": 16,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-05-01T00:00:00.000+0000\",\n          \"name\": \"2016-05-01 00:00:00.0\",\n          \"value\": 22,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-05-06T00:00:00.000+0000\",\n          \"name\": \"2016-05-06 00:00:00.0\",\n          \"value\": 14,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-05-03T00:00:00.000+0000\",\n          \"name\": \"2016-05-03 00:00:00.0\",\n          \"value\": 25,\n          \"data\": {}\n        }\n      ]\n    }\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]
It is possible to create a huge variety of charts that you can embed into your own applications. For example, given a Query Group that consists of Queries for your own brands and your competitors brands, you could create a weekly share of voice chart:
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/1998179136/data/volume/queryGroups/weeks?queryGroupId=183104417&startDate=2016-01-01&endDate=2016-05-07",
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
      "code": "{\n  \"aggregate\": \"volume\",\n  \"dimension1\": \"queryGroups\",\n  \"dimension2\": \"weeks\",\n  \"results\": [\n    {\n      \"id\": 183104417,\n      \"name\": \"All Topics\",\n      \"data\": {},\n      \"values\": [\n        {\n          \"id\": \"2016-02-29T00:00:00.000+0000\",\n          \"name\": \"2016-02-29 00:00:00.0\",\n          \"value\": 3,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-04-04T00:00:00.000+0000\",\n          \"name\": \"2016-04-04 00:00:00.0\",\n          \"value\": 1200,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-04-25T00:00:00.000+0000\",\n          \"name\": \"2016-04-25 00:00:00.0\",\n          \"value\": 1258,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-01-25T00:00:00.000+0000\",\n          \"name\": \"2016-01-25 00:00:00.0\",\n          \"value\": 2,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-02-15T00:00:00.000+0000\",\n          \"name\": \"2016-02-15 00:00:00.0\",\n          \"value\": 4,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-01-11T00:00:00.000+0000\",\n          \"name\": \"2016-01-11 00:00:00.0\",\n          \"value\": 0,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-04-11T00:00:00.000+0000\",\n          \"name\": \"2016-04-11 00:00:00.0\",\n          \"value\": 1447,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-03-21T00:00:00.000+0000\",\n          \"name\": \"2016-03-21 00:00:00.0\",\n          \"value\": 2,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-03-07T00:00:00.000+0000\",\n          \"name\": \"2016-03-07 00:00:00.0\",\n          \"value\": 5,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2015-12-28T00:00:00.000+0000\",\n          \"name\": \"2015-12-28 00:00:00.0\",\n          \"value\": 0,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-02-01T00:00:00.000+0000\",\n          \"name\": \"2016-02-01 00:00:00.0\",\n          \"value\": 2,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-01-18T00:00:00.000+0000\",\n          \"name\": \"2016-01-18 00:00:00.0\",\n          \"value\": 4,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-02-22T00:00:00.000+0000\",\n          \"name\": \"2016-02-22 00:00:00.0\",\n          \"value\": 2,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-03-28T00:00:00.000+0000\",\n          \"name\": \"2016-03-28 00:00:00.0\",\n          \"value\": 398,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-05-02T00:00:00.000+0000\",\n          \"name\": \"2016-05-02 00:00:00.0\",\n          \"value\": 911,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-01-04T00:00:00.000+0000\",\n          \"name\": \"2016-01-04 00:00:00.0\",\n          \"value\": 0,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-04-18T00:00:00.000+0000\",\n          \"name\": \"2016-04-18 00:00:00.0\",\n          \"value\": 1449,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-02-08T00:00:00.000+0000\",\n          \"name\": \"2016-02-08 00:00:00.0\",\n          \"value\": 3,\n          \"data\": {}\n        },\n        {\n          \"id\": \"2016-03-14T00:00:00.000+0000\",\n          \"name\": \"2016-03-14 00:00:00.0\",\n          \"value\": 10,\n          \"data\": {}\n        }\n      ]\n    }\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]