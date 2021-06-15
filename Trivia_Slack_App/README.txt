# Play A Trivia Game Using Slack and a Postman Collection



## What does this collection do?

This allows a user to play a trivia game inside Slack.

## Prerequisites:

1. You need to Create a Postman Webhook that will invoke our Collection. Documentation for doing so is [here](https://postman.slack.com/archives/C8M04F42E/p1547111356013300)
2. You need to create a Slack Incoming Webhook (https://api.slack.com/incoming-webhooks). Fill the value of the URL of the generated Webhook in the variable `slackIncomingWebhookUrl` in PostMan.
3. You need to create a Slack Slash Command (https://api.slack.com/slash-commands). The URL that the slash command will POST to will be the URL of the Webhook you generated in Step 1.
4. Turn on Interactive Components in the Slack App you created in Step 2.(https://api.slack.com/docs/message-buttons). This helps us process the user's input such as when he presses a button or chooses an option in a slack message.
5. Make Sure that the webhook you create is in the Same environment as that of our collection.

## Workflow:

![](http://i63.tinypic.com/fyej49.png)

## The Final Application in Action:



![kapture 2019-01-11 at 14 44 22](https://user-images.githubusercontent.com/21967563/51026586-d1394a00-15b4-11e9-943d-6c68f642bd05.gif)

