![An example Slack post](https://i.imgur.com/2YJeB28.png "An example Slack post with restaurant picks from Lunch Picker running as an 8am monitor.")

Lunch Picker is a [Postman collection](https://www.getpostman.com/docs/postman/collections/creating_collections) that acts as a restaurant discovery service, powered by the [Yelp Fusion API](https://www.yelp.com/developers/documentation/v3). It suggests places for you or a team to have lunch and posts them to Slack, and can be run locally with the [Postman collection runner](https://www.getpostman.com/docs/postman/collection_runs/starting_a_collection_run) or with [Newman](https://www.getpostman.com/docs/postman/collection_runs/command_line_integration_with_newman), or as a scheduled remote job with [Postman Monitors](https://www.getpostman.com/docs/postman/monitors/intro_monitors).

You can [customize Lunch Picker's restaurant selection criteria](#cc479560-f6cf-f199-1757-65d9f051a324) such as location, distance, and price range with environment variables. The collection automatically saves its choice history to a [Postman environment](https://www.getpostman.com/docs/postman/environments_and_globals/manage_environments) after each run, using that history to make sure the choices stay interesting each time it's run.


# Getting Started

Before you can run the Lunch Picker collection, you need to create or update an [environment](https://www.getpostman.com/docs/postman/environments_and_globals/manage_environments). Add the following required variables to a new environment, or update the `Lunch Picker.template` environment you downloaded with the *Run in Postman* button:

|Environment Variable Name |Description
|--------------------------|--------------
|`yelpClientID`            |[A Yelp client ID.](https://www.yelp.com/developers/documentation/v3/authentication)
|`yelpClientSecret`        |[A Yelp client secret.](https://www.yelp.com/developers/documentation/v3/authentication)
|`location`                |Specifies the combination of address, neighborhood, city, state or zip, and optional country to be used when searching for restaurants.
|`webhook`                 |[A Slack incoming webhook url.](https://api.slack.com/incoming-webhooks)
|`postmanApiKey`           |[A Postman API key.](https://docs.api.getpostman.com/#authentication)
|`environmentID`           |The id of your environment. Download your environment and copy the id, or get the id from the [Postman API](https://docs.api.getpostman.com/).



## Get a Yelp Client ID and Secret

You will need to [Create a Yelp app](https://www.yelp.com/developers/documentation/v3/authentication) to get the `yelpClientID` and `yelpClientSecret` values. This takes just a few clicks.


## Enter a Location

Save the address of the location you want to search around as `location`. This should work in any country where Yelp is active.


## Get a Slack Webhook Url

Log in to your team Slack account and [create a Slack app](https://api.slack.com/slack-apps). Then [activate and configure an incoming webhook](https://api.slack.com/incoming-webhooks) for your app. Add this webhook url as `webhook` in your environment.


## Get a Postman Pro API Key

Log in to your online Postman account and [get an API key](https://the.postman.co/dashboard/integrations/pm_pro_api/list) for the [Postman API](https://docs.api.getpostman.com/), then add `postmanApiKey` to your environment.


## Get Your Environment ID

Once you've created your environment, you can get the `environmentID` value by downloading the environment and copying the id from the environment file.

Try running the collection locally using the [Postman collection runner](https://www.getpostman.com/docs/postman/collection_runs/starting_a_collection_run) or [Newman](https://www.getpostman.com/docs/postman/collection_runs/command_line_integration_with_newman). It should get restaurant results for your location and post them to your Slack channel. If it doesn't, check the run results and the Postman console to see what might have gone wrong.

![A successful run](https://i.imgur.com/PqvXcc6.png "The results of a succesful run in the Postman collection runner.")


# Going Further

You can [customize the behavior of the lunch picker with optional environment variables](#cc479560-f6cf-f199-1757-65d9f051a324). Try updating the search radius or the price range to improve your results, or even set favorite restaurants to improve the chance of those restaurants being picked. Once you have the settings you want, [set up a monitor](https://www.getpostman.com/docs/postman/monitors/intro_monitors) to get periodic recommendations. _Bon appétit!_