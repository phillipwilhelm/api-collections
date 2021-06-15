##Overview
This is a Postman collection for quickly getting up and running with just making Twitter searches for many of the common search terms for the COVID-19 / Coronavirus pandemic using the Twitter Recent Search API.

## Twitter Recent Search (Labs)
The [Twitter Labs recent search endpoint](https://developer.twitter.com/en/docs/labs/recent-search/overview) represents the future implementation of Twitter search endpoints.  This Labs endpoint provides developers API access to public Tweets posted in the previous seven days. Labs recent search is a RESTful endpoint that receives a single search query and responds with matching Tweets. Tweets are delivered in reverse-chronological order, starting with the most recent Tweets. The endpoint uses OAuth 2.0 Bearer Token authentication. 

Up to 100 Tweets are returned per request, and pagination tokens are provided for paging through large sets of matching Tweets. Search queries can be created with over 15 "operators" that match on Tweet attributes, such as message keywords, hashtags, and URLs. Operators and rule clauses can be combined with boolean logic and parentheses to help refine the filter's matching behavior. Queries can be up to 512 characters long.

Labs recent search requests support the Labs fields and expansions parameters, and return the new Labs Tweet JSON design shared by the other Labs endpoints. 

Labs recent search supports navigating the Tweet archive by time ranges and Tweet ID ranges. Recent search is designed to support two common use patterns: 

- **"Get historical"**: Requests are for a period of interest, with no focus on the real-time nature of the data. A single request is made, and all matching data is delivered using pagination as needed. This is the default mode for Labs recent search.
- **"Polling" or "listening"**: Requests are made in a "any new Tweets since my last request?" mode. Requests are made on a continual basis, and typically there is a use case focus on near real-time 'listening' for Tweets of interest. 
 
Learn more about these topics:

- **Building search queries** - Labs recent search supports 15 operators that match on Tweet attributes. Queries can be short and simple or can be a complex set of filters with up to 512 characters. Building effective queries is an iterative process. 
- **Making search API requests** -  Labs recent search requests are made using the HTTP GET method and "app-only" (Oauth 2.0) authentication. See the Labs recent search Quick Start guide for help with making your first request. To learn more about request parameters, see the API Reference for more details.
 - **Pagination** - Since most search queries will match more Tweets than can be returned in an API response, the Labs recent search endpoint will split the data payload into multiple 'pages.' The endpoint supports simple pagination methods to assemble Tweets collections.
 
This is a standalone Postman collection dedicated just to the recent search endpoint, created by Postman in an effort to highlight the potential of this particular endpoint while reducing the cognitive load with anyone who is first putting this collection, or any derivative collection build from this collection. Making it easier to get up and running with the [Twitter Rececnt Search API](https://developer.twitter.com/en/docs/labs/recent-search/overview).

## Twitter Developer Account
Before you can use this collection you will need to apply for a Twitter developer account, which is an extra step you can take using any existing Twitter account, over at [dev.twitter.com](https://developer.twitter.com).

<img src="https://kinlane-productions.s3.amazonaws.com/postman-tutorials/twitter-recent-search-api/1-twitter-developer.jpg" width="100%" align="center">

## Apply For API Access
In an effort to address abuse Twitter requires developers to provide a significant amount of information about what they plan on building, making the one-time developer sign up process something that will take you a few minutes--[header over to dev.twitter.com and apply](https://developer.twitter.com/en/apply-for-access).

<img src="https://kinlane-productions.s3.amazonaws.com/postman-tutorials/twitter-recent-search-api/2-apply-for-access.jpg" width="100%" align="center">

## Twitter Application
Once you have an approved Twitter developer account, you will need to create an application before you are given keys to actually begin making calls to the Twitter API. To [create a new application you need to head to the application area](https://developer.twitter.com/en/apps/create) within your Twitter developer account.

<img src="https://kinlane-productions.s3.amazonaws.com/postman-tutorials/twitter-recent-search-api/4-add-application.jpg" width="100%" align="center">

## API Keys
Once you have completed the creation of your new Twitter application you can retrieve your API keys using the "keys and tokensa" tab, providing what you need to make this collection work.

<img src="https://kinlane-productions.s3.amazonaws.com/postman-tutorials/twitter-recent-search-api/5-get-api-keys.jpg" width="100%" align="center">
<p align="center"><strong><em>tokens displayed are not real</em></strong></p>

## Twitter Labs
Before your keys will work you need to do one more thing, [join the Twitter developer labs program](https://developer.twitter.com/en/account/labs), and active the recent search API and associate with your Twitter developer account and application.

<img src="https://kinlane-productions.s3.amazonaws.com/postman-tutorials/twitter-recent-search-api/6-twitter-developer-lab.jpg" width="100%" align="center">

## Postman Authentication
Now that you have your keys you will have to add them to the environment for this Postman collection, connecting the dots between this collection and your Twitter application.

<img src="https://kinlane-productions.s3.amazonaws.com/postman-tutorials/twitter-recent-search-api/7-add-to-environment.jpg" width="100%" align="center">
<p align="center"><strong><em>tokens displayed are not real</em></strong></p>

## Obtain Bearer Token
With your API keys entered into the environment for this collection you can use the "Generate Authentication Token" request to obtain and store the bearer token in the environment for this collection, allowing it to be used for making search requests.

<img src="https://kinlane-productions.s3.amazonaws.com/postman-tutorials/twitter-recent-search-api/8-auth-token.png" width="100%" align="center">

## Twitter Recent Search
Now the Twitter recent search endpoint should work for you, allowing you to adjust the query parameters to find exactly the search you desire. Using Twitter next generation search to make sense of any conversation occurring via Twitter.

<img src="https://kinlane-productions.s3.amazonaws.com/postman-tutorials/twitter-recent-search-api/9-next-generation-search.png" width="100%" align="center">

If you need further information you can visit [the Twitter Developer Labs Recent Search API (V2) documentation](https://developer.twitter.com/en/docs/labs/recent-search/overview). Hopefully this collection gets you what you need to make on-boarding with the Twitter recent search API easier.