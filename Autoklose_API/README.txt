## Introduction

This is the documentation for Autoklose REST API. The requests and the responses are expected to be in JSON format.

## Usage

Generate a token from API page https://app.autoklose.com/integrations
Use it as a URI parameter 

    api_token={{your_api_token}}
Keep your API token safe.


## Pagination

The pagination is available for certain GET routes where expected results are possible to go over 25 items. Some examples are getting a list of campaigns, getting a list of contacts, etc. Each route that uses pagination is marked as such in the documentation below. 
Each paginated request has a specific JSON structure that might look something like this:

    {
        "data": [
            {
                "id": 617,
                ...
            },
            {
                "id": 618,
                ...
            },
            ... (25 results)
        ],
        "links": {
            "first": "https://api.autoklose.com/api/campaigns?page=1",
            "last": "https://api.autoklose.com/api/campaigns?page=2",
            "prev": null,
            "next": "https://api.autoklose.com/api/campaigns?page=2"
        },
        "meta": {
            "current_page": 1,
            "from": 1,
            "last_page": 2,
            "path": "https://api.autoklose.com/api/campaigns",
            "per_page": 25,
            "to": 45,
            "total": 45
        }
    }

The results from data are purposefully omitted. Additional two results are returned, links and meta. Links contain information about which page is one that is currently requested, which one would be the last, previous and the next. In order to make a successful pagination request, it is expected to follow the link for the next link. Meta contains information about the current page, what is the first item number in the request, the last page, the current path, how many items are per one page, until which item results are returned and how many are in total. Using this information, it’s easier to keep track of paginated requests. 

In general, there are two parameters related to the pagination:
* page (default value 1)
* per_page (default value 25, maximum value 100)

Ultimately, what can be seen from the example is that the first 25 campaigns are returned, there are a total of 45 and the next request to get the rest of the campaigns would be at [https://api.autoklose.com/api/campaigns?page=2](#).

## Expansion

The idea behind expansion is that, by default, it doesn't return all relationships of the requested resource. For example, while retrieving the list of campaigns, there might not be the need to get all available statistics for the campaign or all recipients of the campaign, etc. This parameter is available on the most of the API requests, and applies to the response of that request only. There are two ways of using it:
* As a comma separated string 

    expand=user,statistics
* As an array

    expand[]=user&expand[]=statistics

It is allowed to combine expansions or just use a single one.