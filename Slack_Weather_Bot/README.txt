This collection acts as a weather bot for you which posts the current weather to a specified Slack channel.

### Setup:

For the setup, you will need three things.

1. **Google Maps API Key**: You can generate an API Key using this [link](https://developers.google.com/maps/documentation/geocoding/get-api-key)
2. **DarkSky API Key**: The DarkSky API returns weather conditions based on a particular latitude and longitude. You would be needing an API Key to use it. Head to [DarkSky Dev](https://darksky.net/dev) and register for a free account and generate an API Key.
3. **Slack Webhook URL**: Slack allows you to generate incoming webhooks for your team using which you can send a message to a specific channel or user. Go to [Slack](https://api.slack.com/incoming-webhooks) to learn more about how you can generate one.

Once you have all these three, you can add them to the attached environment and your collection is ready for use.

A sample weather report on Slack would look something like this.

![Example](https://user-images.githubusercontent.com/6972850/47005820-361a0b00-d152-11e8-8386-fa82df283821.png)
