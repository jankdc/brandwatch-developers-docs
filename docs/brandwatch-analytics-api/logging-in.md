---
title: "Logging in"
excerpt: "This page will show you how to get logged in to the application."
---
Logging into the application as an API User involves a request to the `/oauth/token` endpoint.
[block:api-header]
{
  "type": "post",
  "title": "1. Getting a token"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "curl -X POST https://api.brandwatch.com/oauth/token --data \"username=[your@username.com]&password=[yourpassword]&grant_type=api-password&client_id=brandwatch-api-client\"",
      "language": "curl"
    }
  ]
}
[/block]
If successful, you will receive a JSON response similar to the following:
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"access_token\": \"aa000000-0aaa-0000-0a00-aa00a000a00a\",\n  \"token_type\": \"bearer\",\n  \"expires_in\": 31535999,\n  \"scope\": \"read trust write\"\n}",
      "language": "json"
    }
  ]
}
[/block]
The access_token value can now be submitted with any other request to the Brandwatch API and it will grant you access to the API.

The `expires_in` field informs you how long (in seconds) the access token is valid for, the default for an API User is one year.
[block:api-header]
{
  "type": "get",
  "title": "2. Using your token"
}
[/block]
Once you have an access token you now have access to all of the API. When making a request the token can be submitted in one of two ways:

1. In the request Headers in the format `Authorization: bearer [ACCESS TOKEN]`
2. In the URL as a parameter `&access_token=[ACCESS TOKEN]`

For the sake of brevity, we do not include the passing of the token in all of our documented calls. However, here is an example of what it would look like with cURL:
[block:code]
{
  "codes": [
    {
      "code": "curl ­-X GET https://api.brandwatch.com/projects/summary.json -­H\n\"Authorization: bearer xxxx-xxxx-xxxx-xxxx”",
      "language": "curl"
    }
  ]
}
[/block]