---
title: "Retrieving Workflow"
excerpt: "Listing the Workflow within your Project."
---
Workflow categories are stored within Projects. They represent special categorization behavior in the Analytics application:

* **Assignment** - A Mention can be assigned to a user by another user.
* **Priority** - A Mention can be given a priority level by a user.
* **Checked** - A Mention can be marked as checked, which can indicate  that it has been seen or interacted with by a user.
* **Status** - A Mention can be given a status level by a user.

You can access them with the associated Project ID:
[block:code]
{
  "codes": [
    {
      "code": "curl -X GET https://api.brandwatch.com/projects/398748937/workflow",
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
      "code": "[\n  {\n    \"id\": 587088,\n    \"name\": \"Assignment\",\n    \"children\": [\n      {\n        \"id\": 587093,\n        \"name\": \"colleague@example.com\",\n        \"ordering\": -1\n      },\n      {\n        \"id\": 588907,\n        \"name\": \"anothercolleague@example.com\",\n        \"ordering\": -1\n      }\n    ]\n  },\n  {\n    \"id\": 587075,\n    \"name\": \"Priority\",\n    \"children\": [\n      {\n        \"id\": 587076,\n        \"name\": \"high\",\n        \"ordering\": 1\n      },\n      {\n        \"id\": 587077,\n        \"name\": \"medium\",\n        \"ordering\": 2\n      },\n      {\n        \"id\": 587078,\n        \"name\": \"low\",\n        \"ordering\": 3\n      }\n    ]\n  },\n  {\n    \"id\": 587091,\n    \"name\": \"Checked\",\n    \"children\": [\n      {\n        \"id\": 587092,\n        \"name\": \"yes\",\n        \"ordering\": -1\n      }\n    ]\n  },\n  {\n    \"id\": 587079,\n    \"name\": \"Status\",\n    \"children\": [\n      {\n        \"id\": 587080,\n        \"name\": \"open\",\n        \"ordering\": 1\n      },\n      {\n        \"id\": 587081,\n        \"name\": \"pending\",\n        \"ordering\": 2\n      },\n      {\n        \"id\": 587082,\n        \"name\": \"closed\",\n        \"ordering\": 3\n      }\n    ]\n  }\n]",
      "language": "json"
    }
  ]
}
[/block]
You can then use these Workflow category names when filtering or breaking down Mention calls.