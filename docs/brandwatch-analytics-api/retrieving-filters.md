---
title: "Retrieving Filters"
excerpt: "Listing the Filters you can use with Mentions."
---
All Mention data calls can be filtered so that you can access specific parts of your data. You can do this by using Filters. Mentions can be filtered by many different values of metadata.

If you are building an application, we recommend caching the Filters that are applied to your Mentions locally, so that you do not have to retrieve them every time that you do a Mentions data call.

You can find out the metadata that Mentions can be filtered by with the following call:
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/filters",
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
      "code": "{\n  \"queryId\": null,\n  \"queryGroupId\": null,\n  \"projectId\": null,\n  \"startDate\": null,\n  \"endDate\": null,\n  \"sinceId\": null,\n  \"untilId\": null,\n  \"dayOfWeekTimezone\": null,\n  \"hourOfDayTimezone\": null,\n  \"search\": null,\n  \"sinceAssignmentUpdated\": null,\n  \"untilAssignmentUpdated\": null,\n  \"author\": null,\n  \"xauthor\": null,\n  \"exactAuthor\": null,\n  \"xexactAuthor\": null,\n  \"authorGroup\": null,\n  \"xauthorGroup\": null,\n  \"sentiment\": null,\n  \"pageType\": null,\n  \"xpageType\": null,\n  \"siteGroup\": null,\n  \"xsiteGroup\": null,\n  \"locationGroup\": null,\n  \"xlocationGroup\": null,\n  \"location\": null,\n  \"xlocation\": null,\n  \"authorLocationGroup\": null,\n  \"xauthorLocationGroup\": null,\n  \"authorLocation\": null,\n  \"xauthorLocation\": null,\n  \"category\": null,\n  \"xcategory\": null,\n  \"parentCategory\": null,\n  \"xparentCategory\": null,\n  \"tag\": null,\n  \"xtag\": null,\n  \"status\": null,\n  \"xstatus\": null,\n  \"priority\": null,\n  \"xpriority\": null,\n  \"checked\": null,\n  \"starred\": null,\n  \"assigned\": null,\n  \"xassigned\": null,\n  \"backlinksMax\": null,\n  \"backlinksMin\": null,\n  \"blogCommentsMax\": null,\n  \"blogCommentsMin\": null,\n  \"pagesPerVisitMax\": null,\n  \"pagesPerVisitMin\": null,\n  \"averageVisitsMax\": null,\n  \"averageVisitsMin\": null,\n  \"monthlyVisitorsMax\": null,\n  \"monthlyVisitorsMin\": null,\n  \"percentFemaleVisitorsMin\": null,\n  \"percentMaleVisitorsMin\": null,\n  \"averageDurationOfVisitMax\": null,\n  \"averageDurationOfVisitMin\": null,\n  \"twitterFollowersMax\": null,\n  \"twitterFollowersMin\": null,\n  \"twitterFollowingMax\": null,\n  \"twitterFollowingMin\": null,\n  \"twitterReplyTo\": null,\n  \"xtwitterReplyTo\": null,\n  \"twitterRetweetOf\": null,\n  \"xtwitterRetweetOf\": null,\n  \"twitterPostCountMax\": null,\n  \"twitterPostCountMin\": null,\n  \"twitterRetweetsMax\": null,\n  \"twitterRetweetsMin\": null,\n  \"forumPostsMax\": null,\n  \"forumPostsMin\": null,\n  \"forumViewsMax\": null,\n  \"forumViewsMin\": null,\n  \"mozRankMax\": null,\n  \"mozRankMin\": null,\n  \"reachMin\": null,\n  \"reachMax\": null,\n  \"influenceMin\": null,\n  \"influenceMax\": null,\n  \"outreachMin\": null,\n  \"outreachMax\": null,\n  \"language\": null,\n  \"xlanguage\": null,\n  \"domain\": null,\n  \"xdomain\": null,\n  \"facebookAuthorId\": null,\n  \"xfacebookAuthorId\": null,\n  \"facebookRole\": null,\n  \"xfacebookRole\": null,\n  \"facebookSubtype\": null,\n  \"xfacebookSubtype\": null,\n  \"subtype\": null,\n  \"xsubtype\": null,\n  \"facebookCommentsMax\": null,\n  \"facebookCommentsMin\": null,\n  \"facebookLikesMax\": null,\n  \"facebookLikesMin\": null,\n  \"facebookSharesMax\": null,\n  \"facebookSharesMin\": null,\n  \"twitterVerified\": null,\n  \"twitterRole\": null,\n  \"twitterAuthorId\": null,\n  \"xtwitterAuthorId\": null,\n  \"impressionsMax\": null,\n  \"impressionsMin\": null,\n  \"impactMax\": null,\n  \"impactMin\": null,\n  \"instagramFollowersMax\": null,\n  \"instagramFollowersMin\": null,\n  \"instagramFollowingMax\": null,\n  \"instagramFollowingMin\": null,\n  \"instagramPostsMax\": null,\n  \"instagramPostsMin\": null,\n  \"instagramLikesMax\": null,\n  \"instagramLikesMin\": null,\n  \"instagramCommentsMax\": null,\n  \"instagramCommentsMin\": null,\n  \"instagramInteractionsMax\": null,\n  \"instagramInteractionsMin\": null,\n  \"threadId\": null,\n  \"xthreadId\": null,\n  \"threadEntryType\": null,\n  \"xthreadEntryType\": null,\n  \"threadAuthor\": null,\n  \"xthreadAuthor\": null,\n  \"postByAuthor\": null,\n  \"xpostByAuthor\": null,\n  \"shareOfAuthor\": null,\n  \"xshareOfAuthor\": null,\n  \"replyToAuthor\": null,\n  \"xreplyToAuthor\": null,\n  \"resourceType\": null,\n  \"xresourceType\": null,\n  \"editorialValueEURMin\": null,\n  \"editorialValueEURMax\": null,\n  \"editorialValueUSDMin\": null,\n  \"editorialValueUSDMax\": null,\n  \"editorialValueGBPMin\": null,\n  \"editorialValueGBPMax\": null,\n  \"insightsEmoticon\": null,\n  \"insightsHashtag\": null,\n  \"insightsMentioned\": null,\n  \"insightsUrl\": null,\n  \"xinsightsEmoticon\": null,\n  \"xinsightsHashtag\": null,\n  \"xinsightsMentioned\": null,\n  \"xinsightsUrl\": null,\n  \"gender\": null,\n  \"accountType\": null,\n  \"profession\": null,\n  \"xprofession\": null,\n  \"interest\": null,\n  \"xinterest\": null,\n  \"exclusiveLocation\": null,\n  \"hourOfDay\": null,\n  \"dayOfWeek\": null,\n  \"geolocated\": null,\n  \"latitudeMin\": null,\n  \"latitudeMax\": null,\n  \"longitudeMin\": null,\n  \"longitudeMax\": null,\n  \"mentionId\": null\n}",
      "language": "json"
    }
  ]
}
[/block]
These Filters can then be used as parameters in Mention data calls. For example, you could pass the parameter `gender="female"` to only retrieve Mentions that were authored by females.