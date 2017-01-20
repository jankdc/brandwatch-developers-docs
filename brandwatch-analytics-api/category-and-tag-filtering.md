---
title: "Category and Tag Filtering"
excerpt: "Filtering the Mentions within your Queries by Categories and Tags."
---
You can also Filter your Mentions by the Categories and Tags that are assigned to them. For your Project, you will need to first retrieve the Categories or Tags that you wish to filter by. You will use the associated Category or Tag IDs in the following parameters:

* `tag` - Return Mentions that *are* tagged with this Tag ID.
* `xtag` - Return Mentions that *are not* tagged with this Tag ID.
* `category` - Return Mentions that *are* tagged with this Category ID.
* `xcategory` - Return Mentions that *are not* tagged with this Category ID.

The Filters are passed as parameters to the Mentions data call. For example, to return Mentions that are tagged by Category ID `838322`:
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/289733322/data/mentions?queryId=1998640329&startDate=2016-05-01&endDate=2016-05-02&page=0&pageSize=1&category=838322",
      "language": "curl"
    }
  ]
}
[/block]
Here is one Mention that matches those Filters, out of total of 72:
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"resultsTotal\": 72,\n  \"resultsPage\": 0,\n  \"resultsPageSize\": 1,\n  \"results\": [\n    {\n      \"accountType\": null,\n      \"assignment\": null,\n      \"author\": \"Najah Sameen\",\n      \"authorCity\": null,\n      \"authorCityCode\": null,\n      \"authorContinent\": \"North America\",\n      \"authorContinentCode\": \"n-a\",\n      \"authorCountry\": \"United States\",\n      \"authorCountryCode\": \"us\",\n      \"authorCounty\": null,\n      \"authorCountyCode\": null,\n      \"authorLocation\": \"n-a,us,,,\",\n      \"authorState\": null,\n      \"authorStateCode\": null,\n      \"avatarUrl\": null,\n      \"averageDurationOfVisit\": 0,\n      \"averageVisits\": 0,\n      \"backlinks\": 0,\n      \"blogComments\": 0,\n      \"categories\": [838322],\n      \"categoryDetails\": [\n        {\n          \"id\": \"838322\",\n          \"name\": \"Lips\",\n          \"parentId\": \"838321\",\n          \"parentName\": \"Beauty products\"\n        }\n      ],\n      \"checked\": false,\n      \"city\": null,\n      \"cityCode\": null,\n      \"continent\": \"North America\",\n      \"continentCode\": \"n-a\",\n      \"country\": \"United States\",\n      \"countryCode\": \"us\",\n      \"county\": null,\n      \"countyCode\": null,\n      \"date\": \"2016-05-01T11:52:05.699+0000\",\n      \"displayUrls\": [],\n      \"domain\": \"www.indianbeautyforever.com\",\n      \"engagement\": 0,\n      \"expandedUrls\": [],\n      \"facebookAuthorId\": null,\n      \"facebookComments\": 0,\n      \"facebookLikes\": 0,\n      \"facebookRole\": null,\n      \"facebookShares\": 0,\n      \"facebookSubtype\": null,\n      \"forumPosts\": 0,\n      \"forumViews\": 0,\n      \"fullname\": null,\n      \"gender\": \"unknown\",\n      \"id\": 99581066231,\n      \"impact\": 39,\n      \"importanceAmplification\": 47,\n      \"importanceReach\": 31,\n      \"impressions\": 0,\n      \"influence\": 0,\n      \"insightsHashtag\": [],\n      \"insightsMentioned\": [],\n      \"instagramCommentCount\": 0,\n      \"instagramFollowerCount\": 0,\n      \"instagramFollowingCount\": 0,\n      \"instagramLikeCount\": 0,\n      \"instagramPostCount\": 0,\n      \"interest\": [],\n      \"language\": \"en\",\n      \"lastAssignmentDate\": null,\n      \"latitude\": 0,\n      \"locationName\": null,\n      \"longitude\": 0,\n      \"matchPositions\": [\n        {\n          \"start\": 133,\n          \"text\": \"oil\",\n          \"length\": 3\n        },\n        {\n          \"start\": 150,\n          \"text\": \"oil\",\n          \"length\": 3\n        },\n        {\n          \"start\": 178,\n          \"text\": \"moisturizing\",\n          \"length\": 12\n        },\n        {\n          \"start\": 201,\n          \"text\": \"lips\",\n          \"length\": 4\n        },\n        {\n          \"start\": 217,\n          \"text\": \"use\",\n          \"length\": 3\n        },\n        {\n          \"start\": 227,\n          \"text\": \"at\",\n          \"length\": 2\n        },\n        {\n          \"start\": 230,\n          \"text\": \"night\",\n          \"length\": 5\n        },\n        {\n          \"start\": 247,\n          \"text\": \"lips\",\n          \"length\": 4\n        }\n      ],\n      \"mediaUrls\": [],\n      \"monthlyVisitors\": 0,\n      \"mozRank\": 0,\n      \"noteIds\": [],\n      \"outreach\": 0,\n      \"pageType\": \"news\",\n      \"pagesPerVisit\": 0,\n      \"percentFemaleVisitors\": 0,\n      \"percentMaleVisitors\": 0,\n      \"priority\": null,\n      \"professions\": [],\n      \"queryId\": 1998640329,\n      \"queryName\": \"Makeup\",\n      \"reach\": 0,\n      \"replyTo\": null,\n      \"resourceId\": 99581066231,\n      \"resourceType\": \"page\",\n      \"retweetOf\": null,\n      \"sentiment\": \"positive\",\n      \"shortUrls\": [],\n      \"snippet\": \"Mango butter. These will hydrate and soften the dry lips. These lip balms also contain essential oils like macadamia nut oil, castor oil, carrot seed oil etc which are immensely moisturizing for flaky lips. I like to use these at night to give my lips boost of moisture. These lip moisturizer are mildly sweet in taste hence if you lick it you...\",\n      \"starred\": false,\n      \"state\": null,\n      \"stateCode\": null,\n      \"status\": null,\n      \"subtype\": null,\n      \"tags\": [],\n      \"threadAuthor\": null,\n      \"threadCreated\": null,\n      \"threadEntryType\": null,\n      \"threadId\": \"0\",\n      \"threadURL\": null,\n      \"title\": \"Island Kiss Tropical Lip Moisturisers Review - Indian Beauty Forever\",\n      \"trackedLinkClicks\": 0,\n      \"trackedLinks\": null,\n      \"twitterAuthorId\": null,\n      \"twitterFollowers\": 0,\n      \"twitterFollowing\": 0,\n      \"twitterPostCount\": 0,\n      \"twitterReplyCount\": 0,\n      \"twitterRetweets\": 0,\n      \"twitterRole\": null,\n      \"twitterVerified\": false,\n      \"url\": \"http://www.indianbeautyforever.com/2016/04/island-kiss-tropical-lip-moisturisers-review.html?showComment=1462103525699\",\n      \"wordCount\": null\n    }\n  ],\n  \"maximumId\": 99581066231,\n  \"maximumIdInResult\": 99581066231,\n  \"startDate\": \"2016-05-01T00:00:00.000+0000\",\n  \"endDate\": \"2016-05-02T00:00:00.000+0000\"\n}",
      "language": "json"
    }
  ]
}
[/block]