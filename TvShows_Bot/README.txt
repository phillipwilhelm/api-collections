This collection was created to better understand how Postman collections, collection runners and monitors work.

The bot (TvShows) should have to be installed as an App in your Slack Workspace and can then be accessed via [slash command](https://api.slack.com/interactivity/slash-commands) `/next-episode`.

**Caution: Postman Monitors are not made to be used the way this collection uses them. Moreover Postman Webhooks are an undocumented Postman feature.**

The following [Whimsical](whimsical.com) diagram can help to get a better understanding of this collection's workflow:

[https://whimsical.com/tvshows-bot-MZ8rKMCxD46wYYyLCxN27p](https://whimsical.com/tvshows-bot-MZ8rKMCxD46wYYyLCxN27p)

## Starting the bot
You can enter `/next-episode [tv-show]` into any channel.

The bot responds with a ‘ok’ and a list of show with a similar name will be displayed:

![Search result](https://i.imgur.com/axk9MIo.png "Search Result")

You can now click the show you are interested in and the bot will return information on the next airing episode:

![Next episode](https://i.imgur.com/5QZory6.png "Next episode")

If no show or no next episode is available, the bot will respond with the corresponding message:

![Show not found](https://i.imgur.com/ubtZJmA.png "Show not found")
![No next episode](https://i.imgur.com/7isAbYB.png "No next episode")

## Setting up your forked collection
### Postman Webhook
After forking this collection and environment inside Postman, you can obtain their ID's by seeing individual GET requests to `https://api.postman.com/collections` and `https://api.postman.com/environments` or through the GUI.

![Collection id](https://i.imgur.com/dEa2lWD.png "Collection id")

With both `{{environment_id}}` and `{{collection_id}}`, send a POST request to https://api.postman.com/webhooks with the following body and header in order to create the Webhook:

**Body**
```
{
  "webhook": {
    "name": "{{name of the monitor}}",
    "collection": "{{collection_id}}",
    "environment": "{{environment_id}}"
  }
}
```
**Header**
```
x-api-key : {{postman_api_key}}
```

The response will look something like:

```
{
    "webhook": {
        "id": "853dec4e-4f5d-438f-841a-8196464d855e",
        "name": "TvShowsWebhookMonitor",
        "collection": "0c6e4d43-3921-4447-97e1-6773c4bb4269",
        "environment": "7d1d14f0-e675-4450-ae12-4515defd59fd",
        "webhookUrl": "https://newman-api.getpostman.com/run/XXXXXX/a128a2f9-4b86-46d1-9ff3-68c945f3639c",
        "uid": "c6229a1a-cb7b-460b-8e59-ce07ddb5649d"
    }
}
```
The `webhookUrl` in the response can now be used to receive payload from Slack and trigger the monitor on Postman cloud.

## Slack App
You can create a new Slack app in any workspace by creating it here

Create a new slash command with URL copied from the previous step. Then activate the Interactivity feature in the `Interactivity & Shortcuts` section and add the same URL in the `Request URL` field.

![Slack config](https://i.imgur.com/H88nqyH.png "Slack config")

## Trakt API

Register to [Trakt.tv](https://trakt.tv), then create a new [app](https://trakt.tv/oauth/applications/new), and set the Postman enviroment variables for `trakt_client_id` and `trakt_client_secret` with the ones of your new Trakt app.

![Trakt config](https://i.imgur.com/H88nqyH.png "Trakt config")

![Postman env variables](https://i.imgur.com/gcUwGJQ.png "Postman env variables")
