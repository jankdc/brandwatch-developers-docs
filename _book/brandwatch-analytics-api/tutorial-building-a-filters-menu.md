---
title: "Tutorial: building a Filters menu"
excerpt: "How to build a menu for your users to control how to get Brandwatch data."
---
[block:api-header]
{
  "type": "basic",
  "title": "Introduction"
}
[/block]
In this tutorial, we'll walk through how to think about building a filters menu in your app that's similar to the one in Brandwatch Analytics. This could allow your users to control the Brandwatch Mentions that are being retrieved by changing the filter to match their own preferences.

Users should be presented with a menu of filters from which to choose the criteria for results, which will be passed into the [Mentions](doc:retrieving-mentions) call.  The basic process for this would be to show a list of all the filter types, reveal the details of each filter type when selected, and make the appropriate API calls to fetch the options for any filter that may vary by user or account. The resulting selection should be stored in order to pass as parameters into the mentions or metrics call.
[block:api-header]
{
  "type": "basic",
  "title": "Filter menu options"
}
[/block]
In the Brandwatch Analytics app, the filters menu contains lots of different filters. Let's restrict ourselves to a subset of those in this tutorial so that we don't end up repeating ourselves over and over. Let's say we wanted to build a Filters menu into an app that looked something like this:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/919d9d4-Filters_menu_-_Page_1.png",
        "Filters menu - Page 1.png",
        1650,
        1125,
        "#e8e1dc"
      ]
    }
  ]
}
[/block]
On the left hand side, you have an area that will render the Mentions that come back from the Analytics [Mentions](doc:retrieving-mentions) call. On the right hand side are some drop-down menus that will allow you to add filters to the Mentions call that populates the area on the left hand side.
[block:api-header]
{
  "type": "basic",
  "title": "Getting the parameters for filters"
}
[/block]
Some of the Filters have presets. In this particular menu, this is true of 

* Sentiment
* Page Type
* Workflow: priority
* Workflow: status

On rendering the filters menu, you will need to populate the drop-down boxes with the presets that the user can select from. These presets will then translate to additional Filters that you pass to the Mentions call as parameters. 

Some Filters are populated from items that the user has generated, or have unique IDs. In the wireframe above, these filters are:

* Tags 
* Categories
* Author lists
* Location lists
* Workflow: assignments

[block:parameters]
{
  "data": {
    "h-0": "Filter",
    "h-1": "Presets",
    "h-2": "Mentions call parameter",
    "h-3": "Explanation",
    "0-0": "Sentiment",
    "1-0": "Page Type",
    "2-0": "Workflow: Priority",
    "3-0": "Workflow: Status",
    "0-1": "[Retrieving Metrics](doc:retrieving-metrics)",
    "0-2": "* `&sentiment=<option>`",
    "0-3": "Filters your Mentions by the Sentiment of the text.",
    "1-1": "[Retrieving Metrics](doc:retrieving-metrics)",
    "1-2": "* `&pageType=<option>`",
    "1-3": "Filters your Mentions by the type of page that they are, e.g. from Twitter, Instagram, or a blog.",
    "2-1": "[Retrieving Workflow](doc:retrieving-workflow)",
    "2-2": "* `&priority=<option>`",
    "2-3": "Filters your Mentions by the Workflow: Priority feature of Brandwatch, which allows users to assign a Priority to their Mentions. Only one Priority can be specified per API call.",
    "3-1": "[Retrieving Workflow](doc:retrieving-workflow)",
    "3-2": "* `&status=<option>`",
    "3-3": "Filters your Mentions by the Workflow: Status feature of Brandwatch, which allows users to assign a Status to Mentions.",
    "5-0": "Tags",
    "5-1": "[Retrieving Tags](doc:retrieving-tags)",
    "5-2": "* `&tag=<tagID>`\n* `&xtag=<tagID>`",
    "5-3": "Filters your Mentions by those with or without a particular Tag.",
    "6-0": "Categories",
    "6-1": "[Retrieving Categories](doc:retrieving-categories)",
    "6-2": "* `&parentCategory=<categoryID>`\n* `&xparentCategory=<categoryID>`\n* `&category=<subcategoryID>`\n* `&xcategory=<subcategoryID>`",
    "6-3": "Filters your Mentions by those with or without a particular Category.",
    "7-0": "Author lists",
    "7-1": "[Retrieving Author Lists](doc:retrieving-author-lists)",
    "7-2": "* `&authorGroup=<authorGroupID>`\n* `&xauthorGroup=<authorGroupID>`",
    "7-3": "Filters your Mentions by the authors in an Author List, inclusively or exclusively.",
    "8-0": "Location lists",
    "8-1": "[Retrieving Location Lists](doc:retrieving-location-list)",
    "8-2": "* `&locationGroup=<locationGroupID>`\n* `&xlocationGroup=<locationGroupID>`",
    "8-3": "Filters your Mentions by the locations in a Location List, inclusively or exclusively.",
    "4-0": "Workflow: assignments",
    "4-1": "[Retrieving Workflow](doc:retrieving-workflow)",
    "4-2": "* `assigned=<username>`",
    "4-3": "Filters your Mentions by the Workflow: Status feature of Brandwatch, which allows users to assign a Mention to another Brandwatch user."
  },
  "cols": 4,
  "rows": 9
}
[/block]
When the user clicks the Refresh button, the Filters that have been selected should have their associated IDs passed through as parameters to the Mentions call as specified above.