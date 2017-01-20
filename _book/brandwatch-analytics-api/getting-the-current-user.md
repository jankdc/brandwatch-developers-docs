---
title: "Retrieving the current User"
excerpt: "Displaying information about who you are logged in as."
---
Each Brandwatch User has associated metadata, including their permissions.
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/user",
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
      "code": "{\n  \"id\": 32987387,\n  \"username\": \"example@example.com\",\n  \"password\": \"[protected]\",\n  \"passwordConfirmation\": null,\n  \"oldPassword\": null,\n  \"passwordExpiryDate\": null,\n  \"clientId\": 59580958,\n  \"firstName\": \"John\",\n  \"lastName\": \"Doe\",\n  \"creationDate\": \"2016-06-29T16:19:17.744+0000\",\n  \"enabled\": true,\n  \"job\": \"Research analyst\",\n  \"department\": \"Insights\",\n  \"uiRole\": \"admin\",\n  \"address\": \"1 Home Road, London, England\",\n  \"phone\": \"\",\n  \"mobile\": \"999-999-999\",\n  \"messenger\": \"johndoe121\",\n  \"apiRole\": [\n    \"BW_BASIC_USER\",\n    \"BW_ADMIN_USER\"\n  ],\n  \"ccAccess\": \"no_access\",\n  \"externalId\": null,\n  \"tags\": {\n    \"notify\": \"true\"\n  },\n  \"twoFactorAuthConfigured\": true,\n  \"blocked\": false\n}",
      "language": "json"
    }
  ]
}
[/block]