![An example Slack post](https://i.imgur.com/2YJeB28.png "An example Slack post with restaurant picks from Lunch Picker running as an 8am monitor.")

Lunch Picker is a [Postman collection](https://www.getpostman.com/docs/postman/collections/creating_collections) that acts as a restaurant discovery service powered by the [Yelp Fusion API](https://www.yelp.com/developers/documentation/v3). When run, the collection suggests places for you or a team to have lunch and posts the suggestions to Slack. It can be run locally with the [Postman collection runner](https://www.getpostman.com/docs/postman/collection_runs/starting_a_collection_run) or with [Newman](https://www.getpostman.com/docs/postman/collection_runs/command_line_integration_with_newman), or as a scheduled remote job with [Postman Monitors](https://www.getpostman.com/docs/postman/monitors/intro_monitors).

You can [customize Lunch Picker's restaurant selection criteria](#cc479560-f6cf-f199-1757-65d9f051a324) such as location, distance, and price range with environment variables. The collection saves its choice history to a [Postman environment](https://www.getpostman.com/docs/postman/environments_and_globals/manage_environments) after each run to ensure future choices don't become repetitive.


# Getting Started

Before you can run the Lunch Picker collection, you need to create or update an [environment](https://www.getpostman.com/docs/postman/environments_and_globals/manage_environments). Add the following required variables to a new environment, or update the `Lunch Picker.template` environment you downloaded with the *Run in Postman* button:

|Environment Variable Name |Required? |Description
|--------------------------|----------|--------------
|`yelpClientID`            |**YES**   |[A Yelp client ID.](https://www.yelp.com/developers/documentation/v3/authentication)
|`yelpClientSecret`        |**YES**   |[A Yelp client secret.](https://www.yelp.com/developers/documentation/v3/authentication)
|`location`                |**YES**   |Specifies the combination of address, neighborhood, city, state or zip, and optional country to be used when searching for restaurants.
|`webhook`                 |**YES**   |[A Slack incoming webhook url.](https://api.slack.com/incoming-webhooks)
|`postmanApiKey`           |**YES**   |[A Postman Pro API key.](https://docs.api.getpostman.com/#authentication)
|`environmentID`           |**YES**   |The id of your environment. Download your environment and copy the id, or get the id from the [Postman API](https://docs.api.getpostman.com/).



## Get a Yelp Client ID and Secret

You will need to [Create a Yelp app](https://www.yelp.com/developers/documentation/v3/authentication) to get the `yelpClientID` and `yelpClientSecret` values.


## Enter a Location

Save the address of the location you want to search as `location`. The address should be in a region where Yelp is available, otherwise you won't get any results.


## Get a Slack Webhook Url

Log in to your team Slack account and [create a Slack app](https://api.slack.com/slack-apps). Then [activate and configure an incoming webhook](https://api.slack.com/incoming-webhooks) for your app. Add this webhook url as `webhook` in your environment.


## Get a Postman Pro API Key

Log in to your online Postman account and [get an API key](https://the.postman.co/dashboard/integrations/pm_pro_api/list) for the [Postman API](https://docs.api.getpostman.com/), then add `postmanApiKey` to your environment.


## Get Your Environment ID

Once you've created your environment, you can get the `environmentID` value by downloading the environment and copying the id from the environment file.

Try running the collection locally using the [Postman collection runner](https://www.getpostman.com/docs/postman/collection_runs/starting_a_collection_run) or [Newman](https://www.getpostman.com/docs/postman/collection_runs/command_line_integration_with_newman). It should get restaurant results for your location and post them to your Slack channel. If it doesn't, check the run results and the Postman console to see what might have gone wrong.

![A successful run](https://i.imgur.com/PqvXcc6.png "A succesful run in the collection runner.")


# Going Further

You can [customize the behavior of Lunch Picker with optional environment variables](#cc479560-f6cf-f199-1757-65d9f051a324). Try updating the search radius or the price range to improve your results, or set favorite restaurants to increase the chance of those restaurants being picked. Once you have the settings you want, [create a monitor](https://www.getpostman.com/docs/postman/monitors/intro_monitors) to get periodic recommendations. _Bon appétit!_