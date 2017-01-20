---
title: "Basic Mentions Filtering"
excerpt: "Filtering the Mentions within your Queries."
---
Now you have seen the Filters that can be applied to Mentions, let's apply two of them. We want to restrict the data that is returned to be only tweets with neutral sentiment. We use two Filters for this:

* `pageType` - In our particular case, we are interested in `twitter`.
* `sentiment` - We want `neutral` Mentions to be returned.

The Filters are passed as parameters to the Mentions data call:
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/289733322/data/mentions?queryId=1998640329&startDate=2016-05-01&endDate=2016-05-02&page=0&pageSize=1&pageType=twitter&sentiment=neutral",
      "language": "curl"
    }
  ]
}
[/block]
Here is one Mention that matches those Filters, out of total of 57:
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"resultsTotal\": 57,\n  \"resultsPage\": 0,\n  \"resultsPageSize\": 1,\n  \"results\": [\n    {\n      \"accountType\": \"individual\",\n      \"assignment\": null,\n      \"author\": \"SomeKindaBoogin\",\n      \"authorCity\": null,\n      \"authorCityCode\": null,\n      \"authorContinent\": \"North America\",\n      \"authorContinentCode\": \"n-a\",\n      \"authorCountry\": \"United States\",\n      \"authorCountryCode\": \"us\",\n      \"authorCounty\": null,\n      \"authorCountyCode\": null,\n      \"authorLocation\": \"n-a,us,,,\",\n      \"authorState\": null,\n      \"authorStateCode\": null,\n      \"avatarUrl\": \"https://pbs.twimg.com/profile_images/558408263138418689/eKfX9JGi_normal.jpeg\",\n      \"averageDurationOfVisit\": 20,\n      \"averageVisits\": 6,\n      \"backlinks\": 49850734,\n      \"blogComments\": 0,\n      \"categories\": [],\n      \"categoryDetails\": [],\n      \"checked\": false,\n      \"city\": null,\n      \"cityCode\": null,\n      \"continent\": \"North America\",\n      \"continentCode\": \"n-a\",\n      \"country\": \"United States\",\n      \"countryCode\": \"us\",\n      \"county\": null,\n      \"countyCode\": null,\n      \"date\": \"2016-05-01T23:37:07.000+0000\",\n      \"displayUrls\": [\n        \"twitter.com/ricky_vaughn99…\"\n      ],\n      \"domain\": \"twitter.com\",\n      \"engagement\": 0,\n      \"expandedUrls\": [\n        \"https://twitter.com/ricky_vaughn99/status/726850523555631104\"\n      ],\n      \"facebookAuthorId\": null,\n      \"facebookComments\": 0,\n      \"facebookLikes\": 0,\n      \"facebookRole\": null,\n      \"facebookShares\": 0,\n      \"facebookSubtype\": null,\n      \"forumPosts\": 0,\n      \"forumViews\": 0,\n      \"fullname\": \"Todd Sweeney\",\n      \"gender\": \"male\",\n      \"id\": 98610951311,\n      \"impact\": 45,\n      \"importanceAmplification\": 30,\n      \"importanceReach\": 60,\n      \"impressions\": 3026,\n      \"influence\": 661,\n      \"insightsHashtag\": [],\n      \"insightsMentioned\": [\n        \"@dissidentusa\"\n      ],\n      \"instagramCommentCount\": 0,\n      \"instagramFollowerCount\": 0,\n      \"instagramFollowingCount\": 0,\n      \"instagramLikeCount\": 0,\n      \"instagramPostCount\": 0,\n      \"interest\": [\n        \"Books\",\n        \"Family & Parenting\"\n      ],\n      \"language\": \"en\",\n      \"lastAssignmentDate\": null,\n      \"latitude\": 0,\n      \"locationName\": null,\n      \"longitude\": 0,\n      \"matchPositions\": [],\n      \"mediaUrls\": [],\n      \"monthlyVisitors\": 6000000000,\n      \"mozRank\": 9.6,\n      \"noteIds\": [],\n      \"outreach\": 0,\n      \"pageType\": \"twitter\",\n      \"pagesPerVisit\": 22,\n      \"percentFemaleVisitors\": 46,\n      \"percentMaleVisitors\": 54,\n      \"priority\": null,\n      \"professions\": [\n        {\n          \"profession\": \"Software developer & IT\",\n          \"jobTitle\": \"Programmer\"\n        },\n        {\n          \"profession\": \"Teacher & Lecturer\",\n          \"jobTitle\": \"Teacher\"\n        }\n      ],\n      \"queryId\": 289733322,\n      \"queryName\": \"Trump\",\n      \"reach\": 661,\n      \"replyTo\": null,\n      \"resourceId\": 98610951311,\n      \"resourceType\": \"page\",\n      \"retweetOf\": \"http://twitter.com/dissidentusa/statuses/726916506186092544\",\n      \"sentiment\": \"neutral\",\n      \"shortUrls\": [\n        \"https://t.co/0kOd9bVFDY\"\n      ],\n      \"snippet\": \"RT @dissidentusa: I'm expecting Trump to inherit a major economic crisis, which the media will blame him for. They are angry. twitter.com/ricky_vaughn99…\",\n      \"starred\": false,\n      \"state\": null,\n      \"stateCode\": null,\n      \"status\": null,\n      \"subtype\": null,\n      \"tags\": [],\n      \"threadAuthor\": \"dissidentusa\",\n      \"threadCreated\": null,\n      \"threadEntryType\": \"share\",\n      \"threadId\": \"0\",\n      \"threadURL\": null,\n      \"title\": \"Todd Sweeney (@SomeKindaBoogin): RT @dissidentusa: I'm expe ...\",\n      \"trackedLinkClicks\": 0,\n      \"trackedLinks\": null,\n      \"twitterAuthorId\": \"2791121294\",\n      \"twitterFollowers\": 3026,\n      \"twitterFollowing\": 1409,\n      \"twitterPostCount\": 101055,\n      \"twitterReplyCount\": 0,\n      \"twitterRetweets\": 0,\n      \"twitterRole\": null,\n      \"twitterVerified\": false,\n      \"url\": \"http://twitter.com/SomeKindaBoogin/statuses/726918403311677440\",\n      \"wordCount\": null\n    }\n  ],\n  \"maximumId\": 98610951311,\n  \"maximumIdInResult\": 98610951311,\n  \"startDate\": \"2016-05-01T00:00:00.000+0000\",\n  \"endDate\": \"2016-05-02T00:00:00.000+0000\"\n}",
      "language": "json"
    }
  ]
}
[/block]