With the goal of understanding how Postman collections and monitors work, this collection was created where-in you can duel with Voldemort. 

The bot (Voldemort) would have to be installed as an app in Slack Workspace and can then be accessed via [slash command](https://api.slack.com/interactivity/slash-commands) `/elder-wand`.  

**Caution: Postman monitors are not made to be used in the way in which this collection uses and Postman webhooks are still in beta .**

The following [whimsical diagram](https://whimsical.com/HmBMK8QWnoSYp3bRNceJjX) can be looked at to get a better understanding about workflow of this collection. 

![Demo GIF](https://thumbs.gfycat.com/InsecureCelebratedCapybara-size_restricted.gif)

Everything that has been done in this collection was inspired from the [Librarian.](https://the.postman.co/collections/804329-f44bd959-938e-e024-39ef-c66a9f0fa2fe?version=latest&workspace=f21c2968-b83d-485e-9360-21fc4de72be3#introduction)  

# Starting the Game
You can enter `/elder-wand` into any channel or in DM’s with `@Voldemort`

The bot responds with a ‘ok’ and initiates the game with a welcome message. 

Along with the storyline of the game, Voldemort attacks you with a spell where-in you are expected to respond with a counter spell from the given options. You will move forward if you managed to overpower the spell or you’ll lose and die as Voldemort never defends. 

# Thinking stops while building the game
The following are some of the small individual problems that I had to solve. Feel free to think about them and DM me if you have some better implementation than the one that was used.
- Spell database and a mechanism to make sure the bot doesn't win the round by using defensive spells. The player has no concept of health so the game ends only if Voldemort manages to overpower the player with offence.  
- While picking a spell, it has to be checked whether there’s a valid counter spell for the given spell. 
- As there’s only one collection and one monitor being used, the initial request as well as answered requests come in to the same collection. We have to manage the workflow accordingly.
- Persisting environment variables to keep track of various variables between runs on Postman Cloud. 

_Spoilers to all these questions ahead_

# Setting up the game

## Postman Webhook

After creating a collection and environment inside Postman, you can obtain their ID's by seeing individual `GET` requests to `https://api.postman.com/collections` and `https://api.postman.com/environments`. 

Create a monitor from the above collection with already created environment. Creating a normal monitor and one which is triggered by a webhook have a slight variation. To create a webhook triggered monitor, do the following 

With both {{environment_id}} and {{collection_id}}, send a `POST` request to `https://api.postman.com/webhooks` with the following body and header

**Body:**
```
{
    "webhook":{
        "name": "{{name of the monitor you want}}",
        "collection": "{{collection_id}}",
        "environment": "{{environment_id}}"
    }
}
```

**Header:**
```
x-api-key : {{postman_api_key}}

```

The obtained URL in the response can now be used to receive payload from Slack and trigger the monitor on Postman cloud.

## Slack App 
You can create a new slack app in any workspace by creating it [here](https://api.slack.com/apps) 

Create a new slash command with URL copied from our previous step. 

You can also get a demo webhook URL from [here](https://webhook.site/) to test the Slack integration of your app. 

## Airtable Base

Create a Airtable base following the schema mentioned below and take a note of your `{{Airtable_api_key}}` from settings. 