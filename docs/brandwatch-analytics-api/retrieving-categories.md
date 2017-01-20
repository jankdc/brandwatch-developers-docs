---
title: "Retrieving Categories"
excerpt: "Listing the Categories within your Project."
---
Categories are stored within Projects.

If you are building an application, we recommend caching the Categories that are applied to your project locally, so that you do not have to retrieve them every time that you do a Mentions data call.

You can access them with the associated Project ID:
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/398748937/categories",
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
      "code": "{\n  \"resultsTotal\": -1,\n  \"resultsPage\": -1,\n  \"resultsPageSize\": -1,\n  \"results\": [\n    {\n      \"id\": 39873297,\n      \"name\": \"Customer Issues\",\n      \"multiple\": false,\n      \"children\": [\n        {\n          \"id\": 19298737,\n          \"name\": \"Shipping\",\n          \"ordering\": 0\n        },\n        {\n          \"id\": 9083947,\n          \"name\": \"Sizing\",\n          \"ordering\": 0\n        },\n        {\n          \"id\": 9328497,\n          \"name\": \"Product faults\",\n          \"ordering\": 0\n        },\n        {\n          \"id\": 39483984,\n          \"name\": \"Environmental\",\n          \"ordering\": 0\n        }\n      ]\n    }\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]
Here, the "Customer Issues" Category with ID `39873297` has four Subcategories, as identified in the `children` array.

You can then use these Category and Subcategory IDs when filtering or breaking down Mention calls. Elsewhere in the documentation you may see the top-level Categories being referred to as "Parent Categories".