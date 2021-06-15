# Postman Air Quality Collection
**Welcome to the Postman Air Quality Collection.**
This collection was created in response to the 2017 wildfires that devastated Northern California. The fires brought tragedy, and also caused hazardous ash and smoke pollution in the surrounding areas. As Postman has an office in San Francisco, we thought it was important to help our fellow Northern Californians and the rest of the world stay aware of the air quality in their surroundings.

This collection gets air quality updates from the AccuWeather API and posts them to Twitter according to your account and location specifications. 


## Technologies Used
1. **Postman** - This collection utilizes [Postman Collections](https://www.getpostman.com/docs/postman/collections/creating_collections), [Postman Monitors](https://www.getpostman.com/docs/postman/monitors/intro_monitors), and [Postman Environments](https://www.getpostman.com/docs/postman/environments_and_globals/manage_environments).

2. **AccuWeather API** - [AccuWeather’s API](https://developer.accuweather.com/home) allows users to obtain real weather data, including air quality data.

  * **Using the AccuWeather API** - 
  To use AccuWeather’s API you will need to create an account and obtain a trial API key from their website. You can make up to 50 calls to the API per day on the trial, which should be enough to run this collection as an individual user.

3. **Twitter** - We’ve chosen to use the [Twitter API](https://developer.twitter.com/en/docs/basics/getting-started)  as a platform to reach out to our community and spread the message about the state of the San Francisco air quality since the Northern California fires have started. You can configure your own Twitter account to post periodic air quality updates.

  * **Using the Twitter API** - 
  To use Twitter’s API, you will need to create [a Twitter app](https://apps.twitter.com/) and get OAuth credentials.

## Environment Variables
You need to set several environment variables before this collection will run:

|Environment Variable Name |Description
|--------------------------|--------------
|`location`                |A string describing the location you would like to monitor
|`accuweatherApiKey`       |An [AccuWeather API key](https://developer.accuweather.com/home)
|`twitterConsumerKey`      |[A Twitter OAuth Consumer Key](https://developer.twitter.com/en/docs/basics/getting-started)
|`twitterConsumerSecret`   |[A Twitter OAuth Consumer Secret](https://developer.twitter.com/en/docs/basics/getting-started)
|`twitterAccessToken`      |[A Twitter OAuth Access Token](https://developer.twitter.com/en/docs/basics/getting-started)
|`twitterAccessSecret`     |[A Twitter OAuth Access Token Secret](https://developer.twitter.com/en/docs/basics/getting-started)