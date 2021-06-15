The Sushi Selector ???? is a Postman collection that recommends a nearby sushi spot. When run locally with the Postman collection runner, the collection searches for sushi restaurants and posts the recommendation as a direct message to your Twitter. 

You can customize Sushi Selector's criteria such as location, distance, and price range with environment variables. If you don't like sushi (????), you can tweak the collection to search for the cheapest burger joint, the nearest park, or the highest rated tourist attractions. 

### Quickstart

Before you can run the Sushi Selector collection, you need to [create or update an environment](https://www.getpostman.com/docs/v6/postman/environments_and_globals/manage_environments). Add the following required variables to a new environment, or update the `Sushi Selector.template` environment you downloaded with the **Run in Postman** button:

|Environment Variable Name |Description
|--------------------------|--------------
|`googlePlacesApiKey`            |[A Google Places API Key](https://developers.google.com/places/web-service/get-api-key)
|`googleMapsGeocodingApiKey`        |[A Google Maps Geocoding API Key](https://developers.google.com/maps/documentation/geocoding/start#get-a-key)
|`address`                |Specifies the combination of address, neighborhood, city, state, or zip to be used when searching for places. This will be geocoded into a latitude and longitude.
|`myTwitterHandle`                 |Your Twitter Handle to send yourself a direct message
|`twitterConsumerKey`, `twitterConsumerSecret`, `twitterAccessToken`, and `twitterAccessTokenSecret`  | [Your Twitter app's auth credentials](https://apps.twitter.com/) to set up OAuth 1.0

### Get Google Places API Key

You will need a [Google Places API Key](https://developers.google.com/places/web-service/get-api-key) to add or update the `googlePlacesApiKey` value within the Postman environment.

### Get Google Maps Geocoding API Key

You will need a [Google Maps Geocoding API Key](https://developers.google.com/maps/documentation/geocoding/start#get-a-key) to add or update the `googleMapsGeocodingApiKey` value within the Postman environment.

### Enter an Address

Save the address of the location you want to search around as `address`. You can use a combination of address, neighborhood, city, state, or zip to initiate your search.

### Enter your Twitter handle

Save your Twitter handle as `myTwitterHandle` within the Postman environment. You will need this to send yourself a direct message via Twitter.

### Get Twitter credentials to set up Oauth 1.0

You will need to [create a Twitter app](https://apps.twitter.com/) to get the `twitterConsumerKey`, `twitterConsumerSecret`, `twitterAccessToken`, and `twitterAccessTokenSecret` values for the Postman environment. For step-by-step screenshots and instructions on setting up Twitter Oauth 1.0 in Postman, check out the [first Twitter request](link to twitter request).
