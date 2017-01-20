---
title: "Retrieving Projects"
excerpt: "Listing the Projects that contain your work."
---
Projects are where your Queries, categorization and configurations are stored. In order to access your data, you'll need to be able to provide the Project that it is stored in. The following call will list your Projects:
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/summary",
      "language": "curl"
    }
  ]
}
[/block]
The result will be a list of the Projects that you have access to with the user that you are logged in as:
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"resultsTotal\": 2,\n  \"resultsPage\": -1,\n  \"resultsPageSize\": -1,\n  \"results\": [\n    {\n      \"id\": 398748937,\n      \"name\": \"Telecoms research\",\n      \"description\": \"Mobile phones\",\n      \"billableClientId\": 127732,\n      \"billableClientName\": \"My company\",\n      \"timezone\": \"Africa/Abidjan\",\n      \"billableClientIsPitch\": false\n    },\n    {\n      \"id\": 32092327,\n      \"name\": \"GPS research\",\n      \"description\": \"In-car navigation systems\",\n      \"billableClientId\": 127732,\n      \"billableClientName\": \"My company\",\n      \"timezone\": \"America/Glace_Bay\",\n      \"billableClientIsPitch\": false\n    }\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]
As you will see in later calls, you will need to know the `id` of the Projects that data is stored in so that you can access them.