## Overview
This collection allows you to configure a Discord bot to get user stats from the popular video game [Fortnite](https://www.epicgames.com/fortnite/). By leveraging the [Fortnite-API](https://fortnite-api.com/) and Postman Monitors, when a user in Discord makes a request, it automatically triggers a Monitor run in Postman and sends the information back to Discord using webhooks. 

### Steps
- Obtain [Postman API key](https://learning.postman.com/docs/developer/intro-api/#generating-a-postman-api-key).
- Populate the environment with username and environment variables.
- Run the request called "Create webhookUrl to run Monitor". Copy the `webhookUrl` from the response. This URL will be the destination of a POST request sent by the Discord Bot, which will ultimately trigger a manual monitor run.
- Set up your own Bot and [Webhooks](https://support.discord.com/hc/en-us/articles/228383668-Intro-to-Webhooks) in Discord. Copy the Webhook URL from Discord Server and the Discord Bot token.
- Copy Discord Bot code from [GitHub repo](https://github.com/seanryankeegan/postman-discordBot).
- Set up a server for your Discord Bot to be run, or just copy/paste into a [REPL environment](https://repl.it/@SeanKeegan2/DiscordPostmanFortnite-Bot#index.js) for testing.
- Make a valid request from Discord and your bot should return user stats: `!fn user <username>`.
   