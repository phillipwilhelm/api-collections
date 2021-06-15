This is a Postman collection for pulling all of the friends for a specific Twitter account using the Twitter API. It is meant to allow anyone, even non-developers to pull the data they want from Twitter using the API without writing code. 

Before you can use this API collection you will have to download the Postman applications, then setup your own Twitter application at: https://developer.twitter.com/en/apps so you can make calls to the Twitter API--do not worry, it is painless, and something even a non-developer can do.

![alt text](https://kinlane-productions.s3.amazonaws.com/postman-tutorials/twitter-status-lookup/twitter-application.png "New Application")

When filling out the form, all you need is to give your app a name, description, website URL, and tell them how it will be used. You can ignore the rest of the fields. Once the application is added you can obtain your access tokens by clicking on the keys and tokens tab.

![alt text](https://kinlane-productions.s3.amazonaws.com/postman-tutorials/twitter-status-lookup/twitter-keys-and-tokens.jpg "Keys and Tokens")

The first time you create your application you will have regenerate your access token and access token secret, and then you will need all four tokens to authenticate (Don't worry those aren't my real tokens). Once you have your own tokens, go back to your Postman application and click on the Twitter Lookup Postman collection, and edit its details.

![alt text](https://kinlane-productions.s3.amazonaws.com/postman-tutorials/twitter-favorites/twitter-favorites-edit.png "Edit Collection")

Once the edit window pops up select the Authorization tab, then select to use OAuth 1.0 and add your auth data to request headers from the dropdown boxes, then add your own {{consumer_key}}, {{consumer_secret}}, {{access_token}}, and {{token_secret}} from the application you setup. 

![alt text](https://kinlane-productions.s3.amazonaws.com/postman-tutorials/twitter-favorites/twitter-favorites-auth.png "Edit Collection Authorization")

Once you have entered all your tokens you should be able to make a Twitter friends API request, passing in the Twitter handles for the users you'd like to loop using the Params tab--then hitting the send button for the request in Postman.

![alt text](https://kinlane-productions.s3.amazonaws.com/postman-tutorials/twitter-friends/postman-twitter-friends-request.png "Make Request")

Once you hit send on the request, with the proper authorization, you will see a full API response from the Twitter API in a JSON format, providing you with all the detail on each user included as part of the API request. A test script for the request will store the JSON response in the environment as a friends variable. If you want to gather more than 200 of your friends, turn on the cursor parameter and re-run the Postman collection. You can only pull 200 at a time, and there are rate limits on how often you can run it. 

![alt text](https://kinlane-productions.s3.amazonaws.com/postman-tutorials/twitter-friends/postman-twitter-friends-request-response.png "See Response")

Each Twitter friends response is pretty verbose, and requires you to wade through a lot of JSON to find what you are looking for. To help make more accessible to non-developers I made a visualizer response lists all of the Twitter accounts you are friends that have been gathered so far. You can see this by clicking on the visualizer tab for the Postman response.

![alt text](https://kinlane-productions.s3.amazonaws.com/postman-tutorials/twitter-friends/postman-twitter-friends-request-visual.png "Visualize Response")

This Postman collection should allow anyone (developer or non-developer) to work with the Twitter API and make lookups via the Twitter API to pull all the tweets favorited by any user. If you have any questions you an ping me on Twitter at [@apievangelist ](https://twitter.com/apievangelist), or via [info@apievangelist.com](mailto:info@apievangelist.com).

You can view the rest of documentation for this endpoint below, and run using the Run in Postman button in the top-right corner of this documentation. You can also find code samples in a variety of programming languages using the dropdown just below the Run in Postman button, helping you quickly integrate this API capability into your application, or you can just use the Postman collection to gather all of your own Twitter friends, store them in an environment, and run manually or automatically via a monitor--allowing you to pull your own Twitter data.

Here is the environment to run this collection--you will need to fill out with your own Twitter tokens.

```{
	"id": "c7a8d5ef-2aef-40a6-bc1e-d1b7512425c7",
	"name": "Twitter Friends",
	"values": [
		{
			"key": "consumer_key",
			"value": "[your consumer_key]",
			"enabled": true
		},
		{
			"key": "consumer_secret",
			"value": "[your consumer secret]",
			"enabled": true
		},
		{
			"key": "access_token",
			"value": "[your access token]",
			"enabled": true
		},
		{
			"key": "token_secret",
			"value": "[your token secret]",
			"enabled": true
		},
		{
			"key": "friends",
			"value": "",
			"enabled": true
		},
		{
			"key": "next_cursor",
			"value": 0,
			"enabled": true
		},
		{
			"key": "previous_cursor",
			"value": 0,
			"enabled": true
		}
	],
	"_postman_variable_scope": "environment",
	"_postman_exported_at": "2020-01-04T02:07:48.986Z",
	"_postman_exported_using": "Postman/7.14.0"
}
```