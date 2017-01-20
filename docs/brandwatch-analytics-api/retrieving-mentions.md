---
title: "Retrieving Mentions"
excerpt: "Listing the Mentions within your Query."
---
Mentions are stored within Queries. There are three required parameters when retrieving Mentions:

* `queryId` - The ID of the Query that contains the Mentions.
* `startDate` - The beginning of the date range that contains the Mentions.
* `endDate` - The end of the date range that contains the Mentions.

You can control the pagination by passing additional parameters:

* `pageSize` - The number of Mentions on each page of the response.
* `page` - The page to retrieve, indexed from 0.

An example call is below:
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/289733322/data/mentions?queryId=348973733&startDate=2016-05-01&endDate=2016-05-02&pageSize=1&page=0",
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
      "code": "{\n  \"resultsTotal\": 99,\n  \"resultsPage\": 0,\n  \"resultsPageSize\": 1,\n  \"results\": [\n    {\n      \"accountType\": null,\n      \"assignment\": null,\n      \"author\": \"\",\n      \"authorCity\": null,\n      \"authorCityCode\": null,\n      \"authorContinent\": null,\n      \"authorContinentCode\": null,\n      \"authorCountry\": null,\n      \"authorCountryCode\": null,\n      \"authorCounty\": null,\n      \"authorCountyCode\": null,\n      \"authorLocation\": null,\n      \"authorState\": null,\n      \"authorStateCode\": null,\n      \"avatarUrl\": null,\n      \"averageDurationOfVisit\": 0,\n      \"averageVisits\": 0,\n      \"backlinks\": 19,\n      \"blogComments\": 0,\n      \"categories\": [],\n      \"categoryDetails\": [],\n      \"checked\": false,\n      \"city\": null,\n      \"cityCode\": null,\n      \"continent\": Europe,\n      \"continentCode\": \"eu\",\n      \"country\": \"United Kingdom\",\n      \"countryCode\": \"uk\",\n      \"county\": null,\n      \"countyCode\": null,\n      \"date\": \"2016-06-07T02:04:00.000+0000\",\n      \"displayUrls\": [],\n      \"domain\": \"bbc.co.uk\",\n      \"engagement\": 0,\n      \"expandedUrls\": [],\n      \"facebookAuthorId\": null,\n      \"facebookComments\": 0,\n      \"facebookLikes\": 0,\n      \"facebookRole\": null,\n      \"facebookShares\": 0,\n      \"facebookSubtype\": null,\n      \"forumPosts\": 0,\n      \"forumViews\": 0,\n      \"fullname\": null,\n      \"gender\": \"unknown\",\n      \"id\": 100057070129,\n      \"impact\": 53,\n      \"importanceAmplification\": 76,\n      \"importanceReach\": 31,\n      \"impressions\": 0,\n      \"influence\": 0,\n      \"insightsHashtag\": [],\n      \"insightsMentioned\": [],\n      \"instagramCommentCount\": 0,\n      \"instagramFollowerCount\": 0,\n      \"instagramFollowingCount\": 0,\n      \"instagramLikeCount\": 0,\n      \"instagramPostCount\": 0,\n      \"interest\": [],\n      \"language\": \"en\",\n      \"lastAssignmentDate\": null,\n      \"latitude\": 0,\n      \"locationName\": null,\n      \"longitude\": 0,\n      \"matchPositions\": [],\n      \"mediaUrls\": [],\n      \"monthlyVisitors\": 0,\n      \"mozRank\": 5.87,\n      \"noteIds\": [],\n      \"outreach\": 0,\n      \"pageType\": \"forum\",\n      \"pagesPerVisit\": 0,\n      \"percentFemaleVisitors\": 0,\n      \"percentMaleVisitors\": 0,\n      \"priority\": null,\n      \"professions\": [],\n      \"queryId\": 348973733,\n      \"queryName\": \"Telecoms news\",\n      \"reach\": 0,\n      \"replyTo\": null,\n      \"resourceId\": 100057070129,\n      \"resourceType\": \"page\",\n      \"retweetOf\": null,\n      \"sentiment\": \"neutral\",\n      \"shortUrls\": [],\n      \"snippet\": \"... known for his boisterous presentations and love of social media, said: 'Get ready for a gratitude adjustment, America. This Un-carrier move is all about giving you a good thanking! No strings. No gotchas. Just...\",\n      \"starred\": false,\n      \"state\": null,\n      \"stateCode\": null,\n      \"status\": null,\n      \"subtype\": null,\n      \"tags\": [],\n      \"threadAuthor\": null,\n      \"threadCreated\": null,\n      \"threadEntryType\": null,\n      \"threadId\": \"0\",\n      \"threadURL\": null,\n      \"title\": \"T-Mobile US customers offered free shares - BBC News\",\n      \"trackedLinkClicks\": 0,\n      \"trackedLinks\": null,\n      \"twitterAuthorId\": null,\n      \"twitterFollowers\": 0,\n      \"twitterFollowing\": 0,\n      \"twitterPostCount\": 0,\n      \"twitterReplyCount\": 0,\n      \"twitterRetweets\": 0,\n      \"twitterRole\": null,\n      \"twitterVerified\": false,\n      \"url\": \"http://www.bbc.co.uk/news/business-36466844\",\n      \"wordCount\": null\n    }\n  ],\n  \"maximumId\": 100057070129,\n  \"maximumIdInResult\": 100057070129,\n  \"startDate\": \"2016-05-01T00:00:00.000+0000\",\n  \"endDate\": \"2016-05-02T00:00:00.000+0000\"\n}",
      "language": "json"
    }
  ]
}
[/block]
### Encoding
The Analytics API will return data as it was found and does not apply any additional encoding or sanitization before returning it through the Mentions endpoint. It is your responsibility to make sure that it is formatted correctly for display in your own application.

## Data restrictions
There are contractual obligations which may affect the metadata of the Mentions that are returned.

### Data Pack restrictions
Particular Data Packs that you have added to your account may have restrictions on the Mention data that you can retrieve through the Brandwatch API. This can cause discrepancies between the data seen in the UI of the Analytics application and the data retrieved via the API. For specific information on the data packs that you have, please contact your account manager.

### Twitter data
We are unable to provide the full metadata of Mentions from Twitter. Any Mention that is a tweet will have the full text and some other metadata stripped out. If you wish to include the full metadata in your own application, then we recommend registering your application with Twitter, parsing the Twitter ID from the `url` field, and then using the [Twitter API](https://dev.twitter.com/rest/reference/get/statuses/show/%3Aid) to retrieve it.

The metadata that will be missing are as follows:
* `author`
* `avatarUrl`
* `date`
* `displayUrls`
* `expandedUrls`
* `fullText`
* `replyTo`
* `retweetsOf`
* `shortUrls`
* `snippet`
* `threadAuthor`
* `threadEntryType`
* `twitterAuthorId`
* `twitterFollowers`
* `twitterFollowing`
* `twitterPostCount`
* `twitterReplyCount`
* `twitterRetweets`
* `twitterRole`
* `twitterVerified`